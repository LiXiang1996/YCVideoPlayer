#### 目录介绍
- 1.视频具有的功能
    - 1.1 基础功能
    - 1.2 高级功能
    - 1.3 拓展功能
- 2.使用方法介绍
    - 2.1 关于gradle引用说明
    - 2.2 添加布局
    - 2.3 最简单的视频播放器参数设定
    - 2.4 优化代码
    - 2.5 注意问题
- 3.集成lib说明
    - 3.1 gradle配置添加
    - 3.2 直接导入lib库
    - 3.3 如何选择视频库
- 4.文档wiki说明
    - 4.1 基础方法说明
    - 4.2 视频优化处理
    - 4.3 视频全局悬浮窗播放
    - 4.4 视频封装思路
    - 4.5 视频问题处理
    - 4.6 音视频博客学习
    - 4.7 边播边缓存
    - 4.8 音视频解码过程
    - 4.9 其他零碎知识
- 5.运行的效果展示
- 6.性能优化和库大小
- 7.其他说明



### 1.视频具有的功能




#### 1.1 基础功能
- A基础功能
- A.1.1 能够自定义视频加载loading类型，设置视频标题，设置视频底部图片，设置播放时长等基础功能
- A.1.2 可以切换播放器的视频播放状态，播放错误，播放未开始，播放开始，播放准备中，正在播放，暂停播放，正在缓冲等等状态
- A.1.3 可以自由设置播放器的播放模式，比如，正常播放，全屏播放，和小屏幕播放。其中全屏播放支持旋转屏幕。
- A.1.4 可以支持多种视频播放类型，比如，原生封装视频播放器，还有基于ijkPlayer封装的播放器。
- A.1.5 可以设置是否隐藏播放音量，播放进度，播放亮度等，可以通过拖动seekBar改变视频进度。还支持设置n秒后不操作则隐藏头部和顶部布局功能
- A.1.6 可以设置竖屏模式下全屏模式和横屏模式下的全屏模式，方便多种使用场景
- A.1.7 top和bottom面版消失和显示：点击视频画面会显示、隐藏操作面板；显示后不操作会5秒后自动消失【也可以设置】



#### 1.2 高级功能
- B.1.1 支持一遍播放一遍缓冲的功能，其中缓冲包括两部分，第一种是播放过程中缓冲，第二种是暂停过程中缓冲
- B.1.2 基于ijkPlayer的封装播放器，支持多种格式视频播放
- B.1.3 可以设置是否记录播放位置，设置播放速度，设置屏幕比例
- B.1.4 支持滑动改变音量【屏幕右边】，改变屏幕亮度【屏幕左边】，屏幕底测左右滑动调节进度
- B.1.5 支持list页面中视频播放，滚动后暂停播放，播放可以自由设置是否记录状态。并且还支持删除视频播放位置状态。
- B.1.6 切换横竖屏：切换全屏时，隐藏状态栏，显示自定义top(显示电量)；竖屏时恢复原有状态
- B.1.7 支持切换视频清晰度模式，同时切换清晰度后，支持视频保持观看进度
- B.1.8 添加锁屏功能，竖屏不提供锁屏按钮，横屏全屏时显示，并且锁屏时，屏蔽手势处理
- B.1.9 当在播放视频页面，由前台切换到后台时，如果视频正在播放或者正在缓冲时，则暂停视频；当从后台切换到前台时，如果视频暂停时或者缓冲暂停，则重新开启视频播放；当退出页面时则销毁视频资源。
- B.2.0 当正在缓冲或者播放准备中状态时，开启缓冲时更新网络加载速度[默认时kbs/每秒]


