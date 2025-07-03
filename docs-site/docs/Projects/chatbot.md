## 🧠 WeClone Deployment Note

!!! note "Project Overview"
    This note records my complete deployment journey of [WeClone](https://github.com/xming521/WeClone), a local fine-tuning tool that turns chat history into a personalized language model, and its integration with [AstrBot](https://github.com/AstrBotDevs/AstrBot).

---

## 🚀 Environment Setup

### ✅ WSL2 Installation and Linux Environment

* Installed WSL2 with Ubuntu.
* Installed Git, Python 3.10+, pip, and `uv` as a fast dependency manager.

!!! tip "Virtual Environment with uv"
    Use `uv venv .venv` to create a virtual environment and `source .venv/bin/activate` to activate it. This avoids interfering with system Python and supports `pyproject.toml` based dependency management.

### ✅ WeClone Project Setup

* GitHub Repo: [WeClone](https://github.com/xming521/WeClone)
* Official Guide: [weclone.love](https://www.weclone.love/what-is-weclone.html)

```bash
# Clone project
cd ~
git clone https://github.com/xming521/WeClone.git
cd WeClone

# Create and activate venv
uv venv .venv
source .venv/bin/activate

# Install dependencies
uv pip install --group main -e .
```

!!! warning "flash-attn optional dependency"
FlashAttention requires CUDA and nvcc. In WSL2, you must install the full CUDA toolkit and set `CUDA_HOME` before installing:
`bash
    uv pip install flash-attn --no-build-isolation
    `
Skip this step if you're not training large models or running on CPU.

## 📦 Model Download via ModelScope

```bash
uv pip install modelscope
modelscope download --model Qwen/Qwen2.5-7B-Instruct --local_dir ./models/Qwen2.5-7B-Instruct
```

!!! info "What is ModelScope?"
ModelScope is a model hosting service by Alibaba DAMO Academy. It provides an easy CLI to download open-source foundation models.
[Model page](https://modelscope.cn/models/Qwen/Qwen2.5-VL-32B-Instruct)

## 🗂️ Data Preprocessing

* Export WeChat chat history using [PyWxDump](https://github.com/xaoyaoo/PyWxDump).
* Place `.csv` in `./data/csv/` folder.
* Preprocess using:

```bash
weclone-cli make-dataset
```

!!! tip "Automated startup shortcut"
Add to `.bashrc`:
`bash
    alias start-weclone='source ~/WeClone/.venv/bin/activate && weclone-cli server'
    `

## 🧪 Model Finetuning & Testing

```bash
# Fine-tuning (Single GPU)
weclone-cli train-sft

# Test model response
weclone-cli test-model
```

## 🌐 API & Interface

```bash
# Start REST API service
weclone-cli server
```

* Default listening on: `http://127.0.0.1:8005/v1`

!!! important "WSL Networking Tip"
If WeClone runs in WSL2 and AstrBot runs in Docker, you must connect via WSL's internal IP (e.g. `172.24.x.x`) rather than `localhost`.
Use `ip addr show` inside WSL to find this IP.

## 🤖 AstrBot Integration

* GitHub: [AstrBot](https://github.com/AstrBotDevs/AstrBot)
* Docs: [docs.astrbot.app](https://docs.astrbot.app/what-is-astrbot.html)

### 🌐 Model Provider Setup

* If WeClone is hosted in WSL2:

  * Set API Base: `http://172.24.x.x:8005/v1`
  * Ensure WeClone server is running and accessible

### 💬 Messaging Platform Tips

* **Feishu**: Bot name in AstrBot must exactly match the name registered in Feishu platform.
* **WeChat Personal**: Use `wechatpadpro` with Docker, and ensure proper config for `admin_key`, `host`, and `port`. Docker network should allow communication between containers.

## 🧰 Other Tools & Tech Used

### 🐳 Docker Compose

Used to deploy supporting services like `wechatpadpro`:

* Web docs often at: [http://localhost:38849/docs](http://localhost:38849/docs)

### 📦 Python Modern Packaging

* `uv` + `pyproject.toml` for dependency management
* Supports multiple dependency groups (main/dev/test)

### 🔬 LLaMA Factory

* WeClone uses [LLaMA-Factory](https://github.com/hiyouga/LLaMA-Factory) under the hood to support LLM training and inference.

---

## ✅ Summary

This setup combines LLM training, API deployment, chat integration, and WSL networking. I now understand how to:

* Export and clean real-world chat data
* Run models locally with REST API
* Connect chatbots via Docker
* Build with modern Python toolchains (uv + pyproject.toml)

!!! success "What’s Next?"
I plan to try:
\- Multi-GPU or LoRA fine-tuning
\- Deploying the WeClone API via cloud (e.g. HuggingFace, EC2)
\- Integrating more platforms via AstrBot (Telegram, Discord, etc)




#
``` bash
# 用到的知识点
使用WeClone的模型根据wechat chat history 训练模型
    -github repo:https://github.com/xming521/WeClone
    -文档指南 https://www.weclone.love/what-is-weclone.html
    - 常用指令 ：
        1.数据预处理 weclone-cli make-dataset
        2.模型微调（单卡训练） weclone-cli train-sft
        3. 使用浏览器Demo简单退推理 weclone-cli webchat-demo； 使用API接口 weclone-cli server，接口监听在http://127.0.0.1:8005/v1
        4.测试模型 ：weclone-cli test-model

window 创建WSL2子系统-linux

PyWxDump
    -基本简介，用于导出微信聊天记录, 提供可视化的工具使用
    -github https://github.com/xaoyaoo/PyWxDump/
    -下载 https://github.com/xaoyaoo/PyWxDump/releases

linux下自动运行设定好的脚本
    。bashrc中写 alias start-weclone='source ~/WeClone/.venv/bin/activate && weclone-cli server'
    然后直接start-weclone

从ModelScope下载模型,例如Qwen2.5-7B-Instruct
    - 可以使用uv pip install modelscope
    -ModelScope 是什么，如何使用，link   https://modelscope.cn/models/Qwen/Qwen2.5-VL-32B-Instruct
    - modelscope download --model Qwen/Qwen2.5-7B-Instruct --local_dir ./models/Qwen2.5-7B-Instruct

AstrBot的部署
    - 文档：https://docs.astrbot.app/what-is-astrbot.html
    - github https://github.com/AstrBotDevs/AstrBot
    - 注意使用astrbot设置大模型的时候有如下问题
        1.服务提供商管理：连接大模型的API base 填什么？
            如果都是在同一主机可以填localhost，但是如果astrbot使用docker部署，大模型在wsl内，需要填wsl的ip，使用ip addr show查看
        2.消息平台，成功连接了飞书和微信个人：注意飞书机器人名必须和飞书中创建的bot名字一致，否则无法调用; 使用wechatpadpro连接个人微信，注意填写admin_key和host,port，还是 需要确定部署的astrbot和wechatpadpro是什么环境 (docker?) 是否共享网络
        

部署到飞书

# 学到的技术
docker compose部署多个应用
-例如部署WechatpadPro
    - 文档页面：http://localhost:38849/docs


uv和pyproject.toml
    - 使用uv venv .venv在当前目录创建python虚拟环境
    - source .venv/bin/activate激活
    - pyproject.toml如何使用，好处有哪些


了解 LLaMA Factory 

```