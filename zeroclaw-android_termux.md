先安装好Termux app  
启动app  
得到ubuntu一样的命令行  
安装 apt install wget  

### 下载地址
https://github.com/zeroclaw-labs/zeroclaw/releases  
wget https://github.com/zeroclaw-labs/zeroclaw/releases/download/v0.5.2/zeroclaw-aarch64-linux-android.tar.gz  
比如下载后、解压到 /data/data/com.termux/files/home/zeroclaw_arm 目录  
mkdir ~/zeroclaw_arm  
tar zxf zeroclaw-aarch64-linux-android.tar.gz -C ~/zeroclaw_arm   


#### 可以添加到 PATH 环境变量
修改  ~/.bashrc ，后面添加  
export PATH=$PATH:/data/data/com.termux/files/home/zeroclaw_arm  

### 配置
cd ~/zeroclaw_arm  
./zeroclaw onboard --interactive

#### 大模型  
###### 如果是本地网络的llama.cpp的，例如
base_url:http://192.168.1.134:8000/v1  
sk-local  
any_model  

###### 如果是 qwen，例如  
sk-********************************  
base_url:https://dashscope.aliyuncs.com/compatible-mode/v1  
qwen3-vl-plus  

其它的先不要配置。  

Next steps:  
    1. Send a quick message:  
       zeroclaw agent -m "Hello, ZeroClaw!"  
    2. Start interactive CLI mode:  
       zeroclaw agent  
    3. Check full status:  
       zeroclaw status   
  ⚡ Happy hacking! 🦀  

<p> </p>  

---
## 飞书
直接修改配置文件， 
nano config.toml   
[channels_config.lark]  
app_id = "cli_*****************"  
app_secret = "****************************"  
allowed_users = ["\*"]  
mention_only = false  
use_feishu = true  
receive_mode = "websocket"  

---
### 启动
./zeroclaw gateway start  
多开一个命令行窗口  
./zeroclaw channel start  

可以再开一个命令行窗口测试  
./zeroclaw agent -m "Hello, ZeroClaw!"  


###### 如不想将配置文件放 ~/.zeroclaw，如移到 /data/data/com.termux/files/home/zeroclaw_arm

cd ~/zeroclaw_arm  
mv ~/.zeroclaw/config.toml .   
mv ~/.zeroclaw/workspace .  

然后启动的方法改变为:   
cd ~/zeroclaw_arm  
./zeroclaw gateway start --config-dir .  
./zeroclaw channel start --config-dir .  

---

#### 其它命令
如果移动的配置的目录，记得加参数  --config-dir .  

./zeroclaw providers  
列出所有可用 Provider 和别名。  

\# Interactive onboarding wizard  
./zeroclaw onboard --interactive  

\# Or quick setup (no prompts)  
./zeroclaw onboard --api-key sk-... --provider openrouter --model "openrouter/auto"  

\# Quickly repair channels/allowlists only  
./zeroclaw onboard --channels-only  

\# Chat with the agent  
./zeroclaw agent -m "Hello, ZeroClaw!"  

\# Interactive mode  
./zeroclaw agent  

\# Start gateway + daemon  
./zeroclaw gateway  
./zeroclaw daemon  

\# Check status  
./zeroclaw status  
./zeroclaw doctor  
./zeroclaw channel doctor  

\# Bind Telegram identity into allowlist  
./zeroclaw channel bind-telegram 123456789  

\# Service + migration helpers  
./zeroclaw service install  
./zeroclaw config schema  
./zeroclaw migrate openclaw --dry-run  
./zeroclaw migrate openclaw  

---






