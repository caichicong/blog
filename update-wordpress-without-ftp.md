
[xcoder.hexccc.com](http://xcoder.hexccc.com)

## 不使用ftp升级wordpress

wordpress经常提示升级插件和主题，但是一般linux vps服务器往往没有安装ftp服务（vsftpd的配置比较复杂）。其实适当配置之后，可以不使用ftp升级wordpress

以下方法适用于Linux平台

首先建立临时文件夹

    mkdir wp-content/tmp
    chmod 777 wp-content/tmp
    
然后修改wp-config.php文件

    define('WP_TEMP_DIR', ABSPATH.'wp-content/tmp');
    define("FS_METHOD", "direct");
    define("FS_CHMOD_DIR", 0777);
    define("FS_CHMOD_FILE", 0777);
    
命令行执行以下命令

    chown www-data:www-data  -R * 
    chmod 777 *.php 
    chmod 777 wp-includes/*
    chmod 777 wp-admin/*
    chmod 777 wp-content/*
    
    
升级之后，文件的权限修改成644， 目录的权限修改成755。ubuntu对应你登录服务器的用户名，www-data对应网站访客使用的身份。请根据实际情况修改。

    find . -type d -exec sudo chmod 755 {} \;  
    find . -type f -exec sudo chmod 644 {} \;  
    sudo chown -R ubuntu:ubuntu .
    sudo chown -R www-data:www-data wp-content
    
    
<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="http://xcoder.hexccc.com/cc.png"></a>
    
This work is licensed under a [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License](http://creativecommons.org/licenses/by-nc-nd/4.0/).

