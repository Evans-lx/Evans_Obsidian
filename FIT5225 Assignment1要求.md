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

# 2 Web服务
你需要开发一个RESTful API，允许客户端将图像上传到服务器。你必须使用**Flask**构建你的Web服务，并使用1024以上的任意端口。你的Flask服务器应该能够同时处理多个客户端。每个图像应该通过HTTP POST请求发送到Web服务，其中包含一个带有唯一ID（例如UUID）和base64编码图像的JSON对象。由于图像是二进制数据，它不能直接插入到JSON中。你必须将图像转换为可以用作普通字符串的文本表示形式。将图像编码为文本的最常见方法是使用base64方法。用于发送图像的示例JSON请求可能如下所示：
```
{
"id":"06e8b9e0-8d2e-11eb-8dcd-0242ac130003",
"image":"YWRzZmFzZGZhc2RmYXNkZmFzZGYzNDM1MyA7aztqMjUzJyBqaDJsM2 ..."
}
```
Web服务为每个请求创建一个线程，并使用YOLO和OpenCV Python库检测图像中的对象。作为建议，你可以从JSON消息的图像编码部分开始，考虑开发你的Web服务，并使用基本的Postman HTTP请求对其进行测试。确认你的Web服务功能正常后，你可以按照WebService API创建客户端请求，使用Locust进行测试。对于每个图像（请求），你的Web服务将返回一个JSON对象，其中包含该图像中检测到的所有对象的列表，如下所示：
```
{
"id":"The id from the client request",
"objects": [
{
"label": "human/book/cat/...",
"accuracy": a real number between 0-1,
"rectangle": {
"height": number,
"left": number,
"top": number,
"width": number
}
}
...
]
}
```
“id”与客户端一起发送的相同ID与图像。这用于将异步响应与客户端请求关联起来。“label”表示检测到的对象类型，例如，猫，书籍等。“Accuracy”表示对象检测的精度，而矩形是一个JSON对象，显示图像中物体周围的框的位置。示例响应如下所示：
```
{
"id": "2b7082f5-d31a-54b7-a46e-5e4889bf69bd",
"objects": [
{
"label": "book",
"accuracy": 0.7890481352806091,
"rectangle": {"height": 114, "left": 380, "top": 363, "width": 254}
},
{
"label": "cat",
"accuracy": 0.6877481352806091,
"rectangle": {"height": 114, "left": 180, "top": 63, "width": 254}
}
]
}
```
你需要使用yolov3-tiny框架开发一个快速可靠的对象检测RESTful API。你将使用预训练的网络权重，因此不需要自己训练对象检测程序。我们已经在yolo_tiny_configs.zip文件中提供了yolov3-tiny配置文件和权重。请注意，此网络是在COCO数据集上进行训练的（<http://cocodataset.org/#home>）。我们还为你提供了来自该数据集的一组样本图像（128张图像，位于zip文件中的inputfolder文件夹中），你应该使用它们进行测试。

# 3 Dockerfile
Docker通过从名为Dockerfile的文件中读取指令来构建镜像。Dockerfile是一个文本文件，包含构建给定镜像所需的所有有序命令。你需要创建一个Dockerfile，其中包含构建Docker镜像所需的所有指令。你可以在这里找到Dockerfile的参考文档：<https://docs.docker.com/engine/reference/builder/>。
为了降低复杂性、依赖关系、文件大小和构建时间，请避免安装额外或不必要的软件包，即使它们可能是“好用的”。例如，你不需要在镜像中包含文本编辑器。优化Dockerfile并保持易于阅读和维护的重要性。

# 4 Kubernetes集群
你的任务是在OCI VM上安装和配置一个Kubernetes集群。为此，你将在OCI上安装K8s在三个VM实例上（你的所有VM实例应该是Intel机器，形状为VM.Standard.E4.Flex，8GB内存和4个OCPUs）。你需要设置一个具有1个控制器和2个运行在OCI VM上的工作节点的K8s集群。你需要在VM上安装Docker引擎。你应该使用Kubeadm配置你的K8s集群。
# 5 Kubernetes服务
当你有一个运行的Kubernetes集群后，你需要创建服务和部署配置，这将依次在集群中创建并部署所需的Pod。Kubernetes的官方文档包含了许多关于如何从Docker镜像创建Pod、设置CPU和/或内存限制以及创建使用选择器的部署的步骤。请确保为每个Pod设置CPU请求和CPU限制为“0.5”，内存请求和限制为“512MiB”。
最初，你将从一个单独的Pod开始测试你的Web服务，并根据第7节的描述逐渐增加数量。实现这一目标的首选方法是创建副本集并相应地扩展它们。
最后，你需要暴露你的部署，以便与Pod中运行的Web服务进行通信。你可以利用**Service和NodePort**来暴露你的部署。你将需要从下一节描述的各种位置调用对象检测服务。OCI通过其网络安全措施限制对你的VM的访问。因此，你应该确保你的控制器实例打开了所有必要的端口，并且必要的网络配置，包括OCI的“安全列表”，已经正确设置。你可能还需要在实例级防火墙上打开端口（如防火墙或iptables）。

# 6 Locust负载生成

# 7 实验和报告

# 8 视频录制