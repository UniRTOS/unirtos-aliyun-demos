# unirtos_aliyun_demos

本仓库推荐通过 `unirtos-cli` 的 demo 工作流使用，以保证创建、环境拉取和编译流程一致。

## 功能描述

本 Demo 展示 UniRTOS 设备通过 MQTT 对接阿里云 IoT 平台的完整流程，适合作为云接入样例。

- 支持阿里云设备鉴权（clientId / username / password）
- 支持 MQTT 主题订阅与消息发布
- 支持 TLS 可选连接能力（可按配置启用）
- 采用异步事件驱动流程，便于扩展业务消息处理

## 快速上手

### 1. 安装 UniRTOS 工具链

- [开发准备](https://www.quectel.com.cn/unirtos/docs?docs_page=快速上手/开发准备/开发准备.html)
- [安装交叉编译工具链](https://www.quectel.com.cn/unirtos/docs?docs_page=快速上手/环境搭建/环境搭建.html)
- [安装 Python3](https://www.python.org/downloads/)
- [安装 git](https://git-scm.com)
- 安装 `unirtos-cli`：`pip install unirtos-cli`

以上工具安装完成后，确认以下命令可用：

```bash
python --version # Python3
git --version
unirtos --version # 1.0.5 及以上版本
unirtos-cli version # 1.0.11 及以上版本
```

### 2. 使用 unirtos-cli 拉取 demo

先查看可用 demo 与版本：

```bash
unirtos-cli ls-demos
```

创建本 demo 工程：

```bash
unirtos-cli new -r unirtos_aliyun_demos
```

如需指定版本：

```bash
unirtos-cli new -r unirtos_aliyun_demos -v 1.0.0
```

### 3. 进入工程并编译

```bash
cd unirtos_aliyun_demos-1.0.0
unirtos-cli env-setup
unirtos-cli build
```

### 4. 配置阿里云连接参数

在 `unirtos_aliyun_demo.c` 中修改以下宏定义以匹配你的阿里云 IoT 设备信息：

| 宏定义 | 说明 |
|--------|------|
| `ALIOT_BASIC_DEMO_SERVER_ADDR` | 阿里云 MQTT 服务器地址 |
| `ALIOT_BASIC_DEMO_SERVER_PORT` | 服务器端口号 |
| `ALIOT_BASIC_DEMO_TOPIC_SUB` | 订阅主题 |
| `ALIOT_BASIC_DEMO_TOPIC_PUB` | 发布主题 |
| `ALIOT_BASIC_DEMO_CLIENTID` | MQTT 客户端标识 |
| `ALIOT_BASIC_DEMO_PRODUCT_KEY` | 阿里云产品 Key |
| `ALIOT_BASIC_DEMO_DEVICE_NAME` | 设备名称 |
| `ALIOT_BASIC_DEMO_DEVICE_SECRET` | 设备密钥 |
| `ALIOT_BASIC_DEMO_MQTTS` | 是否启用 TLS（0 关闭 / 1 开启） |

示例：

```c
#define ALIOT_BASIC_DEMO_SERVER_ADDR     "iot-xxxxxxxx.mqtt.iothub.aliyuncs.com"
#define ALIOT_BASIC_DEMO_SERVER_PORT     1883
#define ALIOT_BASIC_DEMO_TOPIC_SUB       "/xxxxxxxx/device_name/user/get"
#define ALIOT_BASIC_DEMO_CLIENTID        "xxxxxxxx.device_name"
#define ALIOT_BASIC_DEMO_PRODUCT_KEY     "xxxxxxxx"
#define ALIOT_BASIC_DEMO_DEVICE_NAME     "device_name"
#define ALIOT_BASIC_DEMO_DEVICE_SECRET   ""
#define ALIOT_BASIC_DEMO_TEST_CONTENT    "Hello Welcome to test ali mqtt!"
#define ALIOT_BASIC_DEMO_TOPIC_PUB       "/xxxxxxxx/device_name/user/update"
#define ALIOT_BASIC_DEMO_MQTTS           0
```

### 5. 运行日志示例

成功运行后，串口会看到类似日志：

```bash
[I/DEMO] unir_mqtt_aliot_demo_event_cb 281 event:11,evt_param:c111b9c
[I/DEMO] unir_mqtt aliot demo recv new message 749 client idx=1, new message=0
```

## 常用命令

```bash
# 打开 SDK 菜单配置
unirtos-cli menuconfig

# 清理构建产物
unirtos-cli clean
```

## 技术社区

技术社区：https://forumschinese.quectel.com/c/66-category/66

## 贡献指南

欢迎参与共建，建议按以下方式提交：
- 提交前先执行一次基础验证：env-setup、build、clean。
- 使用清晰的提交说明，描述改动目的、影响范围和验证结果。
- 新增功能或行为变化时，同步更新 README 与相关文档。
- 通过 Issue 或 Pull Request 提交问题修复与功能改进。