#### 1.3 拓展功能
- **C1产品需求：类似优酷，爱奇艺视频播放器部分逻辑。比如如果用户没有登录也没有看视频权限，则提示试看视频[自定义布局]；如果用户没有登录但是有看视频权限，则正常观看；如果用户登录，但是没有充值会员，部分需要权限视频则进入试看模式，试看结束后弹出充值会员界面；如果用户余额不足，比如余额只有99元，但是视频观看要199元，则又有其他提示。**
- C2自身需求：比如封装好了视频播放库，那么点击视频上登录按钮则跳到登录页面；点击充值会员页面也跳到充值页面。这个通过定义接口，可以让使用者通过方法调用，灵活处理点击事件。
- C.1.1 可以设置试看模式，设置试看时长。试看结束后就提示登录或者充值……
- C.1.2 对于设置视频的宽高，建议设置成4：3或者16：9或者常用比例，如果不是常用比例，则可能会有黑边。其中黑边的背景可以设置
- C.1.3 可以设置播放有权限的视频时的各种文字描述，而没有把它写在封装库中，使用者自己设定
- C.1.5 支持视频小窗口拖拽功能，可以在应用内随意拖拽，单击点击是播放和暂停切换；长按是拖动处理
- C.1.8 支持监听网络状态变化，当从wifi切换到4g，则提示用户视频移动流量提醒通知
- C.1.9 添加了缓冲视频和播放准备中加载视频的时候，显示网络速度的逻辑


### 2.使用方法介绍
#### 2.1 关于gradle引用说明
- 如下所示
    ```
    compile 'cn.yc:YCVideoPlayerLib:2.6.4'
    ```

#### 2.2 添加布局
- 注意，在实际开发中，由于Android手机碎片化比较严重，分辨率太多了，建议灵活设置布局的宽高比为4：3或者16：9或者你认为合适的，可以用代码设置。
- 如果宽高比变形，则会有黑边
    ```
    <org.yczbj.ycvideoplayerlib.VideoPlayer
        android:id="@+id/video_player"
        android:layout_width="match_parent"
        android:layout_height="240dp"/>
    ```


#### 2.3 最简单的视频播放器参数设定
- 如下所示
    ```
    //设置播放类型
    // IjkPlayer or MediaPlayer
    videoPlayer.setPlayerType(VideoPlayer.TYPE_NATIVE);
    //网络视频地址
    String videoUrl = DataUtil.getVideoListData().get(0).getVideoUrl();
    //设置视频地址和请求头部
    videoPlayer.setUp(videoUrl, null);
    //创建视频控制器
    VideoPlayerController controller = new VideoPlayerController(this);
    controller.setTitle("自定义视频播放器可以播放视频拉");
    //设置视频控制器
    videoPlayer.setController(controller);
    ```


#### 2.4 优化代码
- **如果是在Activity中的话，建议设置下面这段代码**
    ```
    @Override
    protected void onStop() {
        super.onStop();
        //从前台切到后台，当视频正在播放或者正在缓冲时，调用该方法暂停视频
        VideoPlayerManager.instance().suspendVideoPlayer();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        //销毁页面，释放，内部的播放器被释放掉，同时如果在全屏、小窗口模式下都会退出
        VideoPlayerManager.instance().releaseVideoPlayer();
    }

    @Override
    public void onBackPressed() {
        //处理返回键逻辑；如果是全屏，则退出全屏；如果是小窗口，则退出小窗口
        if (VideoPlayerManager.instance().onBackPressed()){
            return;
        }else {
            //销毁页面
            VideoPlayerManager.instance().releaseVideoPlayer();
        }
        super.onBackPressed();
    }

    @Override
    protected void onRestart() {
        super.onRestart();
        //从后台切换到前台，当视频暂停时或者缓冲暂停时，调用该方法重新开启视频播放
        VideoPlayerManager.instance().resumeVideoPlayer();
    }
    ```
- **如果是在Fragment中的话，建议设置下面这段代码**
    ```
    //在宿主Activity中设置代码如下
    @Override
    protected void onStop() {
        super.onStop();
        VideoPlayerManager.instance().releaseVideoPlayer();
    }
    
    @Override
    public void onBackPressed() {
        if (VideoPlayerManager.instance().onBackPressed()) return;
        super.onBackPressed();
    }
    
    //--------------------------------------------------
    
    //在此Fragment中设置代码如下
    @Override
    public void onStop() {
        super.onStop();
        VideoPlayerManager.instance().releaseVideoPlayer();
    }
    ```


