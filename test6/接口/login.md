﻿
# 接口：login  [返回](../README.md)
用例： [登录](../用例/登录.md)

- 功能：
    登录到平台。
    
- 权限：
    访客。    
    
- API请求地址： 
    接口基本地址/v1/api/login

- 请求方式 ：
    POST

- 请求实例：

        {
            "id":"2015104124",
            "password":"xf456756",
            "type":"学生"
        }
        
- 请求参数说明:        

  |参数名称|说明|
  |:---------:|:--------------------------------------------------------|      
  |id|学生学号或者老师的工号，由type决定。|
  |password|用户的密码，不是原文，是加密后的字符串| 
  |type|用户类型，学生或者老师|
  
- 返回实例：

        { 
            "status": 200,
            "info": "OK",    
        }
 
- 返回参数说明：    
 
  |参数名称|说明|
  |:---------:|:--------------------------------------------------------|      
  |status|INT类型，200表示请求成功|
  |info|返回结果说明信息|


