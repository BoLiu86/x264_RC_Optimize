# x264_RC_Optimize
Face detect-based Rate Control for x264

基于人脸检测的x264码率控制算法优化

## History
- 2020/06/16  上传x264-snapshot-20191217-2245-stable作为baseline。
- 2020/07/07  读入待编码图像，完成逐帧下采样。由于目前仅针对IPP...P编码模式尽心RC优化，关闭x264的lookahead功能。
- 2020/07/22  利用U、V分量，逐像素判断编码图像中是否存在人脸。若存在并且像素数大于一定范围，则以MB为单位标记。
- 2020/07/28  优化检测算法，去除孤立的人脸标志。
- 2020/08/09  输出人脸检测结果
- 2020/08/18 使用每个MB的人脸检测结果判断是否使用AQ方法、更新Usages和实验结果  

## Usages
- Windows下，编译x264需要搭建MinGW和msys的环境。编译环境搭建好之后，可执行：**1)**`./configure --enable-shared` **2)**`make` **3)**`make install`生成可执行程序和动态库测试编码效果。
- Linux环境下，未测试。

## Datasets
采用JCT-VC公布的Class E中的测试序列，这些序列均为**会议场景**序列。Class E中的序列是[720p](https://pan.baidu.com/s/1qRX0TP2SfuRTLCqCJzzHdg)的，百度网盘提取码：iyhs，我是通过使用[FFmpeg](http://ffmpeg.org/)将其上采样到[1080p](pan.baidu.com)进行测试的。

## Test Condition and
- 测试条件，编码模式：IPP...P；RC方法：CVBR；码率：1024、1536、1792、2048。
--具体如下：```x264.exe --frames 600 --bitrate 1024 --vbv-bufsize 1024 --vbv-maxrate 1024 -o Johnny_1920x1080_60p_1024.264 Johnny_1920x1080_60p.yuv```

## Results
![Alt text](https://github.com/Ronater/x264_RC_Optimize/blob/master/face_res_new.png)


## References
[1]【x264历史版本】http://download.videolan.org/pub/videolan/x264/snapshots/
[2]【人脸检测理论】Kovac J , Peer P , Solina F . Human skin color clustering for face detection[C]// EUROCON 2003. Computer as a Tool. The IEEE Region 8. IEEE, 2003.
[3]【x264的RC理论】 https://blog.csdn.net/Ronater/article/details/105320592
