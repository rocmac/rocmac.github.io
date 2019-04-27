---
layout: post
title:  oracle procedure
date:   2019-04-27 00:00:00 +0300
categories: DB
tag: [DB] # add tag
---

* content
{:toc}


今天接到紧急任务配置系统流程，基本上流程和数据都是乱的，发现错误数据500余条，需要当天处理完毕，发现手工处理基本无望，只能捡起N久不用的存储过程技能包，简单记录一下吧

--------

简单来说就说遍历流程id，找到流程节点比流程数量多的任务，然后去掉多余的数据

```
DECLARE
CURSOR c_dept IS select * from tw_process where process_id like '918%';
r_dept c_dept%rowtype;
r_trans tw_process_transition%rowtype;
r_number NUMBER;

BEGIN
OPEN c_dept;
LOOP
FETCH c_dept into r_dept;
EXIT WHEN c_dept%NOTFOUND;

select count(*) into r_number
from (
select to_task_id from tw_process_transition where process_id = r_dept.process_id
MINUS
select task_id from tw_process_task t where t.process_id = r_dept.process_id);

if r_number = 0 then
continue;

ELSE

DBMS_OUTPUT.PUT_LINE('process_id:'||r_dept.process_id||'==='||r_trans.to_task_id);

END IF;
END LOOP;
CLOSE c_dept;
END;
```