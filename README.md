# Winter-quarkus

```sh

echo "
  deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
  deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
  deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
  deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-security main restricted universe multiverse
" > /etc/apt/sources.list

export DEBIAN_FRONTEND=noninteractive

apt update -y

apt install -y curl wget git openjdk-21-jdk-headless maven

if [ ! -d ~/Winter-quarkus ]; then cd ~/ ; git clone https://github.com/AndyInAi/Winter-quarkus.git; fi


# 运行

cd  ~/Winter-quarkus && tar xzf quarkus-app.tar.gz

cd ~/Winter-quarkus && java -jar quarkus-app/quarkus-run.jar

# starting HTTP server at http://0.0.0.0:8080/

# 测试
curl http://localhost:8080/


# 或者安装编译环境，编译源代码后运行

(
	_sum=""
	if [ -f ~/quarkus-cli-3.6.0.tar.gz ]; then
		_sum="`sha256sum ~/quarkus-cli-3.6.0.tar.gz | grep 5b592b78ec7fd86354b8aed36964914a683fd6246e66b9a3cc658cdb1ad05e45`"
	fi
	if [ "$_sum" == "" ]; then
		wget -q --show-progress -O ~/quarkus-cli-3.6.0.tar.gz https://github.com/quarkusio/quarkus/releases/download/3.6.0/quarkus-cli-3.6.0.tar.gz
	fi
)

tar xzvf ~/quarkus-cli-3.6.0.tar.gz -C ~/

export PATH=~/quarkus-cli-3.6.0/bin:$PATH
echo 'export PATH=~/quarkus-cli-3.6.0/bin:$PATH' >> /etc/profile


# 编译源代码

cd ~/Winter-quarkus && ./mvnw clean && ./mvnw package

# 运行

cd ~/Winter-quarkus && java -jar target/quarkus-app/quarkus-run.jar

# starting HTTP server at http://0.0.0.0:8080/

# 测试
curl http://localhost:8080/

```
