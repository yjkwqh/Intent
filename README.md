# Intent
自定义WebView验证隐式Intent的使用
@[TOC](FiveTest)

# 第五个实验
## Intent
题目：
<img src="https://img-blog.csdnimg.cn/20190416193735915.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ZhZ2Fib25kXw==,size_16,color_FFFFFF,t_70" width="400"/>

第一个应用(Intent文件夹)：
核心代码：
```java
public class MainActivity extends AppCompatActivity {

    private static final String TAG ="fff" ;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button button1 = (Button)findViewById(R.id.b1);


        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                EditText editText = (EditText)findViewById(R.id.e1);
                String text = editText.getText().toString();
                Intent intent = new Intent(Intent.ACTION_VIEW);
                intent.setData(Uri.parse(text));
//                intent.putExtra("url",text);
                startActivity(intent);
            }
        });
    }

}
```
```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_height="match_parent"
    android:layout_width="match_parent"
    android:orientation="horizontal">
<EditText
    android:id="@+id/e1"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:layout_weight="2"
    android:hint="输入网址"/>

<Button
    android:id="@+id/b1"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:layout_weight="1"
    android:text="搜索"/>
</LinearLayout>
```
运行截图：

<img src="https://img-blog.csdnimg.cn/20190416201736873.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ZhZ2Fib25kXw==,size_16,color_FFFFFF,t_70" width="300" height="500"/><img src="https://img-blog.csdnimg.cn/20190416201847506.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ZhZ2Fib25kXw==,size_16,color_FFFFFF,t_70" width="300" height="500"/>

第二个应用：
核心代码：
```java
public class MainActivity extends AppCompatActivity {

    private static final String TAG ="fff" ;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button button1 = (Button)findViewById(R.id.b1);


        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                EditText editText = (EditText)findViewById(R.id.e1);
                String text = editText.getText().toString();
                Intent intent = new Intent(Intent.ACTION_VIEW);
//                intent.setData(Uri.parse(text));
               intent.putExtra("url",text);
                startActivity(intent);
            }
        });
    }

}
```
```java
public class MainActivity extends AppCompatActivity {

    private static final String TAG ="fff" ;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.webview_layout);
        Intent intent = this.getIntent();
        Bundle bundle = intent.getExtras();

        WebView webView = (WebView)findViewById(R.id.webView1);
        webView.getSettings().setJavaScriptEnabled(true);
        webView.setWebViewClient(new WebViewClient());
        if(bundle !=null){
            String url = bundle.getString("url");
            webView.loadUrl(url);
        }
    }
}
```
运行截图：

<img src="https://img-blog.csdnimg.cn/20190416202930559.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ZhZ2Fib25kXw==,size_16,color_FFFFFF,t_70" width="300" height="500"/> <img src="https://img-blog.csdnimg.cn/2019041620302680.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3ZhZ2Fib25kXw==,size_16,color_FFFFFF,t_70" width="300" height="500"/>
