# CMD֮seajs��������

##1.���� config.js

```javascript
seajs.config({

    //����·���������Ŀ¼����
	paths:{
		base:base+'js',
		inc:base+'inc'
	},
	//���ñ���
    alias:{
		jquery:'base/plugin/jquery-1.11.2-min',
		...
	},
	//��ǰ���ز���ʼ���ض�ģ�飬�������������������ǰ���غ�ES5,jsonģ�顣
    //ע��:'2.3.0û���������'
    //�����Ҫ�ɰ�֮ǰ�汾�еĴ��븴�ƹ���  ������ʾ
	preload:[
		'jquery',
		this.JSON ? '' : 'json',
		Function.prototype.bind ? '' : 'es5'
	],
    //����
    debug:true,  //false
    //�������ȴ��ű����ص��ʱ��
    timeout:20000,
    //��������
    //vars ���õ���ģ���ʶ�еı���ֵ����ģ���ʶ����{key}����ʾ����
    vars:{
        product:'seajs'
    },
    //seajs����·��
    base:'',
    //ӳ������ ·��ת�� ���ߵ���
    map:[],
    //����
    charset:'utf-8'

})
```

//��2.3.0��������δ��� ����preload����
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
2.cmd seajs����(�������)
  ...