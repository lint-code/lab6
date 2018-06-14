# Read ME

#### 一.实验名称

​	自定义WebView验证隐式Intent的使用

#### 二.实验要求与目的

​	“&nbsp;” 本实验通过自定义WebView加载URL来验证隐式Intent的使用 

​	“&nbsp;” 实验包含两个应用：

​		第一个应用：获取URL地址并启动隐式Intent的调用。

​		第二个应用：自定义WebView来加载URL

#### 三.实验步骤

##### 1.编写activity_main.xml文件

​	该布局文件为	RelativeLayout，包含一个EditText和一个Button

##### 2.编写webview.xml文件

```
    <WebView
        android:id="@+id/myWebView"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
    </WebView>
```

##### 3.Java实现

为btn按钮添加一个监听器，获取网址，隐式调用

```
EditText url = (EditText)findViewById(R.id.url);
String data = url.getText().toString();
Intent intent = new Intent();
//String data = "https://www.baidu.com/?tn=64075107_1_dg";
//根据指定字符串解析出uri对象
Uri uri = Uri.parse(data);
//为intent设置action属性
intent.setAction(Intent.ACTION_VIEW);
intent.setData(uri);
startActivity(intent);
```

自定义webview

```
Intent intent = getIntent();
Uri data = intent.getData();
WebView webView = (WebView)findViewById(R.id.myWebView);
webView.setWebViewClient(new WebViewClient());
webView.loadUrl(data.toString());
```

在AndroidManifest.xml中编写intent-filter并允许使用internet

```
<intent-filter>
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT"/>
    <data android:scheme="https" />
    <!--uri字符串总满足以下格式：scheme://host:port/path-->
</intent-filter>
…………
<uses-permission android:name="android.permission.INTERNET"/>
```

实验截图 ：

<img src="https://github.com/chaozhankai/AS-product/blob/master/text6/text6/Intent/app/jiemian.png" height="400" alt="Screenshot"/>

  

<img src="https://github.com/chaozhankai/AS-product/blob/master/text6/text6/Intent/app/guge.png" height="400" alt="Screenshot"/>

  

<img src="https://github.com/chaozhankai/AS-product/blob/master/text6/text6/Intent/app/mybrowser.png" height="400" alt="Screenshot"/>



