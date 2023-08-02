使用 OpenCV 和 MediaPipe 进行剪刀、石头、布手势的识别

MediaPipe是一个用于构建机器学习管道的框架，用于处理视频、音频等时间序列数据。这个跨平台框架适用于桌面/服务器、Android、iOS和嵌入式设备，如Raspberry Pi和Jetson Nano。
MediaPipe具有强大的功能，主要包括如下：
![1690947782434](https://github.com/kings802/python-finger_gesture/assets/19601216/45e58b80-2bee-484e-a661-81ffb72a5ea3)

在手势识别方面，
在对整个图像进行手掌检测后，我们后续的手部地标模型通过回归对检测到的手部区域内的 21 个 3D 手指关节坐标进行精确的关键点定位，即直接坐标预测。该模型学习一致的内部手部姿势表示，并且即使对于部分可见的手和自遮挡也具有鲁棒性。
为了获得地面真实数据，我们用 21 个 3D 坐标手动注释了约 30K 个真实世界图像，如下所示（我们从图像深度图中获取 Z 值，如果每个相应坐标存在的话）。为了更好地覆盖可能的手部姿势并对手部几何形状的性质提供额外的监督，我们还在各种背景上渲染高质量的合成手部模型，并将其映射到相应的 3D 坐标。
来源：MediaPipe Hands Solutions（https://developers.google.com/mediapipe/solutions/vision/hand_landmarker）
![hand_landmarks_docs](https://github.com/kings802/python-finger_gesture/assets/19601216/637d33bd-cf6a-4dbf-9ff1-75a7d5a99ef5)

本文的关键步骤：
1.利用OpenCV获取手势图像
2.使用MediaPipe检测手部的21个关键点位置
3.利用5个手指的质检的关节弯曲的夹角构建5个关键特征
4.抓取图像，构造特征值，形成3中手势的训练样本和测试样本。
5.使用随机森林的有监督分类方法进行训练
6.基于训练好的随机森林模型就行实时图像的手势识别
