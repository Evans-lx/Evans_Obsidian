# 1 概要与背景
该项目旨在构建一个名为CloudDetect的基于Web的系统。它将允许最终用户将图像发送到由Docker容器托管的Web服务，并接收到其上传图像中检测到的对象列表。该项目将利用YOLO（You Only Look Once）库，这是一种先进的实时目标检测系统，以及OpenCV（开源计算机视觉库）来执行所需的图像操作/转换。YOLO和OpenCV都是基于Python的开源计算机视觉和机器学习软件库。Web服务将作为容器托管在Kubernetes集群中。Kubernetes将用作容器编排系统。目标检测Web服务还设计为可以使用Python的Flask库的RESTful API。我们有兴趣通过改变发送到系统的请求数量（需求）和Kubernetes集群中现有Pod的数量（资源）来检查CloudDetect的性能，使用负载生成工具如Locust。

该任务具有以下目标：

- 编写一个Python **Web服务**，接受JSON对象格式的图像，使用YOLO和OpenCV处理图像，并返回一个包含检测到的对象列表的JSON对象。
- 为目标检测Web服务构建**Docker镜像**。
- 在Oracle Cloud Infrastructure（OCI）的虚拟机（实例）上创建**Kubernetes集群**。
- 部署一个**Kubernetes服务**，将入站请求分配到运行目标检测服务的Pod之间。
- 使用Loucust编写**负载生成**脚本。
- 在不同负载和Pod数量条件下**测试**系统。

您可以依次专注于这些目标，以获得部分分数。