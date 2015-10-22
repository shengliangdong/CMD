# CMD之seajs技术分享

##1.配置 config.js

```javascript
seajs.config({

    //设置路径，方便跨目录调用
	paths:{
		base:base+'js',
		inc:base+'inc'
	},
	//设置别名
    alias:{
		jquery:'base/plugin/jquery-1.11.2-min',
		...
	},
	//提前加载并初始化特定模块，以下是在老浏览器中提前加载好ES5,json模块。
    //注意:'2.3.0没有这个功能'
    //如果需要可把之前版本中的代码复制过来  如下所示
	preload:[
		'jquery',
		this.JSON ? '' : 'json',
		Function.prototype.bind ? '' : 'es5'
	],
    //调试
    debug:true,  //false
    //加载器等待脚本加载的最长时间
    timeout:20000,
    //变量配置
    //vars 配置的是模块标识中的变量值，在模块标识中用{key}来表示变量
    vars:{
        product:'seajs'
    },
    //seajs基础路径
    base:'',
    //映射配置 路径转换 在线调试
    map:[],
    //编码
    charset:'utf-8'

})
```

//在2.3.0中增加这段代码 激活preload功能
```javascript
!function() {
    var a = seajs.data, b = document;
    seajs.Module.preload = function(b) {
        var c = a.preload, d = c.length;
        d ? seajs.Module.use(c, function() {
            c.splice(0, d), seajs.Module.preload(b)
        }, a.cwd + "_preload_" + a.cid()) : b()
    }, seajs.use = function(b, c) {
        return seajs.Module.preload(function() {
            seajs.Module.use(b, c, a.cwd + "_use_" + a.cid())
        }), seajs
    }, a.preload = function() {
        var a = [], c = location.search.replace(/(seajs-\w+)(&|$)/g, "$1=1$2");
        return c += " " + b.cookie, c.replace(/(seajs-\w+)=1/g, function(b, c) {
            a.push(c)
        }), a
    }(), define("", [], {})
}();
```
2.cmd seajs构建(后面奉上)
  ...