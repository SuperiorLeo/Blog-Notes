## 如何用Andriod Studio做一个简易学习APP---入门
1. 第一次写博客，可能会有很多不足，学校的项目设计迫在眉睫，虽然我已经学习andriod快两个月了，视频推荐看小破站的天哥在奔跑。
2. 我的b站用视频的方式直接简短的讲解了一个完整app的开发过程，大家若需要的话，可以移步[b站教程](https://www.bilibili.com/video/BV1MK411p7dp/)
3. b站视频主要是
4. ![b站视频目录](https://i-blog.csdnimg.cn/blog_migrate/f3d14530dbba69c38604a61b4cb4b876.png)
## 修订
1. 这篇博客比较长，所以一些修订我就不在这里改了，因为怕大家又重新去找，很麻烦，但是我每次修订，都会把链接放在这里
2. 解决soundpool的播放音效只有几秒和监听事件重写[mediaplayer](https://blog.csdn.net/weixin_43589465/article/details/105442929)
3. 如何理解button[跳转](https://blog.csdn.net/weixin_43589465/article/details/105385707)
4. 优化之如何设计[圆形头像](https://blog.csdn.net/weixin_43589465/article/details/106200310)
5. 优化之如何[去掉顶部栏](https://blog.csdn.net/weixin_43589465/article/details/106344476)

## 文件目录
1. 我刚开始接触的时候，看网上大佬们写的文件，都不知道该放在哪里，所以我这里先把文件所在的目录贴出来。
2. ![建议大家命名用你想做的东西的英文名，方便找](https://i-blog.csdnimg.cn/blog_migrate/cece480e1c6f741dc554bfefc186af75.png)
3. ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/29d41705ca773ad6b8a94695bc09608b.png)
4. ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/6cc185afb4cc9e3f5294c8cf6bcba3b1.png)
##  整个软件的设计思路
1. 我就直接把mindmap贴出来了，太难的打字了，现在已经12点了。![mindmap](https://i-blog.csdnimg.cn/blog_migrate/00b77ad509881f7c438609f1a59178f0.png)

## 正题开始-登录和注册界面
 1. 设计的很丑，先看整体效果
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/e9c93865bc81c30b4cdb50634dd2ce9d.png)
 2. 那么这个界面的layout文件是怎么实现的
 	1. 需要一个textview放我们的标题
 	2. 需要两个edittext作为密码和账号的输入
 	3. 需要两个按钮实现登录和注册的操作
3. 下面展示一些 `内联代码片`，这个具体的原因我就不解释了。

```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@drawable/background"
    tools:context=".MainActivity"
    android:paddingTop="100dp">

    <TextView
        android:id="@+id/tv_title"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="E.va"
        android:gravity="center"
        android:textColor="@color/colorBlue"
        android:textSize="20sp"
        />

    <EditText
        android:id="@+id/et_1"
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:textSize="16sp"
        android:textColor="#000000"
        android:hint="用户名"
        android:background="@drawable/bg_username"
        android:layout_marginLeft="10dp"
        android:layout_marginRight="10dp"
        android:maxLines="1"
        android:paddingLeft="10dp"
        android:paddingRight="10dp"
        android:layout_marginTop="10dp"
        android:layout_below="@id/tv_title"
        />


    <EditText
        android:id="@+id/et_2"
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:textSize="16sp"
        android:textColor="#000000"
        android:hint="密     码"
        android:layout_marginLeft="10dp"
        android:layout_marginRight="10dp"
        android:inputType="textPassword"
        android:layout_below="@id/et_1"
        android:layout_marginTop="10dp"
        android:background="@drawable/bg_username"
        android:maxLines="1"
        android:paddingLeft="10dp"
        android:paddingRight="10dp"
        />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_below="@id/et_2"
        android:paddingLeft="10dp"
        android:paddingRight="10dp"
        >

        <Button
            android:id="@+id/btn_login"
            android:layout_width="0dp"
            android:layout_weight="1"
            android:layout_height="50dp"
            android:gravity="center"
            android:layout_marginTop="20dp"
            android:text="登录"
            android:textSize="18sp"
            android:textColor="#000000"
            android:background="@drawable/bg_btn4"
            />

        <Button
            android:id="@+id/ben_register"
            android:layout_width="0dp"
            android:layout_weight="1"
            android:layout_height="50dp"
            android:gravity="center"
            android:layout_marginTop="20dp"
            android:text="注册"
            android:textSize="18sp"
            android:textColor="#000000"
            android:background="@drawable/bg_btn4"
            />

    </LinearLayout>

</RelativeLayout>
```
5. 那么怎么实现登录和注册呢，太巧了，我现在也不是很会服务器端的登录和注册，如果有会的，希望我们一起探讨。那么下面我给出一种，已知账号和密码的登录方式
6. 实现button的跳转，都是很固定的操作，可以通过下面的探讨和前面说的视频学习
7. 下面展示一些 `内联代码片`。

```
package com.example.eva;

import android.content.Intent;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;

import com.example.eva.util.ToastUtil;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {

    //给控件声明
    private Button mBtnLogin;
    private Button mBtnRegister;
    private EditText mTUserName;
    private EditText mTPassword;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //找到控件
        mBtnLogin = findViewById(R.id.btn_login);
        mBtnRegister = findViewById(R.id.ben_register);
        mTUserName = findViewById(R.id.et_1);
        mTPassword = findViewById(R.id.et_2);
        //暂时只对登录设置了情况，采用提前注入信息的形式
        mBtnLogin.setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        //获取输入的信息
        String username = mTUserName.getText().toString();
        String password = mTPassword.getText().toString();
        String ok = "登陆成功";
        String fail = "密码错误，登陆失败";
        Intent intent = null;

        if(username.equals("lyh")&&password.equals("123456")){
            //这个类是自己封装的一个类
            ToastUtil.showMsg(MainActivity.this,ok);
            //下面实现的是登陆界面的跳转
            intent = new Intent(MainActivity.this, UiActivity.class);
            startActivity(intent);
        }else{
            //登录成功或者失败我们都需要弹出一个信息来告诉用户是成功还是失败
            ToastUtil.showMsg(MainActivity.this,fail);
        }
    }

    @Override
    public void onPointerCaptureChanged(boolean hasCapture) {

    }
}

```
## 登陆界面说完，我们来说具体的几个功能
1. 还是先把功能的图片附上吧
2. 刚开始![刚开始很简陋，大家可以根据自己的要求来做](https://i-blog.csdnimg.cn/blog_migrate/aa6691b545b4775f24c1ecd0fa036364.png)
3. 看图片我们可以得出这个界面我们一共需要一个textview和四个button，并实现对应button的跳转，我在想要不要讲一下跳转，我们先放在这把，如果后面我写完还没到三点的话，我就给大家讲一下我的理解。
4. 我们看一下这个部分的布局文件
5. 下面展示一些 `内联代码片`。

```
<TextView
       android:layout_width="match_parent"
       android:layout_height="30dp"
       android:text="选择学习类型"
       android:gravity="center"
       android:layout_marginTop="200dp"
       android:textColor="#000000"/>

    <Button
        android:id="@+id/btn_1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="背单词"
        android:textColor="#000000"
        android:layout_marginTop="10dp"
        android:background="@drawable/bg_btn4"
        />

    <Button
        android:id="@+id/btn_2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="阅读理解"
        android:textColor="#000000"
        android:background="@drawable/bg_btn4"
        />

    <Button
        android:id="@+id/btn_3"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="听力测试"
        android:background="@drawable/bg_btn4"
        android:textColor="#000000"
        />

    <Button
        android:id="@+id/btn_4"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="今日小测"
        android:background="@drawable/bg_btn4"
        android:textColor="#000000"
        />
```
6. 在这还是讲一下button里面的各种性质吧
	1. id名，如果你要设置button点击事件的话，这个是必须要的哈，不然找不到文件的
	2. width和height顾名思义就是高度和宽度的设置，match_parent的意思就是和父类的一样，wrap_content你可以理解为有多宽显示多宽
	3. text 还有一个是可以放图片的android:drawableLeft，如果想要button里面有一个图片的话，可以用这个
	4. 界面说完了，我们来看一下，这个的跳转怎么实现的，我方的基本都是源码，没有修改的，如果直接赋值的话，可能会报很多错误，因为很多文件你还没有去创建，慢慢创建，最后就不会出错了。
	5. 这个代码，我建议大家可以保存一下，因为这个监听事件写的真的是太漂亮了，不管是排版还是可读性来看，下面展示一些 `内联代码片`。

```
package com.example.eva;

import android.content.Intent;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

public class UiActivity extends AppCompatActivity {
    private Button mBtnWord;
    private Button mBtnRead;
    private Button mBtnListen;
    private Button mBtnTest;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_ui_acticity);

        mBtnWord = findViewById(R.id.btn_1);
        mBtnRead = findViewById(R.id.btn_2);
        mBtnListen = findViewById(R.id.btn_3);
        mBtnTest = findViewById(R.id.btn_4);

        //设置监听事件
        setListener();
    }

   private void setListener(){
        OnClick onClick = new OnClick();
        mBtnWord.setOnClickListener(onClick);
        mBtnRead.setOnClickListener(onClick);
        mBtnListen.setOnClickListener(onClick);
        mBtnTest.setOnClickListener(onClick);
   }

   private class OnClick implements View.OnClickListener{

       @Override
       public void onClick(View v) {
           Intent intent = null;
           switch (v.getId()) {
               case R.id.btn_1:
                   intent = new Intent(UiActivity.this, WordActivity.class);
                   break;
               case R.id.btn_2:
                   intent = new Intent(UiActivity.this, CompreActivity.class);
                   break;
               case R.id.btn_3:
                   intent = new Intent(UiActivity.this, ListenActivity.class);
                   break;
               case R.id.btn_4:
                   intent = new Intent(UiActivity.this, TestActivity.class);
                   break;
           }
           startActivity(intent);
       }
   }

}

```
## 主界面说完了，我们来看看具体的小界面是怎么做的
1. 好吧，才过了20分钟，是我讲的太水了吗？哎，初版先这个亚子吧，后面我们在一起修改，毕竟听学长说在项目设计这块，通院还是挺团结的，hhh
2. 第一个界面，背单词界面，仿造的是百词斩，很多部分还没做全，我就不一直解释了，以后我们再来改，先看图。
3. ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a1aabacdb5ae6d92f19b69fde86ab91d.png)
4. ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/92636516a5d2c6531a74e7da952975a6.png)
5. 第一个界面用的都是我们之前讲的知识，textview和一个button，但是这里有一个比较巧妙地地方，我还是说一下，大家可以看到今日单词和学习天数是并列和平分的对吧，这里其实是一个权重的应用，大家都是工科生，应该还是明白的吧...我把代码贴出来,大家仔细理解一下
6. 下面展示一些 `内联代码片`。

```
<LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_below="@+id/tv_word"
        android:layout_marginTop="30dp"
        android:id="@+id/ll_1"
        >
        <--- 首先我们在最开始的LinearLayout文件下套一个LinearLayout--->
        <TextView
            android:layout_width="0dp"
            android:layout_weight="1"
            android:layout_height="100dp"
            android:text="今日单词:20"
            android:textColor="@color/colorBlack"
            android:gravity="center"
            android:textSize="20sp"
            android:background="@drawable/bg_username"
            android:paddingLeft="10dp"
            />
<--- 大家仔细看这里的两个的width和之前有什么不同，并且多了weight这个，这便是我们刚刚说的权重的问题，两个权重一样，自然是评分，三个自然就是各占1\3--->
        <TextView
            android:layout_width="0dp"
            android:layout_weight="1"
            android:layout_height="100dp"
            android:text="学习天数:100"
            android:textColor="@color/colorBlack"
            android:gravity="center"
            android:textSize="20sp"
            android:background="@drawable/bg_username"
            android:paddingRight="10dp"
            />

    </LinearLayout>
```
7. 这个按钮的跳转
8. 下面展示一些 `内联代码片`。

```
package com.example.eva;

import android.content.Intent;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

public class WordActivity extends AppCompatActivity {
    private Button mBtnWordStart;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_word);
        mBtnWordStart = findViewById(R.id.btn_wordstart);
        mBtnWordStart.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = null;
                intent = new Intent(WordActivity.this,WordTestActivity.class);
                startActivity(intent);
            }
        });
    }
}

```
9. 下面展示一些 `内联代码片`。

```
<ImageView
        android:id="@+id/iv_grid"
        android:layout_width="160dp"
        android:layout_height="120dp"
        android:scaleType="centerCrop"
        android:background="@drawable/plane"
        android:layout_gravity="center"
        />
```
10. 那么第二个切单词的是怎么做的呢，仔细一看，你会发现，这里面怎么又图片，我怎么把图片加载进去呢？
	1. 第一步，把你需要的图片加入到drawable下面的drawable_xhdpi,不要问我为甚这么命名，我也不知道，hh，教程和一些书籍都是这样命名的，记住，千万不要直接放在drawable下面，如果不信，你们可以试一试，原因，百度就知道了哈。
	2. 然后我们来分析这个布局应该怎么去写. 
	3. 这里介绍一个GridView，顾名思义，表格视图，比如可以联系我们的这个图片，这里我需要四个表格来放四张图片
	4. 下面展示一些 `内联代码片`。

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".WordTestActivity"
    android:background="@drawable/background_2"
    android:orientation="vertical">

    <TextView
        android:id="@+id/tv_1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="technology"
        android:textSize="30sp"
        android:textColor="@color/colorBlack"
        android:gravity="center"
        android:layout_marginTop="170dp"
        />

    <GridView
        android:id="@+id/gv"
        android:layout_width="match_parent"
        android:layout_height="400dp"
        android:numColumns="2"
        android:horizontalSpacing="10dp"
        android:verticalSpacing="10dp"
        android:layout_marginTop="20dp"/>

</LinearLayout>
```
5. 显然到这里我们还没有实现将图片放进去的操作，大家可以把它想象成我先把空间划分好，具体的内容我需要到另一个文件中添加，那么这个文件是什么呢？我也把代码给大家附在下面，新建一个layout_grid_item文件，在该文件下放item的样子下面展示一些 `内联代码片`。

```
<ImageView
        android:id="@+id/iv_grid"
        android:layout_width="160dp"
        android:layout_height="120dp"
        android:scaleType="centerCrop"
        android:background="@drawable/plane"
        android:layout_gravity="center"
        />
```
6. 我们只需要一个图片，那么这个问价下面自然只需要一个放图片的控件就可以.，啊，我好困，但这个真的很不好理解，我学的时候都想了好久好久
7. 接下来，我们文件写好了，就要在对应的java文件中去实现下面展示一些 `内联代码片。

```
package com.example.eva;

import android.app.Activity;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.text.TextUtils;
import android.view.View;
import android.widget.AdapterView;
import android.widget.GridView;
import android.widget.SimpleAdapter;

import com.example.eva.util.ToastUtil;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class WordTestActivity extends Activity {

    private GridView mGv;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_word_test);

        mGv = findViewById(R.id.gv);
        mGv.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                //去判断他点击的是不是正确的图片，这里是举例，直接给定的结果
                if(position == 1){
                    ToastUtil.showMsg(WordTestActivity.this,"恭喜你，选择正确");
                }else{
                    ToastUtil.showMsg(WordTestActivity.this,"选择错误，请仔细一点哦");
                }
            }
        });

        int[] imageAry = new int[]{
                R.drawable.plane,R.drawable.technology,R.drawable.cat,R.drawable.battle
        };

        List list = new ArrayList();

        for (int i = 0;i<imageAry.length;i++){
            Map map = new HashMap();
            map.put("image",imageAry[i]);
            list.add(map);
        }
        //实例化SimpleAdapter适配器的对象
        SimpleAdapter adapter = new SimpleAdapter(this,list,R.layout.layout_grid_item,
                new String[]{"image"},new int[]{R.id.iv_grid});
        //获得GridView组件
        GridView gridView = (GridView) findViewById(R.id.gv);
        //向GridView中添加内容
        gridView.setAdapter(adapter);
    }
}

```
11.emm..这个adapter大家要是不明白的话建议看一下天哥的视频，到现在已经又13000多字了，如果解释的话，会有些冗杂
12. 到现在为止呢，你已经实现了我们斩单词界面的设计了，如果成功的话，你会很有成就感的，hhh
## 接下来，我就挑一下八，讲一下这个听力测试的这个部分
1. 还是一样，我们先把图片放出来，先思考一下这个界面我们应该怎么去设计
2. ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/a4b3e1ad2d49203530f3d9feec8d8fdc.png)
3. 我这里比较简洁哈
	1. 两个textview，三个button，以及一个我们之前都没有讲到的多选框，因为单独讲单选和多选太累了，后面在添加吧。
	2. 实现多选呢，我这里用了四个checkbox来实现
	3. 最后结果，这里简单，我是只要提交都是100分，大家可以去判断哪个复选框选中来给出正确还是失败，学习一直都是模仿到自己做，也是给自己的一个锻炼把，说了这么多，其实是因为我也还没有写，hhh
	4. activity_listen.xml文件 `内联代码片`。

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:background="@drawable/background_2"
    tools:context=".ListenActivity"
    android:padding="20dp">

    <TextView
        android:id="@+id/tv_listen_title"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="听力测试"
        android:textColor="@color/colorBlack"
        android:gravity="center_horizontal"
        android:textSize="25sp"
        android:layout_marginTop="20dp"/>

    <Button
        android:id="@+id/btn_play"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="播放听力"
        android:textColor="@color/colorBlack"
        android:layout_marginTop="10dp"/>

    <Button
        android:id="@+id/btn_pause"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="暂停播放"
        android:textColor="@color/colorBlack" />

    <LinearLayout
        android:id="@+id/ll_listen_question"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:padding="20dp">

        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Section A"
            android:textAllCaps="false"
            android:textColor="@color/colorBlack"
            android:textSize="20sp"
            android:gravity="center"
            android:layout_marginTop="15dp"/>

        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Question 1 to 4 are based on the conversation you have just heard"
            android:textColor="@color/colorBlack"
            android:layout_marginTop="10dp"
            android:layout_marginBottom="10dp"/>

        <CheckBox
            android:id="@+id/cb_1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Buy a used car"
            android:textColor="@color/colorBlack"/>

        <CheckBox
            android:id="@+id/cb_2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_below="@id/cb_1"
            android:text="Have his car repaired"
            android:textColor="@color/colorBlack"/>

        <CheckBox
            android:id="@+id/cb_3"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_below="@id/cb_2"
            android:text="Pass a driving test"
            android:textColor="@color/colorBlack"/>

        <CheckBox
            android:id="@+id/cb_4"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_below="@id/cb_3"
            android:text="Sell a car"
            android:textColor="@color/colorBlack"/>

        <Button
            android:id="@+id/btn_listen_submit"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="提交"
            android:textColor="@color/colorBlack"
            android:layout_below="@id/cb_4"
            android:layout_marginTop="10dp"/>
    </LinearLayout>



</LinearLayout>
```
4. 那么来到了这几个button
	1. 播放音频和暂停音频的button大家参考[如何给button添加音效](https://blog.csdn.net/juer2017/article/details/101216632)
	2. 最后一个button，如果不去判断正确性的话就很简单，监听事件即可
	3. ListenActivity的代码
	4. 下面展示一些 `内联代码片`。

```
package com.example.eva;

import android.content.Context;
import android.media.AudioManager;
import android.media.SoundPool;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.LinearLayout;

import com.example.eva.util.ToastUtil;

import java.util.HashMap;

public class ListenActivity extends AppCompatActivity {

    private Button mBtnPlay,mBtnPause,mBtnListenSubmit;
    SoundPool sp;//声明soundpool
    HashMap<Integer,Integer> hm;//hashmap用于存放音频文件
    int currStreamId;//当前正在播放的streamId

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_listen);
        mBtnPlay = findViewById(R.id.btn_play);
        mBtnPause = findViewById(R.id.btn_pause);
        mBtnListenSubmit = findViewById(R.id.btn_listen_submit);
        initSoundPool();//调用方法，初始化

        //两个按钮的点击事件
        mBtnPlay.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                playSound(1,0);
                ToastUtil.showMsg(ListenActivity.this,"播放开始");

            }
        });

        mBtnPause.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                sp.stop(currStreamId);//停止正在播放的
                ToastUtil.showMsg(ListenActivity.this,"播放已暂停");
            }
        });

        mBtnListenSubmit.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                ToastUtil.showMsg(ListenActivity.this,"提交成功");
            }
        });
    }

    private void playSound(int sound ,int loop){
        //AudioManager的使用
        AudioManager am = (AudioManager) this.getSystemService(Context.AUDIO_SERVICE);
        //获取当前音量
        float streamVolumeCurrent = am.getStreamVolume(AudioManager.STREAM_MUSIC);
        //获取z最大音量
        float streamVolumeMax = am.getStreamMaxVolume(AudioManager.STREAM_MUSIC);
        //计算一下播放的音量
        float volume = streamVolumeCurrent / streamVolumeMax;
        //调用方法来播放声音文件
        currStreamId = sp.play(hm.get(sound), volume , volume , 1, loop ,1.0f);
    }

    private void initSoundPool() {
        sp = new SoundPool(4, AudioManager.STREAM_MUSIC,0);//创建对象
        hm = new HashMap<Integer, Integer>();//create 对象来放音频
        //加载声音，并将声音放入hm中
        hm.put(1,sp.load(this,R.raw.listen,1));
    }
}

