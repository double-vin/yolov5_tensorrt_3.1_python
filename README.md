移步：https://github.com/double-vin/yolov5-3.1_tensorrt_python

## How to Run

1. 环境配置：https://blog.csdn.net/weixin_50008473/article/details/115250986?spm=1001.2014.3001.5501
2. 从 .pt文件生成 .wts 文件(以yolov5x.pt为例)

```
git clone https://github.com/ultralytics/yolov5.git
git clone https://github.com/wang-xinyu/tensorrtx.git
cp tensorrtx/yolov5/gen_wts.py yolov5
cd yolov5
python gen_wts.py yolov5x.pt
```

3. 修改CMakeLists.txt

```
# cuda
include_directories(/usr/local/cuda-11.1/include)
link_directories(/usr/local/cuda-11.1/lib64)
# tensorrt
include_directories(/usr/include/x86_64-linux-gnu/)
link_directories(/usr/lib/x86_64-linux-gnu/)
```

4. 修改tensorrtx/yolov5/yolov5.cpp和yololayer.h

```
# 修改为自己需要的模型
#define NET s // s m l x
# 修改为模型对应的类别数
static constexpr int CLASS_NUM = 80
```

5. 编译运行

```
cd tensorrtx/yolov5/
mkdir samples
mkdir build && cd build
cp yolov5/yolov5x.wts build
cmake ..
make
sudo ./yolov5 -s 
sudo ./yolov5 -d  ../samples

# python接口
python yolov5_trt.py
```

6. 新增utils/tools.py

7. 新增infer.py：图片、本地视频和rtsp推理加速

```
python infer.py
# infer_images_videos_rtsps("./inference/videos") 配置图片、本地视频和rtsp路径
```


