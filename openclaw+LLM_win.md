#### Notepad++ markdown 插件
菜单 Plugins -> Plugins Admin...  
在弹出窗口选中 MarkdownViewer++  
再点击 Install  
重新打开 Notepad++后，在工具栏有个 M+ 图标（近右边）。 点击就是切换 Markdown显示开、关。   

可以顺便安装 HEX-Editor、 NppExec 、 NppTextFX2，等插件  

## 为好安全，OpenClaw 最好是安装在虚拟机中 ！ 在真机的话，就在安装之后，消减权限。


## ............................................Changed List
##### 2026-03-230
添加n卡说明  
Windows平台版本的说明，不再更新  
##### 2026-03-24 
假设的目录添加一层目录  
添加设置目录的环境变量，以使单台电脑可以运行多个实例，设置不同端口和目录  
##### 2026-03-23
添加ADM显示卡的说明  
##### 2026-03-17
初始版本

# =======================================================================================================================================  
# llama.cpp 准备
## ............................................ARM，需要编译，PC平台跳过
cd ~  
git clone https://github.com/ggerganov/llama.cpp.git  
cd llama.cpp  
mkdir build && cd build  

### 配置编译选项（针对 ARM 优化）
cmake .. \  
  -DLLAMA_BUILD_TESTS=OFF \  
  -DLLAMA_ARM_FEATURES=ON \  
  -DLLAMA_BUILD_EXAMPLES=ON \  
  -DCMAKE_BUILD_TYPE=Release  

### 编译（-j6 表示用6个核心，根据手机核心数调整，给手机预留1-2核运行）
make -j6

## ............................................ Windows，或其它PC系统

如果是PC中运行 LLAMA.CPP ，可以直接下载可执行版本， github 上有release  
https://github.com/ggml-org/llama.cpp  
https://github.com/ggml-org/llama.cpp/releases  
注意区分 GPU 和 CPU 

如下载的是CPU版本，则解压到 D:\CLAW\llama_cpu 中，即 D:\CLAW\llama_cpu\llama-server.exe 可直接执行。后面以此路径说明。  

## ............................................下载大模型、运行

## 1. 到llama.cpp目录
cd /d D:\CLAW\llama_cpu  
## 2. 创建模型目录
mkdir -p models  
## 3. 下载 Qwen3.5-0.8B 模型
cd models  
wget https://huggingface.co/unsloth/Qwen3.5-0.8B-GGUF/resolve/main/Qwen3.5-0.8B-Q4_K_M.gguf -O qwen3.5-0.8b-q4_k_m.gguf
## 4. 返回主目录
cd ..  
或  
cd /d D:\CLAW\llama_cpu  

## 更多可选模型
### 下载 Qwen3.5-0.8B（约500MB，微量级）
wget https://huggingface.co/unsloth/Qwen3.5-0.8B-GGUF/resolve/main/Qwen3.5-0.8B-Q4_K_M.gguf -O qwen3.5-0.8b-q4_k_m.gguf
### 下载 Qwen3.5-2B（约1.2GB，小轻量级）
wget https://huggingface.co/unsloth/Qwen3.5-2B-GGUF/resolve/main/Qwen3.5-2B-Q4_K_M.gguf -O qwen3.5-2b-q4_k_m.gguf
### 下载 Qwen3.5-4B（约2.2GB，轻量级）
wget https://huggingface.co/unsloth/Qwen3.5-4B-GGUF/resolve/main/Qwen3.5-4B-Q4_K_M.gguf -O qwen3.5-4b-q4_k_m.gguf  
### 下载 Qwen3.5-9B（约4.8GB，入门级）
wget https://huggingface.co/unsloth/Qwen3.5-9B-GGUF/resolve/main/Qwen3.5-9B-Q4_K_M.gguf -O qwen3.5-9b-q4_k_m.gguf  
Windows下直接粘贴链接到浏览器来下载

测试 llama.cpp 是否正常工作（测试模型正常后Ctrl+c退出，路径根据实际修改）  

D:\CLAW\llama_cpu\llama-cli -m D:\CLAW\llama_cpu\models\qwen3.5-0.8b-q4_k_m.gguf -t 6 -cnv -p "你是一个有用的AI助手，请用中文回答。"


## Nvidia 卡
除了安装本身的驱动，还需要 CUDA ，根据 nvidia-smi命令结果，选择显卡支持的对应版本（需要准备注册官方网站的电邮）  
官方网站 https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html  


## AMD的显示卡 
https://github.com/vosen/ZLUDA/releases  

### 步骤 1：下载 ZLUDA
访问 GitHub 仓库： https://github.com/vosen/ZLUDA  
https://gitcode.com/gh_mirrors/co/ComfyUI-Zluda  

