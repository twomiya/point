###移动端页面开发要点
**一、meta标签相关知识**
#####1、移动端页面设置视口宽度等于设备宽度，并禁止缩放。
```
<meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no" />

```

#####2、移动端页面设置视口宽度等于定宽（如640px），并禁止缩放，常用于微信浏览器页面。

```
<meta name="viewport" content="width=640,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no" />

```

#####3、禁止将页面中的数字识别为电话号码

```
<meta name="format-detection" content="telephone=no" />

```

#####4、忽略Android平台中对邮箱地址的识别

```
<meta name="format-detection" content="email=no" />

```
#####5、当网站添加到主屏幕快速启动方式，可隐藏地址栏，仅针对ios的safari

```
<meta name="apple-mobile-web-app-capable" content="yes" />
<!-- ios7.0版本以后，safari上已看不到效果 -->
```

#####6、将网站添加到主屏幕快速启动方式，仅针对ios的safari顶端状态条的样式

```
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
<!-- 可选default、black、black-translucent -->
```

*viewport模版*

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
<meta content="yes" name="apple-mobile-web-app-capable">
<meta content="black" name="apple-mobile-web-app-status-bar-style">
<meta content="telephone=no" name="format-detection">
<meta content="email=no" name="format-detection">
<title>title</title>
<link rel="stylesheet" href="index.css">
</head>

<body>
    content...
</body>

