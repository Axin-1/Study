#第八章 BOM浏览器对象模型
###8.1 BOM概述
#####8.1.1 概述
浏览器对象模型，简称BOM.BOM提供了独立于内容而是与浏览器窗口进行交互的对象.BOM的核心是window对象.与ECMScript不同的是,BOM针对的是浏览器,鉴于市面上的浏览器多种多样,因此会影响BOM的兼容性.

#####8.1.2 主流浏览器
浏览器以为它的多厂商,导致兼容问题是不容忽视的.主流浏览器中各个版本的兼容也不尽相同.因此,在BOM中运用时可能会出现结果不同或者毫无结果的情况.

###8.2 window对象
#####8.2.1 window对象概念
window对象是BOM的核心对象,它除了可以使用全局对象的属性和方法之外,还可以执行浏览器的一些方法.

#####8.2.2 全局作用域
在全局作用域下创建的变量和函数都会成为window的属性和方法的.

     <script>
        var a = 10;
        console.log(window.a);

        function b(){
            return"你好";
        }
        console.log(window.b());
        
        //在全局下window可省略
    </script>

#####8.2.3 窗口大小    
(1) 视图的大小
可见内容视口(视图)相当于document.body的宽度和高度

    <script>
        //可见内容视口(视图)相当于document.body的宽度和高度
        var w = document.body.clientWidth;    
        var h = document.body.clientHeight;
        
        console.log(wh+','+hh);//1384,400

    </script>

(2)视口大小
浏览器的视口大小是包含左侧和下方的滚动条的.

    //浏览器展现区域的宽高,包含滚动条所占区域
        var wh = window.innerWidth;    
        var hh = window.innerHeight;
        
        console.log(wh+','+hh);//1400,978

(3)浏览器的大小
整个浏览器在显示屏上所占有的宽度和高度，包含浏览器的所有部分

    //整个浏览器在显示屏上所占有的宽度和高度，包含浏览器的所有部分
        var ow = window.outerWidth;
        var oh = window.outerHeight;

        console.log(ow+','+oh);

#####8.2.4 窗口位置
浏览器左边界和上边界到操作系统桌面左上角的水平和垂直距离.    

#####8.2.5 open
window.open('需要打开的地址','窗口打开的方式');这是最简单的open参数，还可以增加其他内容。这是open打开的页面基本都可以用close关闭，但open和close有兼容性问题

        document.getElementById('a').onclick=function(){
            //_blank 新窗口打开(默认)
            window.open('视口大小.html');
            //_srlf 当前窗口打开
            window.open('视口大小.html','_self');
        }

         //////////////////////关闭
         document.getElementById('b').onclick=function(){
             window.close('视口大小.html');
         }

#####8.2.6 弹出框

        alert('提示弹出框');//字符串
        confirm('选择弹出框');//返回值是true/false
        prompt('输入弹出框'); //返回值是字符串内容

#####8.2.7 超时调用(一次性定时器)    
setTimeout(回调函数,时间)也叫一次性定时器，创建这个定时器之后会在一定时间中调用函数，执行函数中的脚本。

        // setTimeout(回调函数,时间};    
        setTimeout(function(){
            alert('欢迎光临');
        },2000);



        //递归调用
        function times(){
            //执行代码
            console.log('执行的代码段');
            setTimeout(function(){
                times();
            }, 1000);
        }
        //调用
        times();

#####8.2.8 间歇调用(循环定时器)
setInterval(回调函数，时间)也叫循环定时器，创建这个定时器之后会每隔一段时间触发，触发时间就是参数中的时间，当时间低于10毫秒时，默认为10毫秒。

    setInerval(function(){},1000);

注意：循环定时器存在bug，执行时间大于等待时间，将会出现任务堆叠，一般情况下，使用setTimeout代替

###8.3 location对象
#####8.3.1 location对象的概念
window的location对象获取当前页面的地址(URL)，并把浏览器重新定向到新的页面。在编号时可以不用加window前缀。

#####8.3.2 查看location对象的常用的属性
    href 返回当前完整的URL地址
    host 返回的是服务器名称和端口号
    port 返回端口号
    pathname 返回的是目录和文件名
    searth 返回的是参数，也就是？后面的内容
    protocol 返回使用页面的协议，如http/https


--------------------

###8.4 navigator对象
#####8.4.1 概念
window 的navigator对象包含关于浏览器的信息，在编辑的时候不能使用window这个前缀，可直接使用navigator，该对象代表浏览器本身的名称，版本，系统等信息。但存在兼容问题，请慎用。

#####8.4.2 属性介绍

    console.log(navigator);

navigator.appName :浏览器名称
navigator.appVersion :浏览器的版本
navigator.userAgent :判断浏览器

鉴于兼容问题,在固定浏览器的特定版本进行自主寻找.

#####8.4.3 判断浏览器类型

        if(navigator.userAgent.indexOf('MSIE')!=-1){
            console.log('IE浏览器');
        }else {
            console.log('非IE浏览器');
        }
 
###8.5 screen对象
#####8.5.1 概念
screen对象表示一个屏幕的窗口，他会随着浏览器的不同，窗口大小的位置不同返回不同的值，前提是返回的是当前打开窗口的内容。


#####8.5.2 属性

    console.log(screen);


###8.6 history对象
history对象保存着从窗口被打开的历史记录，每个浏览器窗口，标签页，框架都有自己的history对象。为了保护用户隐私，对访问该对象作出了一部分限制。   

    console.log(history);

#####8.6.2 常用方法
history.go(n) 整数 0代表刷新,整数代表向前跳n步,负数代表向后跳n步.
history.back(n) 代表向后跳n步.   





##练习
需求1：
1.创建一个登陆页面，含用户名和密码
2.登陆后验证密码必须为123，否则弹出登陆失败
3，登陆后跳转到另一个页面，页面上大文字提示‘欢迎你，xxx’ xxx的内容为用户名


需求2:
1.实现不同终端的跳转
2.页面宽度低于414px的时候默认为手机端
3.如果判定是手机端就打开京东的移动端页面
4.如果判定是pc端,就打开京东的pc端界面
5.移动端路径:https://m.jd.com
pc端路径 https://www.jd.com