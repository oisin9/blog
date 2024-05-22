+++
title = "How to Use CloudFlare R2 as Pic Bed"
date = "2024-05-22T10:04:31+08:00"

#
# description is optional
#
# description = "An optional description for SEO. If not provided, an automatically created summary will be used."

tags = ["how-to"]
+++

## 配置Cloudflare R2

Cloudflare的R2慷慨的提供了免费的流量，很适合作为网站的图床来使用，下面就介绍一下如何使用Cloudflare来搭建图床，并搭配PicList来使用。

首先需要注册一个Cloudflare的账号，购买或转入一个域名。

在Cloudflare左侧的控制台中选择R2产品->概述，然后点击创建存储桶，这里桶名可以自己起一个，然后区域选择自动，填写完成后点击创建。

![](https://resource.public.freeoisin.com/pic/1f8568943a50c3e71554f398faf4567b.png)

创建完成后会自动跳到刚刚创建的存储桶界面，点击设置，找到自定义域，点击配置，然后给这个存储桶配置一个自定义域名（假设我们托管到Cloudflare上的域名是xxxx.com，那我们在这里可以填写abc.xxxx.com，这里的abc只是示例，可以自定义填写）

![](https://resource.public.freeoisin.com/pic/80730a7188203779ec27955e0d6677ef.png)

设置完自定义域名后，点击左侧控制栏的R2->概述，然后点击右侧的“管理R2 API令牌”，再点击“创建API令牌”

![](https://resource.public.freeoisin.com/pic/0b7257d3cf5790d0fa2b13a9db4fdb20.png)

填写令牌名称，权限选择“对象读和写”，指定存储桶中选择“仅应用与特定存储桶”，然后点击最下面的“创建API令牌”

创建API令牌后，会显示刚刚创建的API令牌相关信息，这里我们需要把下面三个值记下来，后续将无法查看：

![](https://resource.public.freeoisin.com/pic/a7e53d006692779b5b832002168a33f2.png)

## 配置PicList

打开PicList，设置->上传设置->勾选AWS S3

![](https://resource.public.freeoisin.com/pic/d9764a749b3d2b96932cb2a36cacc9ec.png)

点击图床->AWS S3，创建一个新配置，填写的内容如下：

- AccessKeyID -> 填写刚刚记下来的访问密钥ID
- SecretAccressKey -> 填写机密访问密钥
- 上传路径 -> {md5}.{extName}，这个可以根据实际需要进行调整
- 设定Region -> 除了欧盟区外，一律填写us-east-1
- 设定自定义节点 -> 为 S3 客户端使用管辖权地特定的终结点
- 设定自定义域名 -> 填写我们之前设置的自定义域名，如"https://abc.xxxx.com"
- 设定上传资源的访问策略 -> public-read

点击确定，在PicList上传界面里选择刚刚创建的配置即可正常上传，并使用自定义域名来访问图片资源。
