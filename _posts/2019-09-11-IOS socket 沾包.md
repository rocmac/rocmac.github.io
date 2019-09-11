---
layout: post
title:  IOS socket 沾包
date:   2019-09-11 00:00:00 +0300
categories: IOS
tag: [IOS, socket] # add tag
---

* content
{:toc}


## 背景

由于产品中有IM相关功能，在测试中发现IOS app会有10%左右的几率丢消息，查看代码会发现代码在校验消息长度与消息头中的长度不一致时会直接丢弃掉该消息

## 沾包原因

我们一般使用的是基于TCP的流式Socket，因此本文也主要讲解这一种方式，TCP是一种流协议（stream protocol）。这就意味着数据是以字节流的形式传递给接收者的，没有固有的"报文"或"报文边界"的概念。从这方面来说，读取TCP数据就像从串行端口读取数据一样--无法预先得知在一次指定的读调用中会返回多少字节（也就是说能知道总共要读多少，但是不知道具体某一次读多少）

简单来说就是底层协议会拆包，同一个消息内容会分两次发送

问题代码如下：

```
if(length >16){
    int headLength =[self data2int: [data subdataWithRange:NSMakeRange(4, 2)] length:2];
    int version =[self data2int: [data subdataWithRange:NSMakeRange(6, 2)] length:2];
    int opration =[self data2int: [data subdataWithRange:NSMakeRange(8, 4)] length:4];
    int seqId = [self data2int: [data subdataWithRange:NSMakeRange(12, 4)] length:4];
    NSRange rangeData  = NSMakeRange( 16, length-16);
    if (data.length < (rangeData.length+16)) {
        return;
    }
```

## 解决方案

在发现消息头的长度比实际消息长时，且下一条消息小于4个字节（4字节为消息头的长度），则直接拼接到上一条消息中，组成完整的消息格式

```
-(void) didReadData:(NSData *)data {
    
    //将接收到的数据保存到缓存数据中
    [self.cacheData appendData:data];;

    // 取出4-8位保存的数据长度，计算数据包长度
    NSData *dataLength = [_cacheData subdataWithRange:NSMakeRange(4, 4)];
    int dataLenInt = CFSwapInt32BigToHost(*(int*)([dataLength bytes]));
    NSInteger lengthInteger = 0;
    lengthInteger = (NSInteger)dataLenInt;
    NSInteger complateDataLength = lengthInteger + 8;//算出一个包完整的长度(内容长度＋头长度)
    NSLog(@"data = %ld  ----   length = %d  ",data.length,dataLenInt);
    
    //因为服务号和长度字节占8位，所以大于8才是一个正确的数据包
    while (_cacheData.length > 8) {
        
        if (_cacheData.length < complateDataLength) { //如果缓存中的数据长度小于包头长度 则继续拼接

            [[SingletonSocket sharedInstance].socket readDataWithTimeout:-1 tag:0];//socket读取数据
            break;
            
        }else {
            
            //截取完整数据包
           NSData *dataOne = [_cacheData subdataWithRange:NSMakeRange(0, complateDataLength)];
            [self handleTcpResponseData:dataOne];//处理包数据
            [_cacheData replaceBytesInRange:NSMakeRange(0, complateDataLength) withBytes:nil length:0];
            
            if (_cacheData.length > 8) {
                
                [self didReadData:nil];
                
            }
        }
    }
}
```