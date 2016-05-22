# Cocos2d-JS jsdoc

## Target

Write well formatted comment && Generate a pretty online document for `cocos2d-js` game project.


## Related Skills

- `javascript`
- `node.js`
- `python`
- `html`
- `css`


## jsdoc && cocos2d-js Comment Specification 

`jsdoc` [Installation](https://github.com/jsdoc3/jsdoc/)
`jsdoc` [User Guide](http://usejsdoc.org/)


### `cocos2d-js` Extended Custom Class

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

### Custom Class Instance Method

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

### Custom Class Static Method

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

### Namespace

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

### Namespace && Global Variable

```javascript
/**
 * Global Custom Tag
 * @constant
 * @type Number
 */
cc.CUSTOM_TAG = 99999;
```

### Namespace && Static Method

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

### Function Class

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

### Function Class Singleton

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

### Callback Function

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


## jsdoc Online Document

### Generate
To generate a online doc is pretty simple. First we need to a `conf.json` :
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

Then we can generate the doc using the following command:
```shell
root$ jsdoc -c ./conf.json -d ./docs
```

The generated doc is under `./docs` and we can access it by opening `index.html`:

![jsdoc_default_template_1](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_default_template_1.png)

![jsdoc_default_template_2](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_default_template_2.png)

### jsdoc Template
The default generated doc dose look that good but we can use some beautiful template && customize to make it looks good.

Download any template you like, unzip it and then use it like this:
```shell
root$ jsdoc -c ./conf.json -d ./docs -t ./template/docdash-master
```

Now here comes our pretty pretty look doc:

![jsdoc_custom_template_1](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_1.png)

![jsdoc_custom_template_2](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_2.png)


### Customize Template
To customize the template is also a piece of cake. For example the color of the link text here is not good :

![jsdoc_custom_template_css_1](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_css_1.png)

We can use the `Chrome Developer Tools -- Elements -- Inspect` to quick locate the elemnet we want and check the style:

![jsdoc_custom_template_css_2](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_css_2.png)

and we can change the property on the fly:

![jsdoc_custom_template_css_3](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_css_3.png)

and finally we just need to apply the changes to the corresponding  `css` file:
```css
.type-signature > a {
  color: #D6FDC4;
}
```

and regenerate the doc and that's all:

![jsdoc_custom_template_css_4](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_css_4.png)


## jsdoc markdown

[jsdoc-to-markdown](https://github.com/jsdoc2md/jsdoc-to-markdown) can generate formatted `markdown` doc which is another cool way to share the doc:

```shell
jsdoc2md ./SampleProject/src/MainMenuScene.js > api.md
```

![jsdoc_markdown](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_markdown.png)




