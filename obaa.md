

[obaa.js源码地址](https://github.com/Tencent/omi/tree/master/packages/obaa)

这个函数库只用很少的代码就实现了监听对象属性变化的功能

`obaa.methods` 只在这里使用了一次

    obaa.methods.forEach(function(item) {
        ...
    }

`obaa.triggerStr` 只在这里使用了一次

    if (new RegExp('\\b' + item + '\\b').test(obaa.triggerStr)) {
        ...
    }
    

三个方法
    
    onPropertyChanged
    
    mock
    
    watch

## 辅助方法

    obaa.isArray // 判断是否数组
    obaa.isString // 判断是否字符串
    obaa.isInArray // 判断某个元素是否在数组中
    obaa.isFunction // 判断是否函数
    
    
obaa._getRootName

obaa.add

obaa.set


给Array对象增加方法

    Array.prototype.size = function(length) {
        this.length = length
    }

这段代码使得obaa可以成为在ommonJS规范和AMD规范下的模块。 

如果不需要模块化的功能，则直接把obaa对象作为windows对象的一个属性（即全局变量）。

      if (
        typeof module != 'undefined' &&
        module.exports) {
        module.exports = obaa
      } else if (typeof define === 'function' && define.amd) {
        define(obaa)
      } else {
        win.obaa = obaa
      }