</html>
```

**二、CSS样式技巧**

#####1、禁止ios和android用户选中文字

```
.css{-webkit-user-select:none}
```

#####2、禁止ios长按时触发系统的菜单，禁止ios&android长按时下载图片

```
.css{-webkit-touch-callout: none}
```

#####3、webkit去除表单元素的默认样式

```
.css{-webkit-appearance:none;}
```

#####4、修改webkit表单输入框placeholder的样式

```
input::-webkit-input-placeholder{color:#AAAAAA;}
input:focus::-webkit-input-placeholder{color:#EEEEEE;}
```

#####5、去除android a/button/input标签被点击时产生的边框 & 去除ios a标签被点击时产生的半透明灰色背景

```
a,button,input{-webkit-tap-highlight-color:rgba(255,0,0,0);}
```

#####6、ios使用-webkit-text-size-adjust禁止调整字体大小

```
body{-webkit-text-size-adjust: 100%!important;}
```

#####7、android 上去掉语音输入按钮

```
input::-webkit-input-speech-button {display: none}
```

#####8、移动端定义字体，移动端没有微软雅黑字体

```
/* 移动端定义字体的代码 */
body{font-family:Helvetica;}
```

#####9、禁用Webkit内核浏览器的文字大小调整功能。'

```
-webkit-text-size-adjust: none;
```

#####10、去掉 input[type=search] 搜索框默认的叉号

```
input[type="search"]{
    -webkit-appearance:none;
}
input::-webkit-search-cancel-button {
    display: none;
}
```


**三、其他技巧**

#####1、手机拍照和上传图片

```
<!-- 选择照片 -->
<input type=file accept="image/*">
<!-- 选择视频 -->
<input type=file accept="video/*">
```

#####2、取消input在ios下，输入的时候英文首字母的默认大写

```
<input autocapitalize="off" autocorrect="off" />
```

#####3、打电话和发短信

```
<a href="tel:0755-10086">打电话给:0755-10086</a>
<a href="sms:10086">发短信给: 10086</a>
```


**四、CSS reset**

```
/* hcysun  */
@charset "utf-8";
/* reset */
html{
    -webkit-text-size-adjust:none;
    -webkit-user-select:none;
    -webkit-touch-callout: none
    font-family: Helvetica;
}
body{font-size:12px;}
body,h1,h2,h3,h4,h5,h6,p,dl,dd,ul,ol,pre,form,input,textarea,th,td,select{margin:0; padding:0; font-weight: normal;text-indent: 0;}
a,button,input,textarea,select{ background: none; -webkit-tap-highlight-color:rgba(255,0,0,0); outline:none; -webkit-appearance:none;}
em{font-style:normal}
li{list-style:none}
a{text-decoration:none;}
img{border:none; vertical-align:top;}
table{border-collapse:collapse;}
textarea{ resize:none; overflow:auto;}
/* end reset */
```


**五、常用公用CSS style**

```
/* public */

/* 清除浮动 */
.clear { zoom:1; }
.clear:after { content:''; display:block; clear:both; }

/* 定义盒模型为怪异和模型（宽高不受边框影响） */
.boxSiz{
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    -ms-box-sizing: border-box;
    -o-box-sizing: border-box;
    box-sizing: border-box;
}

/* 强制换行 */
.toWrap{
    word-break: break-all;       /* 只对英文起作用，以字母作为换行依据。 */
    word-wrap: break-word;       /* 只对英文起作用，以单词作为换行依据。*/
    white-space: pre-wrap;     /* 只对中文起作用，强制换行。*/
}

/* 禁止换行 */
.noWrap{
    white-space:nowrap;
}

/* 禁止换行,超出省略号 */
.noWrapEllipsis{
     white-space:nowrap; overflow:hidden; text-overflow:ellipsis;
}

/* 多行显示省略号，less写法，@line是行数 */
.ellipsisLn(@line) {
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: @line;
}

/* 1px 边框解决方案，示例中设置上边框，可以调整 top、right、bottom、left 的值分别设置上下左右边框 */
#box2:after{
    content: " ";
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    height: 1px;
    border-top: 1px solid #000;
    color: #C7C7C7;
    transform-origin: 0 0;
    transform: scaleY(0.5);
}

/* 文字两端对齐 */
.text-justify{
    text-align:justify; 
    text-justify:inter-ideograph;
}

/* 定义盒模型为 flex布局兼容写法并让内容水平垂直居中 */
.flex-center{
    display: -webkit-box;
    display: -moz-box;
    display: -ms-flexbox;
    display: -o-box;
    display: box;

    -webkit-box-pack: center;
    -moz-box-pack: center;
    -ms-flex-pack: center;
    -o-box-pack: center;
    box-pack: center;

    -webkit-box-align: center;
    -moz-box-align: center;
    -ms-flex-align: center;
    -o-box-align: center;
    box-align: center;
}

/* public end */
```

**六、flex布局**

#####1、定义弹性盒模型兼容写法

```
/*
    box
    inline-box
*/
display: -webkit-box;
display: -moz-box;
display: -ms-flexbox;
display: -o-box;
display: box;
```

#####2、box-orient 定义盒模型内伸缩项目的布局方向

```
/**
 * vertical column    垂直
 * horizontal row    水平 默认值
 */
-webkit-box-orient: horizontal;
-moz-box-orient: horizontal;
-ms-flex-direction: row;
-o-box-orient: horizontal;
box-orient: horizontal;
```

#####3、box-direction 定义盒模型内伸缩项目的正序(normal默认值)、倒叙(reverse)

```
/* Firefox */
display:-moz-box;
-moz-box-direction:reverse;
/* Safari、Opera 以及 Chrome */
display:-webkit-box;
-webkit-box-direction:reverse;
```

#####4、box-pack 对盒子水平富裕空间的管理

```
/*
    start
    end
    center
    justify
*/
-webkit-box-pack: center;
-moz-box-pack: center;
-ms-flex-pack: center;
-o-box-pack: center;
box-pack: center;
```

#####5、box-pack 对盒子垂直方向富裕空间的管理

```
/*
    start
    end
    center
*/
/* box-align */
-webkit-box-align: center;
-moz-box-align: center;
-ms-flex-align: center;
-o-box-align: center;
box-align: center;
```

#####6、定义伸缩项目的具体位置

```
/*-moz-box-ordinal-group:1;*/ /* Firefox */
/*-webkit-box-ordinal-group:1;*/ /* Safari 和 Chrome */
.box div:nth-of-type(1){-webkit-box-ordinal-group:1;}
.box div:nth-of-type(2){-webkit-box-ordinal-group:2;}
.box div:nth-of-type(3){-webkit-box-ordinal-group:3;}
.box div:nth-of-type(4){-webkit-box-ordinal-group:4;}
.box div:nth-of-type(5){-webkit-box-ordinal-group:5;}
```

#######7、定义伸缩项目占空间的份数

```
-moz-box-flex:2.0; /* Firefox */
-webkit-box-flex:2.0; /* Safari 和 Chrome */

.box div:nth-of-type(1){-webkit-box-flex:1;}
.box div:nth-of-type(2){-webkit-box-flex:2;}
.box div:nth-of-type(3){-webkit-box-flex:3;}
.box div:nth-of-type(4){-webkit-box-flex:4;}
.box div:nth-of-type(5){-webkit-box-flex:5;}
```

