---
title: 低占用速度快可私有部署的离线版 Google 翻译
published: 2026-06-22
description: 这是文章的简短描述
image: ./cover.jpg
tags: [前端, 开发]
category: 前端开发
draft: false
---
# 低占用速度快可私有部署的离线版 Google 翻译
- [https://github.com/xxnuo/MTranServer?tab=readme-ov-file](https://github.com/xxnuo/MTranServer?tab=readme-ov-file)
## Repository files navigation

- ![](assets/image-20250704234731-t29b1sb.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#README](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#)
- ![](assets/image-20250704234731-dk9cdci.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#Apache-2.0 license](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#)

## MTranServer

![](assets/image-20250704234731-10tmyqe.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#mtranserver](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#mtranserver)

> 迷你翻译服务器 测试版 ⭐️ 给我个 Star 吧

‍

一个超低资源消耗超快的离线翻译服务器，英译中模型仅需 300MiB 内存即可运行，无需显卡。单个请求平均响应时间 50ms。支持全世界主要语言的翻译。翻译质量与 Google 翻译相当。

注意本模型专注于速度和多种设备私有部署，所以翻译质量肯定是不如大模型翻译的效果。

需要高质量的翻译建议使用在线大模型 API。

## Demo

![](assets/image-20250704234731-cdurq9f.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#demo](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#demo)

> 暂无，看预览图

![](https://github.com/xxnuo/MTranServer/raw/main/images/preview.png)

## 同类项目效果(CPU,英译中)

![](assets/image-20250704234731-brn7mba.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#%E5%90%8C%E7%B1%BB%E9%A1%B9%E7%9B%AE%E6%95%88%E6%9E%9Ccpu%E8%8B%B1%E8%AF%91%E4%B8%AD](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#%E5%90%8C%E7%B1%BB%E9%A1%B9%E7%9B%AE%E6%95%88%E6%9E%9Ccpu%E8%8B%B1%E8%AF%91%E4%B8%AD)

|项目名称|内存占用|并发性能|翻译效果|速度|其他信息|
| -------------------| --------| --------| --------| ----| ------------------------------------------------------|
|[facebook/nllb](https://github.com/facebookresearch/fairseq/tree/nllb)|很高|差|一般|慢|Android 移植版的 [RTranslator](https://github.com/niedev/RTranslator) 有很多优化，但占用仍然高，速度也不快|
|[LibreTranslate](https://github.com/LibreTranslate/LibreTranslate)|很高|一般|一般|中等|中端 CPU 每秒处理 3 句，高端 CPU 每秒处理 15-20 句。[详情](https://community.libretranslate.com/t/performance-benchmark-data/486)|
|[OPUS-MT](https://github.com/OpenNMT/CTranslate2#benchmarks)|高|一般|略差|快|[性能测试](https://github.com/OpenNMT/CTranslate2#benchmarks)|
|其他大模型|超高|动态|好好|很慢|32B 及以上参数的模型效果不错，但是对硬件要求很高|
|MTranServer(本项目)|低|高|一般|极快|单个请求平均响应时间 50ms|

> 现有的 Transformer 架构的大模型的小参数量化版本不在考虑范围，因为实际调研使用发现翻译质量很不稳定且会乱翻，幻觉严重，速度也不快。 出了性能更优的 Diffusion 架构的语言模型，再测试。
>
> 表中数据仅供参考，非严格测试，非量化版本对比。

## 更新日志

![](assets/image-20250704234731-xj6ve9a.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#%E6%9B%B4%E6%96%B0%E6%97%A5%E5%BF%97](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#%E6%9B%B4%E6%96%B0%E6%97%A5%E5%BF%97)

2025.03.22 v2.0.1 -\> v2.0.2

- 适配了 AMD64 全系架构，现在支持所有架构的 x86-64 CPU 部署

2025.03.21 v1.1.0 -\> v2.0.1

- 适配 ARM 架构
- 更新底层框架
- 更新模型

2025.03.08 v1.0.4 -\> v1.1.0

- 修复了内存溢出问题, 现在运行一个英译中模型仅需 800M+ 内存, 其他语言模型的内存占用也大幅降低
- 适配添加了多种插件的接口

## 桌面端 Docker 一键包

![](assets/image-20250704234731-g02kegl.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#%E6%A1%8C%E9%9D%A2%E7%AB%AF-docker-%E4%B8%80%E9%94%AE%E5%8C%85](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#%E6%A1%8C%E9%9D%A2%E7%AB%AF-docker-%E4%B8%80%E9%94%AE%E5%8C%85)

> 桌面端一键包部署需要安装 `Docker Desktop`，请自行安装。
>
> Windows、Mac 的 Docker Desktop 内存分配机制会给虚拟机分配比较多的内存，是正常的。Linux 服务器则是正常占用。

确保个人电脑上安装有 `Docker Desktop` 后，下载桌面端一键包

[中国大陆一键包下载地址](https://ocn4e4onws23.feishu.cn/drive/folder/QN1SfG7QeliVWGdDJ8Dce2sUnkf)

[国际一键包下载地址](https://github.com/xxnuo/MTranServer/releases/tag/onekey)

​`解压` ​到任意英文目录，文件夹结构示意图如下：

```notranslate
mtranserver/
├── compose.yml
├── models/
│   ├── enzh
│   │   ├── lex.50.50.enzh.s2t.bin
│   │   ├── model.enzh.intgemm.alphas.bin
│   │   └── vocab.enzh.spm
```

![](assets/image-20250704234731-5vj901l.svg)![](assets/image-20250704234731-rkc5nov.svg)

> 若你位于中国大陆，网络无法访问 Docker 下载镜像，请跳转到下文的 `1.3 可选步骤`。
>
> 一键包仅包含英译中模型，如果需要下载其他语言的模型，请跳转到下文的 `2. 下载模型`。

在 `mtranserver`​ 目录内打开命令行，然后直接跳转到下文的 `3. 启动服务`。

### 服务器 Docker Compose 部署

![](assets/image-20250704234731-syo5yzv.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#%E6%9C%8D%E5%8A%A1%E5%99%A8-docker-compose-%E9%83%A8%E7%BD%B2](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#%E6%9C%8D%E5%8A%A1%E5%99%A8-docker-compose-%E9%83%A8%E7%BD%B2)

#### 1.1 准备

![](assets/image-20250704234731-buwyuvg.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#11-%E5%87%86%E5%A4%87](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#11-%E5%87%86%E5%A4%87)

服务器准备一个存放配置的文件夹，打开终端执行以下命令

```shell
mkdir mtranserver
cd mtranserver
touch compose.yml
mkdir models


      
      
    
  
```

#### 1.2 用编辑器打开 `compose.yml` 文件，写入以下内容

![](assets/image-20250704234731-8imqjtm.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#12-%E7%94%A8%E7%BC%96%E8%BE%91%E5%99%A8%E6%89%93%E5%BC%80-composeyml-%E6%96%87%E4%BB%B6%E5%86%99%E5%85%A5%E4%BB%A5%E4%B8%8B%E5%86%85%E5%AE%B9](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#12-%E7%94%A8%E7%BC%96%E8%BE%91%E5%99%A8%E6%89%93%E5%BC%80-composeyml-%E6%96%87%E4%BB%B6%E5%86%99%E5%85%A5%E4%BB%A5%E4%B8%8B%E5%86%85%E5%AE%B9)

> 1. 修改下面的 `your_token`​ 为你自己设置的一个密码，使用英文大小写和数字。自己内网可以不设置，如果是 `云服务器` ​强烈建议设置一个密码，保护服务以免被 `扫到、攻击、滥用`。
> 2. 如果需要更改端口，修改 `ports`​ 的值，比如修改为 `9999:8989` 表示将服务端口映射到本机 9999 端口。

```yaml
services:
  mtranserver:
    image: xxnuo/mtranserver:latest
    container_name: mtranserver
    restart: unless-stopped
    ports:
      - "8989:8989"
    volumes:
      - ./models:/app/models
    environment:
      - CORE_API_TOKEN=your_token
      - CORE_NUM_WORKERS=1


      
      
    
  
```

#### 1.3 可选步骤

![](assets/image-20250704234731-1rs14wm.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#13-%E5%8F%AF%E9%80%89%E6%AD%A5%E9%AA%A4](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#13-%E5%8F%AF%E9%80%89%E6%AD%A5%E9%AA%A4)

若你的机器在中国大陆无法正常联网下载镜像，可以按如下操作导入镜像

[中国大陆 Docker 镜像下载](https://ocn4e4onws23.feishu.cn/drive/folder/PSUHfwmKPlu6PodAniVcNEPgnCb)

选择最新版的镜像 `mtranserver.image.tar` 下载保存到运行 Docker 的机器上。

进入下载到的目录打开终端，执行如下命令导入镜像

```shell
docker load -i mtranserver.image.tar


      
      
    
  
```

然后正常继续下一步下载模型

### 2. 下载模型

![](assets/image-20250704234731-4lgshq9.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#2-%E4%B8%8B%E8%BD%BD%E6%A8%A1%E5%9E%8B](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#2-%E4%B8%8B%E8%BD%BD%E6%A8%A1%E5%9E%8B)

> 持续更新模型中，如果没有你需要的语言模型，可以联系我添加。

[中国大陆模型镜像下载地址](https://ocn4e4onws23.feishu.cn/drive/folder/C3kffkLr8lxdtid5GYicAcFAnTh)

[国际下载地址](https://github.com/xxnuo/MTranServer/releases/tag/models)

下载模型后，`解压` ​每个语言的压缩包到 `models` 文件夹内。

> 警告：如果使用多个模型，内存占用会成倍增加，请根据自己服务器配置选择合适的模型。

下载了英译中模型的当前文件夹结构示意图：

```notranslate
compose.yml
models/
├── enzh
│   ├── lex.50.50.enzh.s2t.bin
│   ├── model.enzh.intgemm.alphas.bin
│   └── vocab.enzh.spm
```

![](assets/image-20250704234731-fircxvr.svg)![](assets/image-20250704234731-35xdgcy.svg)

如果你下载添加多个模型，这是有中译英、英译中模型文件夹结构示意图：

```notranslate
compose.yml
models/
├── enzh
│   ├── lex.50.50.enzh.s2t.bin
│   ├── model.enzh.intgemm.alphas.bin
│   └── vocab.enzh.spm
├── zhen
│   ├── lex.50.50.zhen.t2s.bin
│   ├── model.zhen.intgemm.alphas.bin
│   └── vocab.zhen.spm
```

![](assets/image-20250704234731-gb0airb.svg)![](assets/image-20250704234731-f6hr1c1.svg)

注意：例如中译日的过程是先中译英，再英译日，也就是需要两个模型 `zhen`​ 和 `enja`。其他语言翻译过程类似。

### 3. 启动服务

![](assets/image-20250704234731-jqxmefc.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#3-%E5%90%AF%E5%8A%A8%E6%9C%8D%E5%8A%A1](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#3-%E5%90%AF%E5%8A%A8%E6%9C%8D%E5%8A%A1)

先启动测试，确保模型位置没放错、能正常启动加载模型、端口没被占用。

```shell
docker compose up


      
      
    
  
```

正常输出示例：

```notranslate
[+] Running 2/2
 ✔ Network sample_default  Created  0.1s
 ✔ Container mtranserver   Created  0.1s
Attaching to mtranserver
mtranserver  | (2025-03-03 12:49:24) [INFO    ] Using maximum available worker count: 16
mtranserver  | (2025-03-03 12:49:24) [INFO    ] Starting Translation Service
mtranserver  | (2025-03-03 12:49:24) [INFO    ] Service port: 8989
mtranserver  | (2025-03-03 12:49:24) [INFO    ] Worker threads: 16
mtranserver  | Successfully loaded model for language pair: enzh
mtranserver  | (2025-03-03 12:49:24) [INFO    ] Models loaded.
mtranserver  | (2025-03-03 12:49:24) [INFO    ] Using default max parallel translations: 32
mtranserver  | (2025-03-03 12:49:24) [INFO    ] Max parallel translations: 32
```

![](assets/image-20250704234731-n4gzngj.svg)![](assets/image-20250704234731-ipm5y99.svg)

然后按 `Ctrl+C` 停止服务运行，然后正式启动服务器

```shell
docker compose up -d


      
      
    
  
```

这时候服务器就在后台运行了。

### 4. 使用

![](assets/image-20250704234731-4hi0kds.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#4-%E4%BD%BF%E7%94%A8](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#4-%E4%BD%BF%E7%94%A8)

下面表格内的 `localhost` 可以替换为你的服务器地址或 Docker 容器名。

下面表格内的 `8989`​ 端口可以替换为你在 `compose.yml` 文件中设置的端口值。

如果未设置 `CORE_API_TOKEN`​ 或者设置为空，翻译插件使用 `无密码` ​的 API。

如果设置了 `CORE_API_TOKEN`​，翻译插件使用 `有密码` ​的 API。

下面表格中的 `your_token`​ 替换为你在 `config.ini`​ 文件中设置的 `CORE_API_TOKEN` 值。

#### 翻译插件接口：

![](assets/image-20250704234731-937x934.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#%E7%BF%BB%E8%AF%91%E6%8F%92%E4%BB%B6%E6%8E%A5%E5%8F%A3](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#%E7%BF%BB%E8%AF%91%E6%8F%92%E4%BB%B6%E6%8E%A5%E5%8F%A3)

> 注：
>
> - [沉浸式翻译](https://immersivetranslate.com/zh-Hans/docs/services/custom/) 在 `设置` ​页面，开发者模式中启用 `Beta` ​特性，即可在 `翻译服务` ​中看到 `自定义 API 设置`​([官方图文教程](https://immersivetranslate.com/zh-Hans/docs/services/custom/))。然后将 `自定义 API 设置` ​的 `每秒最大请求数` ​拉高以充分发挥服务器性能准备体验飞一般的感觉。我设置的是 `每秒最大请求数` ​为 `5000`​，`每次请求最大段落数` ​为 `10`。你可以根据自己服务器配置设置。
> - [简约翻译](https://github.com/fishjar/kiss-translator) 在 `设置` ​页面，接口设置中滚动到下面，即可看到自定义接口 `Custom`​。同理，设置 `最大请求并发数量`​、`每次请求间隔时间` ​以充分发挥服务器性能。我设置的是 `最大请求并发数量` ​为 `100`​，`每次请求间隔时间` ​为 `1`。你可以根据自己服务器配置设置。
>
> 接下来按下表的设置方法设置插件的自定义接口地址。注意第一次请求会慢一些，因为需要加载模型。以后的请求会很快。

|名称|URL|插件设置|
| --------------------------| ----| -----------------------------------------|
|沉浸式翻译无密码|​`http://localhost:8989/imme`|​`自定义API 设置`​-`API URL`|
|沉浸式翻译有密码|​`http://localhost:8989/imme?token=your_token`|同上，需要更改 URL 尾部的 `your_token` ​为你的 `CORE_API_TOKEN` ​值|
|简约翻译无密码|​`http://localhost:8989/kiss`|​`接口设置`​-`Custom`​-`URL`|
|简约翻译有密码|​`http://localhost:8989/kiss`|同上，需要 `KEY` ​填 `your_token`|
|划词翻译自定义翻译源无密码|​`http://localhost:8989/hcfy`|​`设置`​-`其他`​-`自定义翻译源`​-`接口地址`|
|划词翻译自定义翻译源有密码|​`http://localhost:8989/hcfy?token=your_token`|​`设置`​-`其他`​-`自定义翻译源`​-`接口地址`|

**普通用户参照表格内容设置好插件使用的接口地址就可以使用了。**

### 5. 保持更新

![](assets/image-20250704234731-lz9ljrl.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#5-%E4%BF%9D%E6%8C%81%E6%9B%B4%E6%96%B0](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#5-%E4%BF%9D%E6%8C%81%E6%9B%B4%E6%96%B0)

目前是测试版服务器和模型，可能会遇到问题，建议经常保持更新

从上文地址下载新模型，解压覆盖到原 `models` 模型文件夹

然后更新重启服务器：

```shell
docker compose down
docker pull xxnuo/mtranserver:latest
docker compose up -d


      
      
    
  
```

> 国内用户若无法正常 `pull`​ 镜像，按照 `1.3 可选步骤` 手动下载新镜像导入即可。

### 开发者接口：

![](assets/image-20250704234731-nm3s0fc.svg)[https://github.com/xxnuo/MTranServer?tab=readme-ov-file#%E5%BC%80%E5%8F%91%E8%80%85%E6%8E%A5%E5%8F%A3](https://github.com/xxnuo/MTranServer?tab=readme-ov-file#%E5%BC%80%E5%8F%91%E8%80%85%E6%8E%A5%E5%8F%A3)

> Base URL: `http://localhost:8989`

|名称|URL|请求格式|返回格式|认证头|
| ------------------| ----| --------| --------| -------------------------|
|服务版本|​`/version`|无|​`{"version": "v1.1.0"}`|无|
|语言对列表|​`/models`|无|​`{"models":["zhen","enzh"]}`|Authorization: your\_token|
|普通翻译接口|​`/translate`|​`{"from": "en", "to": "zh", "text": "Hello, world!"}`|​`{"result": "你好，世界！"}`|Authorization: your\_token|
|批量翻译接口|​`/translate/batch`|​`{"from": "en", "to": "zh", "texts": ["Hello, world!", "Hello, world!"]}`|​`{"results": ["你好，世界！", "你好，世界！"]}`|Authorization: your\_token|
|健康检查|​`/health`|无|​`{"status": "ok"}`|无|
|心跳检查|​`/__heartbeat__`|无|​`Ready`|无|
|负载均衡心跳检查|​`/__lbheartbeat__`|无|​`Ready`|无|
|谷歌翻译兼容接口 1|​`/language/translate/v2`|​`{"q": "The Great Pyramid of Giza", "source": "en", "target": "zh", "format": "text"}`|​`{"data": {"translations": [{"translatedText": "吉萨大金字塔"}]}}`|Authorization: your\_token|
