---
layout: post
title:  Spring Boot Unit Test
date:   2019-06-19 00:00:00 +0300
categories: ssh
tag: [ssh] # add tag
---

* content
{:toc}


## 概述

当前国内项目开发中很少有写完整单元测试的习惯，个人觉得主要有以下几个原因：
1. 项目进度太赶，赶紧开发完功能甚至连测试都不充分就上线了，根本没时间写单元测试
2. 单元测试还是有一些技巧要掌握的，比如要Mock一些上下文等，一些小伙伴没掌握或者嫌麻烦
3. 意识问题，觉得单元测试比较麻烦，代码经常动的话还得改测试用例
所以一般的公司很难有一些团队合作的高质量代码完成

个人觉得单元测试意义还是非常大的，一些核心的接口写好单元测试用例能够节省不少时间，保证质量，这里简单记录一下Spring boot的单元测试。

---

### 工具

这里依然使用VS Code，报告执行情况一目了然，方法上面有run/debug执行按钮随时随地随心情执行


### 小插曲

执行Unit Test报错：

```
EL1008E: Property or field 'timestamp' cannot be found on object of type 'java.util.HashMap' 
```

简单粗暴的拦截了返回的error

```
@RequestMapping("/error")
    public String error() {
        System.out.println("ErrControlller.error");
        return "err"; // 不使用/error， 可以返回其他的， 但是要保证这个视图存在， 比如存在 public/err.html 
    }
```

### 常用注解

常规操作不解释了

```
    @Autowired
    private WebApplicationContext wac;
    
    @Autowired
    PersonsRepository personsRepository;

    @Before
    public void setUp() throws Exception {
        this.mvc= MockMvcBuilders.webAppContextSetup(wac).build();
    }

    @After
    public void destroy() throws Exception {
    }
```

### 接口测试示例

需要了解一下如何判定返回值：
[JsonPath 使用深入了解一下](https://blog.csdn.net/koflance/article/details/63262484)

访问参数:  .param("page", "1")

返回的json中第二级的参数值assert: .andExpect(jsonPath("$..count").value(7))

返回值判断（记得加转义符）：.andExpect(content().string(equalTo("")))


```
    @Test
    public void testCase() throws Exception {
        // mvc.perform(MockMvcRequestBuilders.get("/api/person/persons?sex=male").accept(MediaType.APPLICATION_JSON))
        // .andExpect(content().contentType(MediaType.APPLICATION_JSON));
        RequestBuilder request = null;

        request = get("/api/persons")
                .param("page", "1")
                .param("sex", "")
                .param("email", "");
        mvc.perform(request).andExpect(status().isOk())
                .andExpect(jsonPath("$..count").value(7))
                .andDo(print());
        // .andExpect(content().contentType(MediaType.APPLICATION_JSON_VALUE));
                // .andExpect(content().string(equalTo("[]")));


        request = get("/api/persons/sex");
        mvc.perform(request).andExpect(status().isOk())
                .andExpect(content().string(equalTo("[{\"label\":\"female\",\"value\":\"female\"},{\"label\":\"male\",\"value\":\"male\"}]")))
                .andDo(print());
    }
```