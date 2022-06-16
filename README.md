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

bash: python: command not found
软链接没弄。
ln -s /usr/bin/python3.8 /usr/bin/python
ln: failed to create symbolic link '/usr/bin/python': File exists
ln -sf /usr/bin/python3.9 /usr/bin/python


运行build-ros.sh时出现问题一:
[rosbuild] rospack found package "ORB_SLAM2" at "", but the current   directory is "/home/angelo/ORB_SLAM2/Examples/ROS/ORB_SLAM2".  You should   double-check your ROS_PACKAGE_PATH to ensure that packages are found in the   correct precedence order.
jia export lujing


error while loading shared libraries: libg2o_core.so: cannot open shared object file: No such file or directory解决方法
在build文件夹目录环境下输入：sudo ldconfig
然后编译就可以了。
因为g2o刚装,没生效。

下载associate.py，https://vision.in.tum.de/data/datasets/rgbd-dataset/tools放在数据集下，在数据集下打开一个终端执行以下命令生成：associations.txt
python associate.py rgb.txt depth.txt > associations.txt
AttributeError: 'dict_keys' object has no attribute 'remove'
将associate.py中第86行87行的
    first_keys = first_list.keys()
    second_keys = second_list.keys()
改为
    first_keys = list(first_list.keys())
    second_keys = list(second_list.keys())
    
pcl1.8.1 vtk7.1.1 qt5
https://blog.csdn.net/way7486chundan/article/details/110296785?utm_term=ubuntu16.04%E5%AE%89%E8%A3%85vtk7&utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~all~sobaiduweb~default-0-110296785-null-null&spm=3001.4430#t8

kdtree.so.1.8.0:undefined reference to `LZ4_decompress_safe_continue’
解决办法：
/pcl/build/kdtree/CMakeFiles/pcl_kdtree.dir/下的link.txt里在末尾写上：-llz4

报错#include <boost/uuid/sha1.hpp>undefined


#if (BOOST_VERSION >= 106600)
#include <boost/uuid/detail/sha1.hpp>
#else
#include <boost/uuid/sha1.hpp>
#endif

    报错内容：

error: no matching function for call to  
boost::uuids::random_generator_pure::random_generator_pure(boost::random::mt19937*

   

则更改
gedit /home/mjy/repo/pcl-1.8/pcl-master-1.8/pcl-master/outofcore/include/pcl/outofcore/impl/octree_disk_container.hpp

注释以下代码：

    //template<typename PointT>
    //boost::uuids::random_generator OutofcoreOctreeDiskContainer<PointT>::uuid_gen_ (&rand_gen_);
    
 报错/home/zyf/pcl-pcl-1.8.1/segmentation/include/pcl/segmentation/ground_plane_comparator.h:150:17: error: invalid initialization of reference of type ‘const std::vector<float>&’ from expression of type ‘const boost::shared_ptr<std::vector<float> >’
  150 |         return (plane_coeff_d_);

改为return (*plane_coeff_d_);

