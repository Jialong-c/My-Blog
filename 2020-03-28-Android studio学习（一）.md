---
layout:     post
title:      Android studio学习（一）
subtitle:   学习Android studio关于activity的相关技能
date:       2020-03-28
author:     Jialong
header-img: img/android studio.png
catalog: true
tags:
    - Android studio
    - Mobile application
---
> **Android studio学习**
>
> # 探究“活动”



## 1. 在活动中使用Toast

Toast是Android系统提供的一种提醒方式，在程序中可以使用它将一些短小的信息通知给用户，这些信息会在一段时间后自动消失，并且不会占用任何屏幕空间，我们现在开始在活动中使用Toast。



首先需要定义弹出Toast的触发点，我们以界面上的按钮（**button 1**）作触发器，点击按钮时将弹出一个Toast。在**`onCreate()`**方法中添加如下代码：

```java
protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.first_layout);
        Button button1=(Button) findViewById(R.id.button_1);
        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(firstactivity.this, "you clicked button 1",
                        Toast.LENGTH_SHORT).show();
            }
        });
    }
```

在活动中，可以通过**`findViewById()`**方法获取在布局文件（此代码中为first_layout.xml文件）中定义的元素，这里我们传入**R.id.button_1**。**button**在布局文件下的定义代码如下：

```java
<Button
        android:id="@+id/button_1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="button 1"
        />
```

**`findViewById()`**方法返回的是一个**View**对象，我们需要向下转型将它转成**Button**对象。得到**Button**的实例之后，通过调用**`setOnClickListener()`**方法为其注册一个监听器，点击时就会执行监听器中的**`onClick()`**方法，下来我们在**`onClick()`**方法中编写弹出Toast的功能。



通过静态方法**`makeText()`**创建出一个**Toast**对象，然后调用**`show()`**将**Toast**显示出来就可以了。需要注意的是，**`makeText()`**方法需要传入3个参数。第一个参数是**Context**,也就是**Toast**要求的上下文，由于活动本身就是一个**Context**对象，因此这里直接传入**firstactivity.this**即可。第二个参数是**Toast**显示的文本内容，第三个参数是**Toast**显示的时长，有两个内置常量可以选择**Toast.LENGTH_SHORT**和**Toast.LENGTH_LONG**





## 2. 在活动中使用Menu



手机屏幕的空间非常有限，如果活动中有很多菜单需要显示，这时候就需要使用**Menu**让菜单得到展示的同时，也能不占用任何屏幕空间。



首先在**res**目录下新建一个**menu**文件夹，右击**res**目录-->**New**-->**Directory**，输入文件夹名**menu**。接着在这个文件夹下在新建一个名为**main**的菜单文件，右击**menu**文件夹-->**New**-->**Menu resource file**。然后再main.xml中添加如下代码：

```java
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/add_item"
        android:title="add"/>
    <item
        android:id="@+id/remove_item"
        android:title="remove"/>
</menu>
```



这里我们创建了两个菜单项，其中<**item**>标签就是用来创建具体的某一菜单项，然后通过**android:id**给这个菜单项指定一个唯一的标识符，通过**android:title**给这个菜单项制定一个名称。



接着重新回到**firstactivity**中来重写**`onCreateOptionsMenu()`**方法，重写方法可以使用**Ctrl+O**快捷键。

然后再**`onCreateOptionsMenu()`**方法中编写如下代码：

```java
public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.main, menu);
        return true;
    }
```

通过**`getMenuInflater()`**方法能够得到**MenuInflater**对象，再调用它的**`inflate()`**方法就可以给当前活动创建菜单了。**`inflate()`**方法接收两个参数，第一个参数用于指定我们通过哪一个资源文件来创建菜单，这里传入**R.menu.main**。第二个参数用于指定我们的菜单项将添加到哪一个**Menu**对象中去，这里直接使用**`onCreateOptionsMenu()`**方法中传入的**menu**参数。返回**true**表示允许菜单显示，返回**false**无法显示菜单。



现在已经可以显示出菜单，但这还不够，我们要让菜单可用，就要定义菜单响应事件。在**firstactivity**中重写**`onOptionsItemSelected()`**方法：

```java 
public boolean onOptionsItemSelected(@NonNull MenuItem item) {
        switch (item.getItemId()) {
            case R.id.add_item:
                Toast.makeText(this,"you clicked add",Toast.LENGTH_SHORT).show();
                break;
            case R.id.remove_item:
                Toast.makeText(this,"you clicked remove",Toast.LENGTH_SHORT).show();
                break;
            default:
        }
        return true;
    }
```

在**`onOptionsItemSelected()`**方法中，通过调用**`item.getItemId()`**来判断我们点击的是哪一个菜单项，然后给每个菜单项加入逻辑处理。



## 3. 使用Intent关联活动



### 3.1 使用显式Intent



在项目中创建一个新活动**secondactivity**，在second_layout.xml文件下创建**button 2**，接下来介绍显式**Intent**如何使用。



