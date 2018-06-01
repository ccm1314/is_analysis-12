# 实验五：图书管理系统数据库设计与界面设计
|学号|班级|姓名|
|:-------:|:-------------: | :----------:|
|201510414124|软件(本)15-1|熊峰|

## 1.数据库表设计
## 1.1. 图书表
|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|bookId|integer(10)|主键|否||||
|bookISBN|varchar2(100)||否||||
|bookName|varchar2(100)| |否||||
|publisher|varchar2(50)||否|||出版社|
|totalStock|integer||否|||总的库存|
|author|varchar2(50)||否||||
|summary|varchar2(100)| |是|||描述|

## 1.2. 读者表
|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|readerId|integer(10)|主键|否||||
|readerName|varchar2(20)||否||||
|bookId|integer(10)|外键|否|||与借书信息相关联|
|lendBookTime|varchar2(100)||否|||借书时间|
|returnBookTime|varchar2(100)||否|||还书时间|

## 1.3. 管理员表

|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|mangerId|integer(10)|主键|否||||
|mangerName|varchar2(20)||否||||
|mangerNumber|integer||否|||管理员编号|
|mangerAddress|varchar2(100)||否||||
|mangerPhone|varchar2(100)||否||||
## 1.4. 超级管理员表

|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|superMangerId|integer(10)|主键|否||||
|superMangerName|varchar2(20)||否||||
|mangerId|integer(10)|外键|否|||关联普通管理员|
|superMangerNumber|integer(10)||否|||只有一个超级管理员编号|
|superMangerAddress|varchar2(100)||否||||
|superMangerPhone|varchar2(100)||否||||

## 1.5. 借阅记录表

|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|lendId|integer(10)||否|||借阅图书时产生的唯一ID|
|lendTime|varchar(100)||否||在当前时间以后||
|readerId|integer(10)|外键|否|||与读者相关联|
|bookId|integer(10)|外键|否|||与借阅的图书相关联|
|ruleReturnTime|varchar(100)||否|||规定还书的时间,即不能一直借书，逾期将受到处罚|

## 1.6. 还书记录表
|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|returnBookId|integer(10)|主键|否|||还书时产生的唯一ID，便于查询是否还书|
|lendId|integer(10)|外键|否|||删除借书记录|
|readerId|integer(10)|外键|否|||删除读者已借记录|
|bookId|integer(10)|外键|否|||增加一条还书记录|


## 1.7. 预定图书表
|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|reserveId|integer(10)|主键|否|||预定图书时产生的唯一ID|
|readerId|integer(10)|外键|否|||增加预定读者的信息|
|bookId|integer(10)|外键|否|||增加一条预定图书信息|
|reserveTime|varchar2(100)||否|||预定图书的时间|


## 2.界面设计
## 2.1. 图书管理系统主界面
![](./图书管理系统.png '图书管理系统')

- 用例图参见：读者管理设计用例
- 类图参见：借书类，读者类，管理员类
- 顺序图参见：借书顺序图
- API接口如下：
###  1. 借阅图书

- 功能：读者在网络平台借阅图书
- 请求地址： http://127.0.0.1:8080/test5/api/mangerSystem/lend.html?bookId=
- 请求方法：POST
- 请求参数：bookId(Integer)

|参数名称|必填|说明|
|:-------:|:-------------: | :----------:|
|bookId|是|默认会提交图书ID |
|method|是|固定为 “POST”。|

- 返回实例：
```
{
    "code": 200,
    "data": {
            "bookId": "15656548",
            "name": "《简爱》",
            "submit":"提交"
     },
    "returnmsg": "借阅成功"
}
```
- 返回参数说明：
    
|参数名称|说明|
|:-------:|:-------------: |
|returnmsg|响应结果|
|data|借阅的图书信息|
|code|状态码|
- 说明：若读者在网上借阅后，则必须去图书馆领取借阅的图书

###  2. 增加图书

- 功能：管理员对图书的增加
- 请求地址： http://127.0.0.1:8080/test5/api/mangerSystem/addbook.html?bookId=
- 请求方法：POST
- 请求参数：bookId(Integer)

|参数名称|必填|说明|
|:-------:|:-------------: | :----------:|
|bookId|是|增加一条图书信息 |
|method|是|固定为 “POST”。|

- 返回实例：
```
{
    "code": 200,
    "data": {
            "bookId": "64543453",
            "ISBN":"123-658-7895-452136",
            "publisher":"四川出版社",
            "bookname": "《哈姆雷特》",
            "totalstock":0,
            "author":"威廉·莎士比亚",
            "summary":"丹麦王子哈姆雷特在德国威登堡大学就读时突然接到父亲的死讯，回国奔丧时接连遇到了叔父克劳狄斯即位和叔父与母亲乔特鲁德在父亲葬礼后一个月匆忙结婚的一连串事变，这使哈姆雷特充满了疑惑和不满",
            "submit":"提交"
     },
    "returnmsg": "增加成功"
}
```
- 返回参数说明：
    
|参数名称|说明|
|:-------:|:-------------: |
|returnmsg|响应的成功结果|
|totalstock|库存的信息|
|code|状态码|
|summary|图书的简要描述|
|bookId|图书的唯一ID|


###  3. 修改图书

- 功能：管理员修改图书的相关信息
- 请求地址： http://127.0.0.1:8080/test5/api/mangerSystem/update.html?bookId=
- 请求方法：POST
- 请求参数：bookId(Integer)

|参数名称|必填|说明|
|:-------:|:-------------: | :----------:|
|bookId|是|默认会提交图书ID |
|method|是|固定为 “POST”。|

- 返回实例：
```
{
    "code": 200,
    "data": {
            "bookId": "64543453",
            "ISBN":"123-658-7895-452136",
            "publisher":"北京出版社",
            "bookname": "《哈姆雷特》",
            "totalstock":100,
            "author":"威廉·莎士比亚",
            "summary":"丹麦王子哈姆雷特在德国威登堡大学就读时突然接到父亲的死讯，回国奔丧时接连遇到了叔父克劳狄斯即位和叔父与母亲乔特鲁德在父亲葬礼后一个月匆忙结婚的一连串事变，这使哈姆雷特充满了疑惑和不满",
            "submit":"提交"
     },
    "returnmsg": "修改成功"
}
```
- 返回参数说明：
    
|参数名称|说明|
|:-------:|:-------------: |
|returnmsg|响应结果|
|data|返回对图书修改后的信息|
|code|状态码|