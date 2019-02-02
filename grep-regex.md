## grep命令中使用正则表达式

grep命令在Linux下很常用。但是grep的正则表达式跟我们平常在javascript和php下使用的正则表达式有很多不同的地方。

grep的基本用法如下，其中pattern对应正则表达式：

    grep options [pattern] filename

有用的选项（options）

    grep -i 'pattern' test.txt // 忽略大小写
    
    grep -v 'pattern' test.txt // 不匹配含有该pattern的行
    
    // 显示匹配行的前后n行，具体可参看手册
    
    grep -A 'pattern' test.txt
    
    grep -B 'pattern' test.txt
    
    grep -C 'pattern' test.txt
    

grep可以使用POSIX字符组

    grep '[[:alnum:]]' test.txt // 匹配数字和字符
    
    grep '[[:alpha:]]' test.txt // 匹配字符
    
    grep '[[:digit:]]' test.txt // 匹配数字
    
    grep '[[:space:]]' test.txt // 匹配空白字符
    
    
匹配一行的开头和结尾
 
    grep '^start' test.txt
    
    grep 'end$' test.txt
    
匹配单词

    grep '\<word\>' test.txt
    
量词匹配

    // *不需要转义
    grep 'n*' test.txt
    
    // +要转义
    grep 'n+' test.txt  ==>  grep 'n\+' test.txt
    
    // ?要转义
    grep 'bn?' test.txt  ==>  grep 'bn\?' test.txt
    
    // {}要转义
    grep 'bn{1,4}' test.txt  ==>  grep 'bn\{1,4\}' test.txt
    
多选匹配

    // {}和竖线都要要转义
    grep '(test1|test2)' test.txt ==> grep '\(test1\|test2\)' test.txt
    
    
<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png"></a>
    
This work is licensed under a [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License](http://creativecommons.org/licenses/by-nc-nd/4.0/).