### 步骤 2：安装 AMD 显卡驱动
确保你的系统中安装的是最新的 AMD 显卡驱动（AMD Software: Adrenalin Edition）。

### 步骤 3：配置运行环境
#### Windows 用户
将 ZLUDA 提供的 nvcuda.dll 和 nvml.dll 复制到你要运行的应用程序所在目录。  
或者使用 ZLUDA 提供的启动器： <ZLUDA_DIRECTORY>zluda_with.exe -- <APPLICATION> <<ARGUMENTS>>

https://www.amd.com/en/developer/resources/rocm-hub/hip-sdk.html  

https://www.amd.com/zh-cn/support/downloads/drivers.html/graphics/radeon-r9-r7-r5/radeon-r5-300-series/amd-radeon-r5-m330.html  

# =======================================================================================================================================
# 部署 OpenClaw AI

## ............................................  Git  
需要 git  
https://git-scm.cn/install/windows  
下载后，解压成git子目录，并将里面子目录cmd的全路径(即 D:\CLAW\git\cmd )添加我继续环境变量的PATH中

## ............................................ 安装 Node.js
https://nodejs.org/en/download
建议v24版本，下载可执行版本  

解压到 D:\CLAW\node_v24，并添加其全路径(即 D:\CLAW\node_v24 )到 系统环境变量PATH

## 验证安装
node -v  
npm -v
## ............................................ 安装 OpenClaw 
命令行执行    
mkdir D:\CLAW\OpenClaw  
cd /d D:\CLAW\OpenClaw  
npm install openclaw@2026.3.13  
##### 2026.3.22 版本的WEB UI有问题。等修复后再更新。
##### 如果加 -g 参数就是安装到系统全局的目录中的。作为独立项目，通常不加此参数。
##### 如果有报错，先清理 npm 缓存再安装 npm cache clean --force

## 查看是否安装成功
D:\CLAW\OpenClaw\node_modules\.bin\openclaw --version

# =======================================================================================================================================
# 集成方案——OpenClaw 调用本地 llama.cpp

## ............................................ 启动 llama.cpp 本地 API 服务（关键）

## 在命令行启动 llama.cpp API服务  
set llamaPath=D:\CLAW\llama_cpu\llama-server  
set modelPath=D:\CLAW\llama_cpu\models\qwen3.5-0.8b-q4_k_m.gguf  
set net_info= --host 127.0.0.1 --port 8000
%llamaPath% -m %modelPath% %net_info% --api-key sk-local -c 16384 -b 512 -ngl 0 --threads 4

### 参数说明
#### 1. -m D:\CLAW\llama_cpu\models\qwen3.5-0.8b-q4_k_m.gguf
全称：--model
作用：指定要加载的模型文件路径
这里使用的是 Qwen3.5-0.8B 4 位量化 GGUF 模型，体积小、速度快、适合本地运行。

#### 2. --host 127.0.0.1 --port 8000
作用：服务监听的 IP 地址和端口
127.0.0.1  表示只允许本机访问，更安全。
如需局域网访问，可改为 0.0.0.0。

#### 3. -c 16384
参数全称：--ctx-size
作用：上下文窗口大小（token 数）
16384 表示模型最多能记住约 1.6 万字的上下文。

#### 4. --api-key sk-local
作用：设置 API 访问密钥
调用接口时必须带上这个 key，防止被其他人滥用。

#### 5. -b 512
参数全称：--batch-size
作用：推理批次大小
控制模型一次处理多少 token，影响速度与显存占用，512 是通用稳妥值。

#### 6. -ngl 0
参数全称：--n-gpu-layers
作用：将多少层模型放到 GPU 运行
0  = 纯 CPU 运行，不使用显卡。
有显卡可改成 20/35/99 等数字加速。

#### 8. --threads 4
作用：CPU 推理线程数
建议设置为 CPU 核心数或略少，4 线程适合大多数设备。

#### 9. --verbose
作用：开启详细日志
启动时会打印模型信息、推理速度、请求日志，方便调试与排错。


## ............................................  配置 OpenClaw 对接本地模型
D:\CLAW\OpenClaw\node_modules\.bin\openclaw onboard
配置选项（按顺序选）

### 安全提示：选 Yes
### 模式：选 QuickStart
### 模型提供商：选中 → Custom Provider（自定义）
### API Base URL：输入 http://127.0.0.1:8000/v1 (URL中主机端口，根据实际修改)
### API Key ：输入 sk-local                    （和上面启动命令一致）
### Model ID：输入 qwen3.5-0.8b-q4_k_m.gguf    （随便填，不影响）
### 交互渠道：选 Skip for now
### 技能   ：选 Skip for now
### 钩子   ：选 Skip for now
保存配置，记录生成的 Dashboard Token

