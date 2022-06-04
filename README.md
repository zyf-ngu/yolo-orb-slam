# yolo-orb-slam
semantics mapping and navigation
Prerequisites
Pangolin
git clone -b v0.5 https://
https://blog.csdn.net/Robert_Q/article/details/121690089
OpenCV
https://blog.csdn.net/qq_20373723/article/details/119328559
Eigen3
DBoW2 and g2o (Included in Thirdparty folder)

We use modified versions of the DBoW2 library to perform place recognition and g2o library to perform non-linear optimizations. Both modified libraries (which are BSD) are included in the Thirdparty folder.
ORB-SLAM3
https://blog.csdn.net/BigHandsome2020/article/details/123458612#t6

发现源码里没有euroc_examples.sh文件
https://github.com/electech6/ORB_SLAM3_detailed_comments

ORB-slam2编译时报错‘usleep’ was not declared in this scope
根据报错信息在文件添加
include<unistd.h>

编译会产生关于opencv的错误，类似"FATAL_ERROR "OpenCV > 2.4.3 not found."的错误

解决办法：
①修改cmakelist.txt，将opencv3.0改为4.2，我遇到两个地方，一个是orbslam2文件夹，另一个好像是DBoW2文件夹，可以根据错误信息查看。
https://blog.csdn.net/weixin_42584917/article/details/111308873

错误 ‘CV_LOAD_IMAGE_UNCHANGED’ was not declared in this scope
cv::IMREAD_UNCHANGED
