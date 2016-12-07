在mongoose中默认的collection(表)名都是复数(结尾+s),如果需要使用单数形式的数据表名,在创建Schema实例的时候加入第二个参数
```
var mongoose = require("mongoose");
var aSchema = new mongoose.Schema({
	fields:Schema.Type
},{
	collection: "collection_name"
});
```
也可以把表名加到uncountables就可以了