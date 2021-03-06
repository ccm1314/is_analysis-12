﻿
# 接口：getTeacherInfo  [返回](../README.md)
用例： [查看用户信息](../用例/查看用户信息.md),[修改用户信息](../用例/修改用户信息.md)

- 功能：
    查看教师的所有信息。
    
- 权限：
    老师：查看自己的信息，必须先登录。    
    
- API请求地址： 
    接口基本地址/v1/api/getUserInfo/<user_id>

- 请求方式 ：
    GET
      
- 请求参数说明:        

  |参数名称|说明|
  |:---------:|:--------------------------------------------------------|      
  |teacher_id|老师的ID号。对应表TEACHERS.TEACHER_ID的值|
  
- 返回实例：

        {         
            "status": true,
            "info": null,
            "ID":"2013452",    
            "name":"小张",
            "class_dept":"信息科学与工程学院"
            "github_username":"zwdbox",
            "type":"教师",            
            "semester":"0", 
            "course":"信息系统分析与设计", 
        }
 
- 返回参数说明：    
 
  |参数名称|说明|
  |:---------:|:--------------------------------------------------------|      
  |status|bool类型，true表示正确的返回，false表示有错误|
  |info|返回结果说明信息|
  |ID|工号|
  |name|用户的真实姓名|  
  |class_dept|学院名称|
  |github_username|gitHub用户名|
  |type|用户类型：老师|
  |semester|0代表第一学期，依此类推|
  |course|课程名称|

