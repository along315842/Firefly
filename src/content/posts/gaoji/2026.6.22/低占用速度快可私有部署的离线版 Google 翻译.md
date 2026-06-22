---
title: 低占用速度快可私有部署的离线版 Google 翻译
published: 2026-06-22
description: MTranServer 是一个超低资源消耗的离线翻译服务器，英译中模型仅需 300MiB 内存，单请求平均响应 50ms，翻译质量与 Google 翻译相当，支持 Docker 私有化部署。
tags: [翻译, Docker, 私有部署, 开源工具]
category: 实用工具
---

> 项目地址：[https://github.com/xxnuo/MTranServer](https://github.com/xxnuo/MTranServer)

## MTranServer 简介

一个超低资源消耗、超快速度的离线翻译服务器，英译中模型仅需 300MiB 内存即可运行，无需显卡。单个请求平均响应时间 50ms，支持全世界主要语言的翻译，翻译质量与 Google 翻译相当。

> 注意：本模型专注于速度和多设备私有部署，翻译质量不如大模型。需要高质量翻译建议使用在线大模型 API。

## 预览

![预览图](https://github.com/xxnuo/MTranServer/raw/main/images/preview.png)

## 同类项目效果对比（CPU，英译中）

| 项目名称 | 内存占用 | 并发性能 | 翻译效果 | 速度 | 其他信息 |
| --- | --- | --- | --- | --- | --- |
| [facebook/nllb](https://github.com/facebookresearch/fairseq/tree/nllb) | 很高 | 差 | 一般 | 慢 | Android 移植版 [RTranslator](https://github.com/niedev/RTranslator) 有优化，但占用仍高、速度不快 |
| [LibreTranslate](https://github.com/LibreTranslate/LibreTranslate) | 很高 | 一般 | 一般 | 中等 | 中端 CPU 每秒处理 3 句，高端 CPU 每秒处理 15-20 句。[详情](https://community.libretranslate.com/t/performance-benchmark-data/486) |
| [OPUS-MT](https://github.com/OpenNMT/CTranslate2#benchmarks) | 高 | 一般 | 略差 | 快 | [性能测试](https://github.com/OpenNMT/CTranslate2#benchmarks) |
| 其他大模型 | 超高 | 动态 | 好 | 很慢 | 32B 及以上参数效果不错，但对硬件要求很高 |
| **MTranServer（本项目）** | **低** | **高** | **一般** | **极快** | 单个请求平均响应时间 50ms |

> 现有 Transformer 架构大模型的小参数量化版本不在考虑范围，实际调研发现翻译质量很不稳定，会乱翻，幻觉严重，速度也不快。待出现性能更优的 Diffusion 架构语言模型后再行测试。
>
> 表中数据仅供参考，非严格测试，非量化版本对比。

## 更新日志

**2025.03.22** `v2.0.1` → `v2.0.2`

- 适配了 AMD64 全系架构，现在支持所有架构的 x86-64 CPU 部署

**2025.03.21** `v1.1.0` → `v2.0.1`

- 适配 ARM 架构
- 更新底层框架
- 更新模型

**2025.03.08** `v1.0.4` → `v1.1.0`

- 修复了内存溢出问题，现在运行英译中模型仅需 800M+ 内存，其他语言模型内存占用也大幅降低
- 适配添加了多种插件的接口

---

## 部署指南

### 方式一：桌面端 Docker 一键包

> 桌面端一键包部署需要预先安装 `Docker Desktop`。
>
> Windows、Mac 的 Docker Desktop 内存分配机制会给虚拟机分配较多内存，属正常现象。Linux 服务器则正常占用。

确保安装有 `Docker Desktop` 后，下载桌面端一键包：

- [中国大陆一键包下载地址](https://ocn4e4onws23.feishu.cn/drive/folder/QN1SfG7QeliVWGdDJ8Dce2sUnkf)
- [国际一键包下载地址](https://github.com/xxnuo/MTranServer/releases/tag/onekey)

解压到任意**英文路径**目录，文件夹结构如下：

```
mtranserver/
├── compose.yml
├── models/
│   └── enzh/
│       ├── lex.50.50.enzh.s2t.bin
│       ├── model.enzh.intgemm.alphas.bin
│       └── vocab.enzh.spm
```

> 若位于中国大陆、网络无法访问 Docker 下载镜像，请参阅下文 [1.3 可选步骤](#13-可选步骤)。
>
> 一键包仅包含英译中模型，如需其他语言模型，请参阅下文 [2. 下载模型](#2-下载模型)。

在 `mtranserver` 目录内打开命令行，然后直接跳转到 [3. 启动服务](#3-启动服务)。

---

### 方式二：服务器 Docker Compose 部署

#### 1.1 准备

服务器准备一个存放配置的文件夹，打开终端执行以下命令：

```shell
mkdir mtranserver
cd mtranserver
touch compose.yml
mkdir models
```

#### 1.2 编写 compose.yml

用编辑器打开 `compose.yml` 文件，写入以下内容：

> 1. 将 `your_token` 替换为自己设置的密码（英文大小写和数字）。内网可不设置，**云服务器强烈建议设置**，防止被扫描、攻击或滥用。
> 2. 如需更改端口，修改 `ports` 的值，例如 `9999:8989` 表示将服务映射到本机 9999 端口。

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

若机器在中国大陆无法正常联网下载镜像，可按如下方式手动导入：

1. 前往 [中国大陆 Docker 镜像下载](https://ocn4e4onws23.feishu.cn/drive/folder/PSUHfwmKPlu6PodAniVcNEPgnCb)，下载最新版 `mtranserver.image.tar`。
2. 进入下载目录，执行以下命令导入镜像：

```shell
docker load -i mtranserver.image.tar
```

然后继续下一步下载模型。

---

### 2. 下载模型

> 持续更新模型中，如果没有你需要的语言模型，可以联系作者添加。

- [中国大陆模型镜像下载地址](https://ocn4e4onws23.feishu.cn/drive/folder/C3kffkLr8lxdtid5GYicAcFAnTh)
- [国际下载地址](https://github.com/xxnuo/MTranServer/releases/tag/models)

下载后，将每个语言的压缩包**解压**到 `models` 文件夹内。

> ⚠️ 警告：使用多个模型时，内存占用会成倍增加，请根据服务器配置选择合适的模型数量。

仅含英译中模型的目录结构：

```
compose.yml
models/
└── enzh/
    ├── lex.50.50.enzh.s2t.bin
    ├── model.enzh.intgemm.alphas.bin
    └── vocab.enzh.spm
```

同时含中译英、英译中模型的目录结构：

```
compose.yml
models/
├── enzh/
│   ├── lex.50.50.enzh.s2t.bin
│   ├── model.enzh.intgemm.alphas.bin
│   └── vocab.enzh.spm
└── zhen/
    ├── lex.50.50.zhen.t2s.bin
    ├── model.zhen.intgemm.alphas.bin
    └── vocab.zhen.spm
```

> 注意：中译日的过程是先中译英、再英译日，即需要 `zhen` 和 `enja` 两个模型。其他语言翻译过程类似。

---

### 3. 启动服务

先前台启动测试，确认模型路径正确、能正常加载、端口未被占用：

```shell
docker compose up
```

正常启动输出示例：

```
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

按 `Ctrl+C` 停止后，正式后台启动服务：

```shell
docker compose up -d
```

---

### 4. 配置翻译插件

下表中的 `localhost` 可替换为你的服务器地址或 Docker 容器名，`8989` 端口可替换为 `compose.yml` 中设置的端口值。

- 未设置 `CORE_API_TOKEN` 或设置为空 → 使用**无密码** API
- 已设置 `CORE_API_TOKEN` → 使用**有密码** API（将表中 `your_token` 替换为实际值）

> **使用提示：**
>
> - **沉浸式翻译**：在`设置`页面开启开发者模式中的 `Beta` 特性，即可在`翻译服务`中看到`自定义 API 设置`（[官方图文教程](https://immersivetranslate.com/zh-Hans/docs/services/custom/)）。建议将`每秒最大请求数`拉高（推荐 `5000`），`每次请求最大段落数`设为 `10`，以充分发挥服务器性能。
> - **简约翻译**：在`设置`页面，接口设置中滚动到底部可见自定义接口 `Custom`。建议`最大请求并发数量`设为 `100`，`每次请求间隔时间`设为 `1`。

| 名称 | URL | 插件设置位置 |
| --- | --- | --- |
| 沉浸式翻译（无密码） | `http://localhost:8989/imme` | `自定义API 设置` - `API URL` |
| 沉浸式翻译（有密码） | `http://localhost:8989/imme?token=your_token` | 同上，需将 URL 中 `your_token` 替换为实际值 |
| 简约翻译（无密码） | `http://localhost:8989/kiss` | `接口设置` - `Custom` - `URL` |
| 简约翻译（有密码） | `http://localhost:8989/kiss` | 同上，`KEY` 填入 `your_token` |
| 划词翻译（无密码） | `http://localhost:8989/hcfy` | `设置` - `其他` - `自定义翻译源` - `接口地址` |
| 划词翻译（有密码） | `http://localhost:8989/hcfy?token=your_token` | 同上 |

**普通用户按表格配置好插件接口地址即可开始使用。**

---

### 5. 保持更新

目前仍为测试版，建议定期更新以获取最新模型和修复：

1. 从上文地址下载新模型，解压覆盖到原 `models` 文件夹
2. 更新并重启服务器：

```shell
docker compose down
docker pull xxnuo/mtranserver:latest
docker compose up -d
```

> 国内用户若无法正常 `pull` 镜像，按照 [1.3 可选步骤](#13-可选步骤) 手动下载新镜像导入即可。

---

## 开发者接口

> Base URL: `http://localhost:8989`

| 名称 | URL | 请求格式 | 返回格式 | 认证头 |
| --- | --- | --- | --- | --- |
| 服务版本 | `/version` | 无 | `{"version": "v1.1.0"}` | 无 |
| 语言对列表 | `/models` | 无 | `{"models":["zhen","enzh"]}` | `Authorization: your_token` |
| 普通翻译接口 | `/translate` | `{"from": "en", "to": "zh", "text": "Hello, world!"}` | `{"result": "你好，世界！"}` | `Authorization: your_token` |
| 批量翻译接口 | `/translate/batch` | `{"from": "en", "to": "zh", "texts": ["Hello, world!"]}` | `{"results": ["你好，世界！"]}` | `Authorization: your_token` |
| 健康检查 | `/health` | 无 | `{"status": "ok"}` | 无 |
| 心跳检查 | `/__heartbeat__` | 无 | `Ready` | 无 |
| 负载均衡心跳检查 | `/__lbheartbeat__` | 无 | `Ready` | 无 |
| 谷歌翻译兼容接口 | `/language/translate/v2` | `{"q": "The Great Pyramid of Giza", "source": "en", "target": "zh", "format": "text"}` | `{"data": {"translations": [{"translatedText": "吉萨大金字塔"}]}}` | `Authorization: your_token` |
