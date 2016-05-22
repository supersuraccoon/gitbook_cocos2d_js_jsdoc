# Cocos2d-JS jsdoc

## 目标

使用 `jsdoc` 为 `cocos2d-js` 游戏源码添加文档注释，生成在线的 `doc` ，方便查阅。


## 涉及技术

- `javascript`
- `node.js`
- `python`
- `html`
- `css`


## jsdoc && cocos2d-js 注释规范

`jsdoc` 的[安装](https://github.com/jsdoc3/jsdoc/)
`jsdoc` 的[文档](http://usejsdoc.org/)


### 继承 `cocos2d-js` 自定义类

```javascript
/**
 * @class
 * @extends cc.Node
 * @property {Number}   a   - property a of cc.CustomNode
 * @property {Number}   b   - property b of cc.CustomNode
 * @property {Number}   c   - property c of cc.CustomNode
 * @classdesc cc.CustomNode
 */
cc.CustomNode = cc.Node.extend(/** @lends cc.CustomNode# */{
    // ......
});
```

### 自定义类的实例方法

```javascript
cc.CustomNode = cc.Node.extend(/** @lends cc.CustomNode# */{
    /**
     * cocos constructor
     * @function
     */
    ctor:function() {
        cc.Node.prototype.ctor.call(this);
    },
    /**
     * cc.CustomNode instance Method A
     * @function
     */
    funcA:function() {},
    /**
     * cc.CustomNode instance Method B
     * @function
     */
    funcB:function() {}
});
```

### 自定义类的静态方法

```javascript
cc.CustomNode = cc.Node.extend(/** @lends cc.CustomNode# */{
    // ......
});
/** 
 * cc.CustomNode Class Static Method
 * @return {cc.CustomNode}
 * @example
 * // example
 * var node = cc.CustomNode.create();
 */
cc.CustomNode.create = function() {};
```

### 命名空间

```javascript
/**
 * cc Namespace.
 * @namespace
 */
var cc = cc || {};


/**
 * cc.NamespaceA Namespace.
 * @namespace
 */
cc.NamespaceA = cc.NamespaceA || {};


/**
 * cc.NamespaceB Namespace.
 * @namespace
 */
cc.NamespaceB = cc.NamespaceB || {};
```

### 全局常量

```javascript
/**
 * Global Custom Tag
 * @constant
 * @type Number
 */
cc.CUSTOM_TAG = 99999;
```

### 命名空间 && 静态函数

```javascript
/** 
 * SomeUtil -- A static util function.
 * @param {int} param1 - param1
 * @param {int} param2 - param2
 * @param {int} param3 - param3
 * @return {int}
 */
cc.NamespaceA.SomeUtil = function (param1, param2, param3) {
    return param1 + param2 + param3;
};
```

### `Function`模拟类

```javascript
/**
 * @class
 * @classdesc cc.NamespaceB.SomeManager
 */
cc.NamespaceB.SomeManager = function() {
    /** 
     * init method
     * @function
     * @param {string} tag - some tag
     * @see cc.NamespaceB.SomeManager#funcB
     */
    this.init = function(tag) {
    };
    /** 
     * funcA method
     * @function
     */
    this.funcA = function() {};
    /** 
     * funcB method
     * @function
     */
    this.funcB = function() {};
};
```

### `Function`模拟类单例模式

```javascript
cc.NamespaceB.SomeManager = function() {
    // ......
};
var _sharedSomeManager = null;
/** 
 * cc.NamespaceB.SomeManager singleton.
 * @return {cc.NamespaceB.SomeManager}
 * @example
 * // example
 * cc.NamespaceB.SomeManager.getInstance().funcA();
 */
cc.NamespaceB.SomeManager.getInstance = function() {
    if (_sharedSomeManager == null) {
        _sharedSomeManager = new cc.NamespaceB.SomeManager();
        _sharedSomeManager.init();
    }
    return _sharedSomeManager;
};
```

### 回调函数

```javascript
cc.NamespaceB.SomeManager = function() {
    // ......
    /** 
     * callBackFunc method
     * @function
     * @param {cc.NamespaceB.SomeManager~customCallback} callbackFunc - A callback function.
     */
    this.funcWithCallback = function(callbackFunc) {
        callbackFunc();
    }
    /**
     * This callback for funcWithCallback method.
     * @callback cc.NamespaceB.SomeManager~customCallback
     * @param {object} event - Event object.
     */
};
```


## jsdoc 在线文档

### 文档生成
生成文档十分简单，首先配置 `conf.json` :
```json
{
    "tags": {
    },
    "source": {
        "include": [
            "../SampleProject/src/MainMenuScene.js"
        ]
    },
    "plugins": ["plugins/markdown"],
    "templates": {
        "cleverLinks": false,
        "monospaceLinks": false
    }
}
```

运行命令就可以生成:
```shell
root$ jsdoc -c ./conf.json -d ./docs
```

生成后的文档在 `./docs` 中，打开 `index.html` 即可:

![jsdoc_default_template_1](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_default_template_1.png)

![jsdoc_default_template_2](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_default_template_2.png)

### 使用文档模板
默认生成的模板不太好看，可以使用漂亮一点的模板，甚至在其基础上修改。

下载的模板只需解压，在生成 `doc` 的时候指定使用的模板即可:
```shell
root$ jsdoc -c ./conf.json -d ./docs -t ./template/docdash-master
```

这样就会生成漂亮的在线文档了。

![jsdoc_custom_template_1](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_1.png)

![jsdoc_custom_template_2](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_2.png)


### 修改文档模板样式
修改模板样式是极其简单的，如这里的链接文字看不清楚:

![jsdoc_custom_template_css_1](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_css_1.png)

可以通过 `Chrome` 的调试工具，快速定位一下其样式:

![jsdoc_custom_template_css_2](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_css_2.png)

接着直接修改一下，选择喜欢的颜色后，记录下来:

![jsdoc_custom_template_css_3](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_css_3.png)

对应的在模板的 `jsdoc.css` 中对应一下即可:
```css
.type-signature > a {
  color: #D6FDC4;
}
```

然后重新生成一下文档即可:

![jsdoc_custom_template_css_4](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_css_4.png)


## jsdoc markdown

[jsdoc-to-markdown](https://github.com/jsdoc2md/jsdoc-to-markdown)可以生成格式化好的 `markdown` 格式文档，使用方法非常简单，可以参见其帮助文档。

```shell
jsdoc2md ./SampleProject/src/MainMenuScene.js > api.md
```

![jsdoc_markdown](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_markdown.png)




