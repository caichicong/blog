

[obaa.js源码地址](https://github.com/Tencent/omi/tree/master/packages/obaa)

用很少的代码就实现了监听对象属性变化的功能

`obaa.methods`

`obaa.triggerStr`

## 辅助方法

    obaa.isArray // 判断是否数组
    obaa.isString // 判断是否字符串
    obaa.isFunction // 判断是否函数
    
    
obaa._getRootName

obaa.add

obaa.set

可以用在CMD规范和AMD规范下的模块。 如果不需要模块化的功能，则直接把obaa对象作为windows对象的一个属性

      if (
        typeof module != 'undefined' &&
        module.exports) {
        module.exports = obaa
      } else if (typeof define === 'function' && define.amd) {
        define(obaa)
      } else {
        win.obaa = obaa
      }
