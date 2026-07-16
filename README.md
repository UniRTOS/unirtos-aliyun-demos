# unirtos-aliyun-demos

[中文](README.zh.md) | English

This repository is recommended to be used through the `unirtos-cli` demo workflow to ensure consistency in project creation, environment setup, and build procedures.

## Feature Description

This demo shows the complete workflow for a UniRTOS device connecting to the Alibaba Cloud IoT platform through MQTT, and is suitable as a cloud connectivity example.

- Supports Alibaba Cloud device authentication (`clientId / username / password`)
- Supports MQTT topic subscription and message publishing
- Supports optional TLS connectivity (can be enabled by configuration)
- Uses an asynchronous event-driven workflow for easy extension of business message handling

## Quick Start

### 1. Install the UniRTOS Toolchain

- [Development Preparation](https://www.quectel.com.cn/unirtos/docs?docs_page=快速上手/开发准备/开发准备.html)
- [Install the Cross-Compilation Toolchain](https://www.quectel.com.cn/unirtos/docs?docs_page=快速上手/环境搭建/环境搭建.html)
- [Install Python3](https://www.python.org/downloads/)
- [Install git](https://git-scm.com)
- Install `unirtos-cli`: `pip install unirtos-cli`

After the above tools are installed, confirm that the following commands are available:

```bash
python --version # Python3
git --version
unirtos --version # 1.0.5 or later
unirtos-cli version # 1.0.11 or later
```

### 2. Fetch the Demo Using unirtos-cli

First, check the available demos and versions:

```bash
unirtos-cli ls-demos
```

Create this demo project:

```bash
unirtos-cli new -r unirtos-aliyun-demos
```

To specify a version:

```bash
unirtos-cli new -r unirtos-aliyun-demos -v 1.0.0
```

### 3. Enter the Project and Build

```bash
cd unirtos-aliyun-demos-1.0.0
unirtos-cli env-setup
unirtos-cli build
```

### 4. Configure Alibaba Cloud Connection Parameters

Modify the following macro definitions in `unirtos_aliyun_demo.c` to match your Alibaba Cloud IoT device information:

| Macro | Description |
|--------|-------------|
| `ALIOT_BASIC_DEMO_SERVER_ADDR` | Alibaba Cloud MQTT server address |
| `ALIOT_BASIC_DEMO_SERVER_PORT` | Server port number |
| `ALIOT_BASIC_DEMO_TOPIC_SUB` | Subscription topic |
| `ALIOT_BASIC_DEMO_TOPIC_PUB` | Publish topic |
| `ALIOT_BASIC_DEMO_CLIENTID` | MQTT client identifier |
| `ALIOT_BASIC_DEMO_PRODUCT_KEY` | Alibaba Cloud product key |
| `ALIOT_BASIC_DEMO_DEVICE_NAME` | Device name |
| `ALIOT_BASIC_DEMO_DEVICE_SECRET` | Device secret |
| `ALIOT_BASIC_DEMO_MQTTS` | Whether to enable TLS (`0` disabled / `1` enabled) |

Example:

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

### 5. Example Runtime Log

After successful execution, the serial port will show logs similar to the following:

```bash
[I/DEMO] unir_mqtt_aliot_demo_event_cb 281 event:11,evt_param:c111b9c
[I/DEMO] unir_mqtt aliot demo recv new message 749 client idx=1, new message=0
```

## Common Commands

```bash
# Open the SDK menu configuration
unirtos-cli menuconfig

# Clean build artifacts
unirtos-cli clean
```

## Technical Community

Technical Community: https://forumschinese.quectel.com/c/66-category/66

## Contribution Guide

Contributions are welcome. It is recommended to submit changes in the following way:
- Run a basic verification before submission: `env-setup`, `build`, `clean`.
- Use clear commit messages describing the purpose of the change, scope of impact, and verification results.
- When adding new features or changing behavior, update the README and related documentation accordingly.
- Submit bug fixes and feature improvements through Issues or Pull Requests.