#### 2.5 注意问题
##### 2.5.1如果是全屏播放，则需要在清单文件中设置当前activity的属性值**
- android:configChanges 保证了在全屏的时候横竖屏切换不会执行Activity的相关生命周期，打断视频的播放
- android:screenOrientation 固定了屏幕的初始方向
- 这两个变量控制全屏后和退出全屏的屏幕方向
    ```
        <activity android:name=".ui.test2.TestMyActivity"
            android:configChanges="orientation|keyboardHidden|screenSize"
            android:screenOrientation="portrait"/>
    ```


##### 2.5.2 关于设置日志是否打印
- 如下所示
    ```
    if(BuildConfig.DEBUG){
        VideoLogUtil.setIsLog(true);
    }else {
        VideoLogUtil.setIsLog(false);
    }
    ```



### 4.文档wiki说明[待更新，待完善]
- [Home]()
- [基础方法说明](https://github.com/yangchong211/YCVideoPlayer/blob/master/read/wiki1.md)
    - 01.最简单的播放
    - 02.竖屏全屏播放
    - 03.横屏全屏播放
    - 04.小窗口播放
    - 05.全屏播放切换视频清晰度
    - 06.在列表中播放
    - 07.在activity播放视频处理home键逻辑
    - 08.在fragment中播放
    - 09.显示视频top[分享，下载，更多按钮控件]
    - 10.全局悬浮播放视频
    - 11.常见api说明
- [视频优化处理](https://github.com/yangchong211/YCVideoPlayer/blob/master/read/wiki2.md)
    - 01.播放加载优化
    - 02.前后台切换优化
    - 03.视频播放异常优化
    - 04.视频播放颤动优化
    - 05.视频解码优化
    - 06.SeekTo设置优化
    - 07.关于so库优化
    - 08.关于网络状态监听优化
    - 09.关于代码规范优化
    - 10.关于布局优化
    - 11.选择SurfaceView还是TextureView
- [视频全局悬浮窗播放]()
- [视频封装思路]()
- [视频问题处理]()
- [音视频博客学习]()
- [边播边缓存]()
- [详细ReadMe，原文档](https://github.com/yangchong211/YCVideoPlayer/blob/master/read/README.md)



### 5.运行的效果展示
![image](http://p2mqszpjf.bkt.clouddn.com/ycVideoPlayer2.png)
![image](http://p0u62g00n.bkt.clouddn.com/Screenshot_2018-01-05-13-21-49.jpg)
![image](http://p2mqszpjf.bkt.clouddn.com/Screenshot_2018-01-16-11-22-43.jpg)
![image](http://p2mqszpjf.bkt.clouddn.com/Screenshot_2018-01-16-11-24-31.jpg)
![image](http://p2mqszpjf.bkt.clouddn.com/Screenshot_20180116-113446.png)
![image](http://p2mqszpjf.bkt.clouddn.com/Screenshot_20180116-113706.png)
![image](http://p2mqszpjf.bkt.clouddn.com/Screenshot_20180116-113721.png)
![image](http://p2mqszpjf.bkt.clouddn.com/Screenshot_20180116-113732.png)
![image](http://p2mqszpjf.bkt.clouddn.com/Screenshot_20180116-113802.png)
![image](http://p2mqszpjf.bkt.clouddn.com/Screenshot_20180116-113840.png)
![image](http://p2mqszpjf.bkt.clouddn.com/Screenshot_20180116-135824.png)
![image](https://upload-images.jianshu.io/upload_images/4432347-c2b61a83c1aaecba.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image](https://upload-images.jianshu.io/upload_images/4432347-f4776dfc42c94ebd.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image](https://upload-images.jianshu.io/upload_images/4432347-1b5870de5a3d3318.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


















```







