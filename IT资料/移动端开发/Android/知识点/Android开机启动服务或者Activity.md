有些时候，应用需要在开机时就自动运行，例如某个自动从网上更新内容的后台 `service`。怎样实现开机自动运行的应用？在撰写本文时，联想到高焕堂先生以“Don''t call me, I''ll call you back!”总结Android框架，真是说到点子上了。理解这句话的含义，许多有关Android平台上实现某种功能的问题，都能迎刃而解。

使用场景：手机开机后，自动运行程序，在屏幕上显示"Hello. I started!"字样。

背景知识：当Android启动时，会发出一个系统广播，内容为 `ACTION_BOOT_COMPLETED`，它的字符串常量表示为`android.intent.action.BOOT_COMPLETED`。只要在程序中“捕捉”到这个消息，再启动之即可。记住，Android框架说：Don''t call me, I''ll call you back。我们要做的是做好接收这个消息的准备，而实现的手段就是实现一个`BroadcastReceiver`。

代码解析：

> 1. 界面Activity：SayHello.java

```java
package com.ghstudio.BootStartDemo;

import android.app.Activity;
import android.os.Bundle;
import android.widget.TextView;

public class SayHello extends Activity {

@Override
public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);


TextView tv = new TextView(this);
tv.setText("Hello. I started!");


setContentView(tv);
}
}
```

这段代码很简单，当Activity启动时，创建一个TextView，用它显示"Hello. I started!"字样。

> 2. 接收广播消息：BootBroadcastReceiver.java

```java
package com.ghstudio.BootStartDemo;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;

public class BootBroadcastReceiver extends BroadcastReceiver {

static final String ACTION = "android.intent.action.BOOT_COMPLETED";

@Override
public void onReceive(Context context, Intent intent) {

if (intent.getAction().equals(ACTION)){
Intent sayHelloIntent=new Intent(context,SayHello.class);
sayHelloIntent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);

context.startActivity(sayHelloIntent);
}
}

}
```

该类派生自BroadcastReceiver，覆载方法onReceive中，检测接收到的Intent是否符合BOOT_COMPLETED，如果符合，则启动SayHello那个Activity。

> 3. 配置文件：AndroidManifest.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
package="com.ghstudio.BootStartDemo"
android:versionCode="1"
android:versionName="1.0">
<application android:icon="@drawable/icon" android:label="@string/app_name">
<activity android:name=".SayHello"
android:label="@string/app_name">
<intent-filter>
<action android:name="android.intent.action.MAIN" />
<category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
</activity>
<receiver android:name=".BootBroadcastReceiver">
<intent-filter>
<action android:name="android.intent.action.BOOT_COMPLETED" />
</intent-filter>
</receiver>
</application>
<uses-sdk android:minSdkVersion="3" />

<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"></uses-permission>

</manifest>
```

注意其中粗体字那一部分，该节点向系统注册了一个`receiver`，子节点`intent-filter`表示接收 `android.intent.action.BOOT_COMPLETED`消息。不要忘记配置 `android.permission.RECEIVE_BOOT_COMPLETED`权限。

完成后，编译出apk包，安装到模拟器或手机中。关机，重新开机。