```
5. 我已经不记得编号是多少了，晕，到这里呢，我们已经实现了两个界面的跳转了，剩下的两个我就不演示了，因为很多东西都是重复的，而且大家做的东西还是有一些不太一样，只要学会了方法，很多东西都是举一反三的。
## 里面有一个封装的ToastUtil的类
1. 我把源码放在这了，比较我也是参照天哥的代码写的，相互帮助最可爱啦
2. 下面展示一些 `内联代码片`。

```
package com.example.eva.util;

import android.content.Context;
import android.widget.Toast;

//进行一个简单的封装
public class ToastUtil {
    public static Toast mToast;
    public static void showMsg(Context context, String msg){
        if ((mToast == null)){
            mToast = Toast.makeText(context,msg,Toast.LENGTH_LONG);
        }else {
            mToast.setText(msg);
        }
        mToast.show();
    }

}

```
## 关于源码
1. 我本来是想传到github的，不过看了一下我自己的界面设计，实在是太难看了，我也才学了2个月，很多地方还有一些不足，所以暂时先不上传了。
2. 这篇文章是我第一次写博客，很多地方写的不是很好，有些东西解释的也不是很清楚，但是大家可以作为茶余饭后看一看，也求指导一下我不会的地方。
3. 后面如果有更新我再放在这个csdn上，快2万字了，又饿又困。
## 声明
1. 拒绝一切啥都不改的白嫖党哈，每个东西要有自己的特色才有意义。
2. 转发请标明出处
## 联系方式
1. 我的邮箱578018334@qq.com,emm...如果有更好的办法或者错误纠正，欢迎呀
2. 我还是希望大家在这个csdn上留言，这样会的都可以相互指导，人多了，项目设计自然就不是问题啦。

