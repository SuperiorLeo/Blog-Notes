## 如何设计圆形头像
1. 很多时候，我们需要设计类似于头像一样的部分，但是这部分很多时候都是用圆形头像，本篇博客就是讨论如何设计圆形头像
## 效果图
![效果图](https://i-blog.csdnimg.cn/blog_migrate/5d797611e11ddb782cf8c53ca4a235cb.jpeg)
## 实现代码
1. 利用widget下的cardview和imageview实现。
2. 整体分为两个部分，先划分总体布局和圆形区域；接着在圆形区域插入目标图片。
3. 注意imageview部分，width和height一定是match_parent，因为是在第一步划分的圆形区域显示的。
```
<android.support.v7.widget.CardView
            android:id="@+id/cv_user_head"
            android:layout_width="60dp"
            android:layout_height="60dp"
            app:cardCornerRadius="45dp"
            app:cardElevation="10dp"
            android:layout_marginTop="5dp"
            android:layout_marginLeft="220dp"
            app:cardPreventCornerOverlap="true"
            >
            <ImageView
                android:id="@+id/tv_user_head"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:src="@drawable/head"
                android:scaleType="centerCrop"/>
        </android.support.v7.widget.CardView>
```


