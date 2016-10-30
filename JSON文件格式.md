# JSON数据格式

## JSON 对象
JSON对象在**花括号**中书写  
对象可以包含多个**键/值**对  
```json
{
  "name" : "pp",
  "age" : "10"
}
```

## JSON 数组
JSON数组在**方括号**中书写  
数组可包含多个对象  
```json
{
  "students" : [
    {
      "name" : "pp",
      "age" : "10"
    },
    {
      "name" : "ppp",
      "age" : "12"
    },
    {
      "name" : "pppp",
      "age" : "14"
    }
  ]
}
```

## JSON 多维数组
若JSON数组中对象的**值**为一个**对象**  
则这个数组就是多维数组  
```json
{
  "name" : {
    "firstname" : "p",
    "lastname" : "pp"
  },
  "age" : "10"
}
```
