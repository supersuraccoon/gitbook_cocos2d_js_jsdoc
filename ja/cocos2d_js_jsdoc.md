# Cocos2d-JS jsdoc

## 目標

`jsdoc` を用いて `cocos2d-js` プロジェクトに綺麗なオンラインドキュメントを自動作成する解決方法を見つける。


## 関連技術

- `javascript`
- `node.js`
- `python`
- `html`
- `css`


## jsdoc && cocos2d-js コメント仕様 

`jsdoc` [インストール](https://github.com/jsdoc3/jsdoc/)
`jsdoc` [ユーザーガイド](http://usejsdoc.org/)


### `cocos2d-js` Extended カスタムクラス

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

### カスタムクラス インスタンスメソッド

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

### カスタムクラス 静的メソッド

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

### 名前空間

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

### 名前空間 && グローバル変数

```javascript
/**
 * Global Custom Tag
 * @constant
 * @type Number
 */
cc.CUSTOM_TAG = 99999;
```

### 名前空間 && 静的メソッド

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

### Function クラス

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

### Function クラス シングルトン

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

### コールバック関数

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


## jsdoc ドキュメント

### 自動作成
`conf.json` :
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

次のコマンドより簡単にドキュメントを作成できます:
```shell
root$ jsdoc -c ./conf.json -d ./docs
```

作成したドキュメントは`./docs`にあります。`index.html`を開くと:

![jsdoc_default_template_1](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_default_template_1.png)

![jsdoc_default_template_2](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_default_template_2.png)

### jsdoc テンプレート
デフォルトで作成したドキュメントはあまり綺麗ではないのでここはテンプレートを使って綺麗なドキュメントを作成しましょう。

まずは好きなテンプレートをダウンロード＆＆解凍して、この前コマンドの変数として指定します:
```shell
root$ jsdoc -c ./conf.json -d ./docs -t ./template/docdash-master
```

これで先のドキュメントも綺麗になりました:

![jsdoc_custom_template_1](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_1.png)

![jsdoc_custom_template_2](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_2.png)


### テンプレートのカステム
使用したテンプレートも簡単に思い通りにカステムすることができます。
例えばこのリンク文字の色が見づらいと思います :

![jsdoc_custom_template_css_1](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_css_1.png)

ここで `Chrome Developer Tools -- Elements -- Inspect` を用いてこのリンクの文字の`css`を見つけ出して:

![jsdoc_custom_template_css_2](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_css_2.png)

そして好きな色をまず試して探します:

![jsdoc_custom_template_css_3](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_css_3.png)

最後は決めた色をテンプレートの`css`に対応すればオッケー:
```css
.type-signature > a {
  color: #D6FDC4;
}
```

ドキュメントをコマンドでもう一度咲くせし、これで完成です:

![jsdoc_custom_template_css_4](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_custom_template_css_4.png)


## jsdoc markdown

[jsdoc-to-markdown](https://github.com/jsdoc2md/jsdoc-to-markdown) を使って先ほどのオンラインドキュメントを`markdown` として出力することも可能です:

```shell
jsdoc2md ./SampleProject/src/MainMenuScene.js > api.md
```

![jsdoc_markdown](http://o7ga66t11.bkt.clouddn.com/cocos2d-js-jsdoc/jsdoc_markdown.png)




