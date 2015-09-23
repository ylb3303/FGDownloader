# FGGDownloader
用于断点续传，退出程序后，下次启动后，恢复下载从上次下载位置开始下载
/*
![演示](file:///Users/xiaguifeng/Desktop/11.gif)
/*
FGGDownloader简介<br>
-----------------------------------------------------------------------------------------
基于UNSURLConnection封装的断点续传类，用于大文件下载，退出程序后，下次接着下载。<br>
用法简介：<br>
-->1.在项目中导入FGGDownloader.h头文件；<br>
-->2.搭建UI时，设置显示进度的UIProgressView的进度值:[FGGDownloader lastProgressWithUrl:],
这个方法的返回值是float类型的；<br>
设置显示文件大小/文件总大小的Label的文字：[FGGDownloader lastProgressWithUrl:]；<br>

-->3.开始或恢复下载任务的方法：downloadWithUrlString:(NSString *)urlString
toPath:(NSString *)destinationPath
process:(ProcessHandle)process
completion:(CompletionHandle)completion
failure:(FailureHandle)failure
这个方法包含三个回调代码块，分别是：<br>
1)下载过程中的回调代码块，带2个参数：下载进度参数progress，已下载文件大小sizeString；<br>
2)下载成功回调的代码块，没有参数；<br>
3)下载失败的回调代码块，带一个下载错误参数error。<br>

-->4.在下载出错的回调代码块中处理出错信息。在出错的回调代码块中或者暂停下载任务时，<br>
调用cancelDownloadTask:方法取消/暂停下载任务；<br>
-->5.AppDelegate的程序将要退出的applicationWillTerminate:方法中，
取消下载：cancelDownloading:。<br>
-----------------------------------------------------------------------------------------
注意：<br>
++若是单个下载任务，最好在视图控制器中将下载对象设置成成员变量：FGGDownloader *_downloader;<br>
++若有多个下载任务，最好在视图控制器中弄一个字典，存放下载对象，每次新建或者恢复下载时，将下载任务对象
以下载url为key存到这个字典中；在暂停下载或者下载出错时，根据下载url从字典中取出对应的下载对象，用
cancelDownloading:方法取消这个对象的下载，并从字典中移除这个键值对；<br>
++若有多个下载对象，在程序将要退出的方法中，应当结束所有的下载任务。<br>
=========================================================================================
Copyright (c) 2015年 夏桂峰. All rights reserved.
*/
