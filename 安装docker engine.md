# 1. 更新 apt 包索引并安装允许通过 HTTPS 使用存储库的依赖项
sudo apt update
sudo apt install ca-certificates curl

# 2. 创建存放密钥的目录，并下载 Docker 官方的 GPG 密钥
sudo install -m 0755 -d /etc/apt/keyrings

sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

sudo chmod a+r /etc/apt/keyrings/docker.asc

# 3. 将 Docker 存储库配置写入系统的源列表中
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF

Types: deb

URIs: https://download.docker.com/linux/ubuntu

Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")

Components: stable

Architectures: $(dpkg --print-architecture)

Signed-By: /etc/apt/keyrings/docker.asc

<img width="860" height="439" alt="image" src="https://github.com/user-attachments/assets/f426e2c1-3346-4bed-bb62-73b7eeb7194a" />


EOF
# 1. 再次更新 apt 包索引，让系统读取刚刚添加的 Docker 源
sudo apt update

# 2. 安装 Docker Engine、CLI 命令行工具以及必要的插件
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
#接下来验证是否成功
# 1. 检查 Docker 服务是否正在运行（如果看到绿色的 active (running)，按 'q' 键退出）
sudo systemctl status docker

# 2. 运行经典的 hello-world 容器测试
sudo docker run hello-world
#看到hello form docker就是成功了
<img width="710" height="382" alt="image" src="https://github.com/user-attachments/assets/b69ac827-63df-41a5-8752-64192e5808e1" />

默认情况下，运行 docker 命令需要 root 权限（每次都要加 sudo）。如果您希望直接使用普通用户运行 Docker，可以执行以下命令将当前用户加入 docker 用户组：

Bash
sudo usermod -aG docker $USER

#如果出现了报错

level=warning msg="Error getting v2 registry: Get \"https://registry-1.docker.io/v2/\": net/http: request canceled..."

原因分析：
这段报错的意思是：Docker 在尝试连接 Docker Hub 的官方服务器 (registry-1.docker.io) 下载测试镜像时，连接超时被取消了。这是国内极其常见的情况，
主要是因为国内网络环境无法直接稳定访问 Docker 的官方镜像仓库。

我们直接在V2里面左下角看自己的端口
<img width="288" height="58" alt="image" src="https://github.com/user-attachments/assets/e05cef7d-d886-4fe3-a2f4-e096ad8cd30a" />

#然后输入下面指令
sudo mkdir -p /etc/systemd/system/docker.service.d

sudo tee /etc/systemd/system/docker.service.d/http-proxy.conf <<EOF

[Service]

Environment="HTTP_PROXY=http://127.0.0.1:您的端口号"

Environment="HTTPS_PROXY=http://127.0.0.1:您的端口号"

EOF
#这时候重启配置
sudo systemctl daemon-reload

sudo systemctl restart docker
#重启后，您可以先用下面这个命令检查一下 Docker 是否成功读取到了代理设置：

sudo docker info | grep Proxy

如果输出中能看到 HTTP Proxy: http://127.0.0.1:您的端口号 等字样，说明参数设置已经生效！