#### 再说几个OpenClaw的环境变量参数

REM 主目录，默认值:~/.openclaw/
set OPENCLAW_HOME=%CD%\openclaw_moved

REM state文件所在目录，默认值:~/.openclaw/
set OPENCLAW_STATE_DIR=%CD%\openclaw_moved

REM 配置文件全路径，默认值:~/.openclaw/openclaw.json
set OPENCLAW_CONFIG_PATH=%CD%\openclaw_moved\openclaw.json

REM log级别，2个可选:debug trace
set OPENCLAW_LOG_LEVEL=debug
##### 如果不想保存到个人目录中，可以使用上边的几个环境变量去改变路径

# =======================================================================================================================================
## ............................................  OpenClaw 接入 QQ 机器人

腾讯专门给 OpenClaw 开了 QQ 机器人入口，扫码创建机器人、三条命令接入，不需要公网IP。

### 1、注册 QQ 开放平台
https://q.qq.com/qqbot/openclaw/login.html
打开之后用手机 QQ 扫码登录。如果你之前没注册过 QQ 开放平台，扫码后会让你走一遍实名认证：填姓名、身份证号、手机号，然后人脸识别。整个过程跟注册微信小程序差不多，几分钟搞定。
已经注册过 QQ 开放平台的直接扫码就进去了，不用重复认证。

### 2、创建 QQ 机器人
#### ① 直接有个「创建机器人」按钮，点一下
#### ② 不需要填应用名称，不需要写描述，不需要上传图标，不需要选权限。就是点一下。然后你就有了一个 QQ 机器人。

3、接入 OpenClaw

机器人创建好之后，页面给的三条命令长这样（Token 会是你自己的，这里用示例）：

### 1. 安装 QQ 机器人插件
D:\CLAW\OpenClaw\node_modules\.bin\openclaw plugins install @sliverp/qqbot@latest

### 2. 配置机器人 Token（AppID:AppSecret 格式）
D:\CLAW\OpenClaw\node_modules\.bin\openclaw channels add --channel qqbot --token "102917561:你的AppSecret"

### 3. 重启 Gateway 让配置生效
D:\CLAW\OpenClaw\node_modules\.bin\openclaw gateway restart

### 4、验证是否成功

确认 Gateway 在运行，打开手机 QQ（或者电脑版 QQ），在联系人或搜索里找到你刚创建的机器人。给它发一条消息，比如「你好」。如果机器人正常回复了，说明全通了。
一个 QQ 号能建 5 个机器人

### 5、启动 OpenClaw 并测试

### 启动网关
D:\CLAW\OpenClaw\node_modules\.bin\openclaw gateway --verbose  

#### 前台运行 --- 日常运行这个命令就可以
openclaw gateway run  


## ............................................ Feishu
飞书开通过程类似，开通机器人。
麻烦一点是要设置权限、消息和回调 

权限，批量导入

{  
  "scopes": {  
    "tenant": [  
      "aily:file:read",  
      "aily:file:write",  
      "application:application.app_message_stats.overview:readonly",  
      "application:application:self_manage",  
      "application:bot.menu:write",  
      "cardkit:card:write",  
      "contact:user.employee_id:readonly",  
      "corehr:file:download",  
      "docs:document.content:read",  
      "event:ip_list",  
      "im:chat",  
      "im:chat.access_event.bot_p2p_chat:read",  
      "im:chat.members:bot_access",  
      "im:message",  
      "im:message.group_at_msg:readonly",  
      "im:message.group_msg",  
      "im:message.p2p_msg:readonly",  
      "im:message:readonly",  
      "im:message:send_as_bot",  
      "im:resource",  
      "sheets:spreadsheet",  
      "wiki:wiki:readonly"  
    ],  
    "user": ["aily:file:read", "aily:file:write", "im:chat.access_event.bot_p2p_chat:read"]  
  }  
}  

权限json来源链接：https://juejin.cn/post/7608178484016447528

⚠️在配置事件订阅前，请务必确保已完成以下步骤：
运行 openclaw channels add 添加了 Feishu 渠道
网关处于启动状态（可通过 openclaw gateway status 检查状态）

在 事件订阅 页面：
选择 使用长连接接收事件（WebSocket 模式）
添加事件：im.message.receive_v1（接收消息）
⚠️ 注意：如果网关未启动或渠道未添加，长连接设置将保存失败。



# =======================================================================================================================================
## 测试、调试



