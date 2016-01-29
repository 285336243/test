
##### android support v7包自带的ActionBarActivity的配置

###### 完整类名：android.support.v7.app.ActionBarActivity；  
  ActionBarActivity被废了，以前的老项目还在用，记录下配置
1. 左边显示配置
```java
 //设置标题
 getSupportActionBar().setTitle("聊天");
 //actionbar 添加logo
 getSupportActionBar().setLogo(R.drawable.de_bar_logo);
 //右侧可点击
 getSupportActionBar().setDisplayHomeAsUpEnabled(true);
 //设置右边图片
 getSupportActionBar().setHomeAsUpIndicator(R.drawable.de_actionbar_back);
```
**效果图：**
![image](http://d.picphotos.baidu.com/album/s%3D1100%3Bq%3D90/sign=2830ec0e7ff0f736dcfe48003a658868/adaf2edda3cc7cd90e44eea83e01213fb80e9152.jpg "效果图")


---

2. 右边显示配置  
继承类中设置：  

```java
 @Override
    public boolean onCreateOptionsMenu(Menu menu) {

        MenuInflater inflater = getMenuInflater();
        this.mMenu = menu;
        inflater.inflate(R.menu.de_main_menu, menu);
        if (hasNewFriends) {
            mMenu.getItem(0).setIcon(getResources().getDrawable(R.drawable.de_ic_add_hasmessage));
            mMenu.getItem(0).getSubMenu().getItem(1).setIcon(getResources().getDrawable(R.drawable.de_btn_main_contacts_select));
        } else {
            mMenu.getItem(0).setIcon(getResources().getDrawable(R.drawable.de_ic_add));
            mMenu.getItem(0).getSubMenu().getItem(1).setIcon(getResources().getDrawable(R.drawable.de_btn_main_contacts));
        }

        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        switch (item.getItemId()) {
            case R.id.add_item1://发起聊天
                startActivity(new Intent(this, FriendListActivity.class));
                break;
//            case R.id.add_item2://选择群组
//
//                if (RongIM.getInstance() != null)
//                    RongIM.getInstance().startSubConversationList(this, Conversation.ConversationType.GROUP);
//                break;
            case R.id.add_item3://通讯录
                startActivity(new Intent(MainActivity.this, ContactsActivity.class));
                break;
            case R.id.set_item1://我的账号
                startActivity(new Intent(MainActivity.this, MyAccountActivity.class));
                break;
            case R.id.set_item2://新消息提醒
                startActivity(new Intent(MainActivity.this, NewMessageRemindActivity.class));
                break;
            case R.id.set_item3://隐私
                startActivity(new Intent(MainActivity.this, PrivacyActivity.class));
                break;
            case R.id.set_item4://关于融云
                startActivity(new Intent(MainActivity.this, AboutRongCloudActivity.class));
                break;
            case R.id.set_item5://退出

                final AlertDialog.Builder alterDialog = new AlertDialog.Builder(this);
                alterDialog.setMessage("确定退出应用？");
                alterDialog.setCancelable(true);

                alterDialog.setPositiveButton("确定", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                   //do something
                    }
                });
                alterDialog.setNegativeButton("取消", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        dialog.cancel();
                    }
                });
                alterDialog.show();

                break;
        }
        return super.onOptionsItemSelected(item);
    }
```

布局文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"

    xmlns:app="http://schemas.android.com/apk/res-auto">

    <item
        android:id="@+id/action_add_conversation"
        android:icon="@drawable/de_ic_add"
        android:title="@string/action_settings"
        app:showAsAction="ifRoom|withText">
        <menu>
            <item
                android:id="@+id/add_item1"
                android:icon="@drawable/de_btn_main_chat"
                android:title="@string/add_chat" />
            <!--<item-->
                <!--android:id="@+id/add_item2"-->
                <!--android:icon="@drawable/de_btn_main_groups"-->
                <!--android:title="@string/add_select_group" />-->
            <item
                android:id="@+id/add_item3"
                android:icon="@drawable/de_btn_main_contacts"
                android:title="@string/add_contacts" />
        </menu>
    </item>


    <item
        android:id="@+id/action_settings"
        android:icon="@drawable/de_ic_set"
        android:orderInCategory="100"
        android:title="@string/set_set"
        app:showAsAction="ifRoom|withText">
        <menu>
            <item
                android:id="@+id/set_item1"
                android:icon="@drawable/de_btn_main_personal_information"
                android:title="@string/set_personal_information" />
            <item
                android:id="@+id/set_item2"
                android:icon="@drawable/de_btn_main_news_reminded"
                android:title="@string/set_news_reminded" />
            <item
                android:id="@+id/set_item3"
                android:icon="@drawable/de_btn_main_privacy"
                android:title="@string/set_privacy" />
            <item
                android:id="@+id/set_item4"
                android:icon="@drawable/de_btn_main_rongcloud"
                android:title="@string/set_rongcloud" />
            <item
                android:id="@+id/set_item5"
                android:icon="@drawable/de_btn_main_sign_out"
                android:title="@string/set_logout" />
        </menu>
    </item>
</menu>
```
##### 效果图：
- 添加朋友    
![添加朋友](http://f.picphotos.baidu.com/album/s%3D1100%3Bq%3D90/sign=3a284fcda7ec08fa220017a669de061c/32fa828ba61ea8d330349f76900a304e251f58aa.jpg "添加朋友")  
- 设置：  <br>
![设置](http://g.picphotos.baidu.com/album/s%3D740%3Bq%3D90/sign=258bde0d7ff0f736dcfe4e053a6ec224/b3b7d0a20cf431ad4500ab4b4c36acaf2fdd98f6.jpg "设置")<br>

添加新朋友后,图标变化：  
![添加新朋友后](http://a.picphotos.baidu.com/album/s%3D1100%3Bq%3D90/sign=1efeb6220b33874498c52b7d613fe288/c9fcc3cec3fdfc037a9f0bcad33f8794a5c226d9.jpg "添加新朋友后")

参考：==融云demo源码==
