
[xcoder.hexccc.com](http://xcoder.hexccc.com)

[obaa.js源码地址](https://github.com/Tencent/omi/tree/master/packages/obaa)

这个函数库只用很少的代码就实现了监听对象属性变化的功能

`obaa.methods` 只在这里使用了一次

    obaa.methods.forEach(function(item) {
        ...
    }
    
    
obaa.triggerStr 都是数组的方法
    
    obaa.triggerStr = [
    'concat',
    'copyWithin',
    'fill',
    'pop',
    'push',
    'reverse',
    'shift',
    'sort',
    'splice',
    'unshift',
    'size'
    ].join(',')

`obaa.triggerStr` 只在这里使用了一次

    if (new RegExp('\\b' + item + '\\b').test(obaa.triggerStr)) {
        ...
    }
    

$observer

eventPropArr

propertyChangedHandler

$observeProps.$observerPath

初始一般都是"#"

## Object.defineProperty



## 三个方法
    
### onPropertyChanged

当对象变化的时候，
    
### mock
    
遍历obaa.methods
    
### watch



## 辅助方法

    obaa.isArray // 判断是否数组
    obaa.isString // 判断是否字符串
    obaa.isInArray // 判断某个元素是否在数组中
    obaa.isFunction // 判断是否函数
    
    
## obaa._getRootName

obaa._getRootName 查找对象上的属性

## obaa.set 和 obaa.add

如果对象本身没有某个属性，那么要使用 `obaa.set` 这个方法

    //if obj.c is undefined
    obaa.set(obj, 'c', 3)
    obj.c = 4 //trigger observe callback
    
    //if obj.c is undefined
    obj.c = 3
    obj.c = 4 //don't trigger observe callback
    
obaa.set 实现如下，exec参数的作用暂时还没看懂

    obaa.set = function(obj, prop, value, exec) {
        if (!exec) {
          obj[prop] = value
        }
        var $observer = obj.$observer
        $observer.watch(obj, prop)
        if (exec) {
          obj[prop] = value
        }
    }

`obaa.add` 方法其实跟 `obaa.set` 类似，只是更加简单

给Array对象增加方法

    Array.prototype.size = function(length) {
        this.length = length
    }
    
这样修改arr的length属性就不会触发回调
    
    arr.size(2) //trigger observe callback
    arr.length = 2 //don't trigger observe callback

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
      
      
    
这段代码给数组对象增加N个以pure开头的方法，这些新的方法不回触发回调
      
    target[
    'pure' + item.substring(0, 1).toUpperCase() + item.substring(1)
      ] = function() {
      return Array.prototype[item].apply(
        this,
        Array.prototype.slice.call(arguments)
      )
    }
    
例如对应push方法，增加了一个purePush 方法 

    arr.purePush(111) // 这样子不会触发回调
    
    
## 参考资料

[https://www.cnblogs.com/chenguangliang/p/5856701.html](https://www.cnblogs.com/chenguangliang/p/5856701.html)


<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="http://xcoder.hexccc.com/cc.png"></a>
    
This work is licensed under a [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License](http://creativecommons.org/licenses/by-nc-nd/4.0/).