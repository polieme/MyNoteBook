## 大概原理
大致原理是,如果手指按在view上，则使用ScheduledExecutorService对象执行scheduleWithFixedDelay()方法，每隔一个间隔不停地向Handler发送Message，此处Message里的信息是View id，然后由Handler在handlemessage的时候处理需要触发的事件。

## 实现
1. 首先,让对应的View设置一个OnTouchListener，在手指按下时触发不停的发送消息,手指抬起时停止发送
```java
subtractButton.setOnTouchListener(new OnTouchListener() {
            @Override
            public boolean onTouch(View v, MotionEvent event) {
                if(event.getAction() == MotionEvent.ACTION_DOWN){
                    updateAddOrSubtract(v.getId());    //手指按下时触发不停的发送消息
                }else if(event.getAction() == MotionEvent.ACTION_UP){
                    stopAddOrSubtract();    //手指抬起时停止发送
                }
                return true;
            }
        });
```

2. 发送消息与终止方法：先定义一个ScheduledExecutorService对象，然后调用scheduleWithFixedDelay()方法
```java
private ScheduledExecutorService scheduledExecutor;
private void updateAddOrSubtract(int viewId) {
           stop();//如果同时摁两个按钮或两个以上，会出现定时器不能停止的问题，因此在这里加上这个，把之前的定时器先关掉
     
        final int vid = viewId;
        scheduledExecutor = Executors.newSingleThreadScheduledExecutor();
        scheduledExecutor.scheduleWithFixedDelay(new Runnable() {
            @Override
            public void run() {
                Message msg = new Message();
                msg.what = vid;
                handler.sendMessage(msg);
            }
        }, 0, 100, TimeUnit.MILLISECONDS);    //每间隔100ms发送Message
    }

    private void stopAddOrSubtract() {
        if (scheduledExecutor != null) {
            scheduledExecutor.shutdownNow();
            scheduledExecutor = null;
        }
    }
```
3. 用来处理Touch事件的Handler定义如下：
```java
private Handler handler = new Handler(){
        @Override
        public void handleMessage(Message msg) {
            int viewId = msg.what;
            switch (viewId){
                case R.id.custom_number_picker_subtract_button:
                    setValue(value - rangeability);    //减小操作
                    break;
                case R.id.custom_number_picker_add_button:
                    setValue(value + rangeability);    //增大操作
                    break;
            }
        }
    };
```

