|知识点|内容|
|-----|----|
|DrawerLayout|侧滑|
|toolbar|toolbar的按键设置(返回键,菜单),继承和复用,toolbar的navigation导航按钮设置位置|
|底部导航视图+fragment|自己实现底部导航视图|
|baseActivity|要有那些功能|
|关于drawable和drawable-v24|出现的错误  Binary XML file line #0: Error inflating class android.support.design.widget.BottomNavigationView|
|BottomNavigationView|在使用这个控件的时候,一般用到矢量图,需要添加  ` implementation 'com.android.support:design:26.1.0' `和     `implementation 'com.android.support:support-vector-drawable:26.1.0' `和     最后这个在defaultconfigure中 `vectorDrawables.useSupportLibrary= true`|
|fragment使用|使用的相关问题|
|recycleview使用|对item整体的监听|
|textview添加省略|` android:maxLines="1"  android:ellipsize="end"  android:singleLine="true"`|
|**避免在include中添加id,否则layout中的id不能直接findviewbyid**在包含id的include xml代码块中寻找被包含layout的中控件id|因为include的xml代码块中包含id,不能直接用findbyid(R.id.toolbar),需要inflate一个layout,例如,` View layout = getLayoutInflater().inflate(R.layout.toolbar_layout,null);toolbar = layout.findViewById(R.id.toolbar);`|
|在baseActivity中初始化控件是一个错误的做法,尤其是需要在onCreate中对控件进行操作时|因为要findViewById操作,所以需要子类{@link #setContentView(View)}方法执行之后才能初始化toolbar,所以不能在baseActivity的{@link #onCreate(Bundle)} 方法中执行下面这个方法|

|ConstraintLayout|布局倾向于top,bottom,start,end|


### toolbar
- 定义单独的toolbar_layout实现复用效果
- 在styles文件中去除actionbar,去除actionbar的几种方法
- 几个主要属性app:title,subtitle,logo,navigationIcon,通过向toolbar布局中添加textview实现标题在中间的效果
- Toolbar setNavigationIcon无效原因：  1.设置在setSupportActionBar( mToolbar );之前无效；  2.设置在DrawerLayout.setDrawerListener(ActionBarDrawerToggle);之前也无效；
- 下面这几行代码的作用,代码测试 
 ```
     //        getSupportActionBar().setDisplayHomeAsUpEnabled(true);//左侧添加一个默认的返回图标
     //        getSupportActionBar().setHomeButtonEnabled(true);
     //        getSupportActionBar().setDisplayShowHomeEnabled(true);
   ```
### drawable 和 drawable-v24
- 不知道drawable-v24是什么作用,存疑,没有解决
- 图片和布局应该放在drawable中,如果只放在drawable-v24 ,那么xml中应用相关图片和布局的空间不能被实现,报错如下:

```
        Caused by: android.view.InflateException: Binary XML file line #0: Error inflating class android.support.design.widget.BottomNavigationView
```
  
- 上面这个报错的特点是 Binary XML file line #0,后面的控件BottomNavigationView找不到相关对象

### fragment 
- 直接的使用碎片,例如在<fragment>标签中使用name制定类,使用layout制定布局,layout属性不必须,因为那么制定的类就已经会实现布局
- 定义一个framelayout容器,动态添加fragment布局,replace方法,还有add,remove方法,涉及tag标签
- fragment 中使用recycleview,传递参数

### recycleview
- 对item整体监听,有两种考虑   (1) 对整个item的layout布局设置监听 (2) 在adapter中添加一个接口,包含onClick(int position)和onItemClick两个接口方法

### include layout 
- 写代码测试include中包含layout,在寻找layout中的id的方法,**代码测试**