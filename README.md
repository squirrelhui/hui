# 法规对比项目基础环境安装部署手册

## 一、功能介绍

​       本软件实现在物理Linux服务器、主流厂商的云主机以及Linux虚拟环境，利用ansible软件配合kubernetes官方提供的二进制软件包自动部署具备一个master节点和一个node节点的kubernetes集群，并可用于后续安装法规项目软件。

​       本次安装部署完成后已获取的软件版本如下：

​       kubernetes   v1.16.0

​       docker           v18.09.6



## 二、安装指南

### （一）安装前建议

用户可以根据自身系统的环境和使用的场景选择不同方式的安装方法。

1、**开发环境**可以参考**“windows、mac系统、Linux系统（单台）——安装虚拟Linux环境指南”**<a href="###1、windows、mac系统、Linux系统（单台）——安装虚拟Linux环境指南">点击跳转</a>

2、**服务器生产或测试环境**可以参考**“多台Linux系统物理机安装指南”**<a href="###2、多台Linux系统物理机安装指南">点击跳转</a>

3、**云主机环境**可以参考**“云主机环境安装指南”**<a href="###（三）云主机环境安装指南">点击跳转</a>



### （二）物理机环境安装指南

### 1、windows、mac系统、Linux系统（单台）——安装虚拟Linux环境指南

#### （1）下载Vagrant软件

可自行根据操作系统版本选择安装相应的Vagrant软件。

下载链接为：https://www.vagrantup.com/downloads.html

#### （2）Vagrant软件安装指南

a、windos系统、mac系统

[Vagrant安装参考链接](https://www.vagrantup.com/docs/installation/)

b、Linux系统

安装时运行以下命令

```powershell
# CentOS系统
yum -y install https://releases.hashicorp.com/vagrant/2.2.7/vagrant_2.2.7_linux_amd64.zip

# Ubuntu系统
apt install -y vagrant
```

#### （3）Vagrant软件安装验证

注意：a、在windows系统上，按下win键+R键，在弹出的窗口输入“cmd”即可进入命令提示符界面。

​            b、在mac系统上，按下command键+ 空格键，然后在弹出的窗口输入“te”，可以进入终端界面。

​            c、图形界面的Linux系统上，CentOS系统按下Ctrl键+T键，Ubuntu系统按下Ctrl键+Alt键+T键，可以打开终端界面。

在命令提示符或终端界面输入以下命令进行验证。

```
vagrant --version

# 如出现vagrant版本信息即为安装成功
Vagrant 2.2.7
```

#### （4）下载Virtualbox

可自行根据操作系统版本选择安装相应的Virtualbox软件。

下载链接为：https://www.virtualbox.org/wiki/Downloads

#### （5） Virtualbox软件安装指南

[Windows系统参考链接（请点击）](https://blog.csdn.net/shaock2018/article/details/103598635?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158596083419724839259831%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=158596083419724839259831&biz_id=14&utm_source=distribute.pc_search_result.none-task-blog-soetl_SOETL-7)

[Mac系统参考链接（请点击）](https://www.cnblogs.com/andong2015/p/7688120.html)

[Linux系统参考链接（请点击）](https://www.virtualbox.org/wiki/Linux_Downloads)

#### （6）下载Vagrant软件配置文件及基础镜像

下载链接为：https://pan.baidu.com/s/1s0VD5KJmSx4lZJW5RpATtg      提取码为：35dl

文件名称为：bayes_vagrant.zip

建议解压至目录为    ~/bayes_centos

#### （7）构建Linux虚拟环境

```
# 进入解压的目录
cd D:\bayes_centos

# 向vagrant软件导入自制镜像
vagrant box add bayes-centos bayes-centos.box

# 启动虚拟机
vagrant up

# 验证虚拟机状态
vagrant status

# 远程进入虚拟机（用户名为：root，密码为：vagrant）
vagrant ssh k8smaster
vagrant ssh k8snode1

# 删除虚拟机
vagrant destroy k8smaster
vagrant destroy k8snode1
```

注意：

如需要自定义虚拟机配置或其他信息，可使用文本编辑器对Vagrantfile进行编辑。

不进行修改的，默认启动两台2C2G及CentOS系统的虚拟机。

此外，在解压文件夹内同步创建两个虚拟主机的共享目录用于放置共享文件。

共享目录示例如下：

物理机内目录是：

D:\bayes_centos\k8smaster\

D:\bayes_centos\k8snode1\

虚拟机目录是：

/root/vagrant/

#### （8）部署kubernetes集群

可以具体参”二、安装指南 第（三）点“部署kubernetes集群<a href="###（三）部署kubernetes集群">点击跳转</a>



### 2、多台Linux系统物理机安装指南

可以具体参”二、安装指南 第（三）点“部署kubernetes集群<a href="###（三）部署kubernetes集群">点击跳转</a>



### （三）云主机环境安装指南

#### 1、下载terraform软件

可自行根据操作系统版本选择安装相应的terraform软件。

下载链接地址：https://www.terraform.io/downloads.html

#### 2、安装terraform软件

[各主流操作系统的安装指南（含视频教程）](https://learn.hashicorp.com/terraform/getting-started/install)

#### 3、验证terraform软件安装情况

注意：a、在windows系统上，按下win键+R键，在弹出的窗口输入cmd即可进入命令提示符界面。

​            b、在mac系统上，按下command键+ 空格键，然后在弹出的窗口输入te，可以进入终端界面。

​            c、图形界面的Linux系统上，CentOS系统按下Ctrl键+T键，Ubuntu系统按下Ctrl键+Alt键+T键，可以打开终端界面。

在命令提示符或终端界面输入以下命令进行验证。

```
# terraform --version

# 出现类似以下版本提示即为安装成功
Terraform v0.12.24
```

#### 4、获取云主机营运商的密钥（以阿里云、腾讯云为例）

#### （1）获取密钥

阿里云获取密钥方式如下：

[阿里云官方指南](https://help.aliyun.com/knowledge_detail/144253.html)

腾讯云获取密钥方式如下：

[腾讯云官方指南](https://cloud.tencent.com/document/api/213/30654)

注意：切记保存好**下载的CSV文件**后续步骤中需要使用。

#### （2）配置密钥环境变量

阿里云：安装Alibaba Cloud CLI配置profile环境

 [官方安装指南](https://github.com/aliyun/aliyun-cli/blob/master/README-CN.md)

腾讯云：配置密钥的环境变量

```
    $ export TENCENTCLOUD_SECRET_ID="your_fancy_accessid"
    $ export TENCENTCLOUD_SECRET_KEY="your_fancy_accesskey"
    $ export TENCENTCLOUD_REGION="ap-guangzhou"
```

#### 5、下载terraform部署模板

阿里云模板：

下载链接为：https://pan.baidu.com/s/1AMT8UjV1T0l-DvzQC8GlXw   提取码为：02l2

下载文件为：terraform.tf

建议下载目录为c:\ali



腾讯云模板：

下载链接为：https://pan.baidu.com/s/1nCElxjtQIzg660GFsygZww    提取码为：kgg3

下载文件为：tencent.tf

建议下载目录为c:\tencent



#### 6、配置terraform模板

如果需要对云主机进行配置的，可以使用文本编辑器对terraform.tf进行修改。

如不修改，则默认配置为2台2C4G的云主机并配置两个公网ip，收费方式为按量付费。

#### 7、使用terraform构建云主机

```
# terraform软件初始化（下载插件时间较长，请耐心等待）
terraform init

# terraform软件检查配置文件
terraform plan

# terraform软件构建云主机
terraform apply

# terraform显示云主机状态信息
1、验证是否成功构建
2、获取云主机创建的公网ip及内网ip
terraform show

#运行，并输入账户、密码来访问ECS实例。
ssh root@<公网ip>
如使用默认模板创建，账户名：root，密码：bayes@888

# terraform删除云主机
terraform destroy
```



### （四）部署kubernetes集群

#### 1、下载软件包

（1）安装git软件

```shell
# CentOS系统执行以下命令
# yum -y install git

# Ubuntu系统执行以下命令
# apt-get -y install git
```



（2）dpa_tools下载地址：

```
# cd /root/
# git clone https://codehub.devcloud.huaweicloud.com/DataOps00001/dpa_tools.git

# 按提示输入你的账户和密码
账户格式为：bayesba/yejianhui
密码：您的华为云账号密码
```

注意：dpa_tools文件下载至master节点和node节点主机/root/目录下

校验：

```shell
# 执行以下命令
# ls /root/

# 若出现以下信息即为已按要求下载软件
dpa_tools
```



（3）binary_pkg.tar.gz下载地址：

本软件包暂时使用百度网盘进行文件共享，提取码为36j3。

链接：https://pan.baidu.com/s/1HYd8DPjRlKeonaAg5n_oJg

注意：binary_pkg.tar.gz文件下载至master节点主机/root/目录下

```
# 解压软件包
# cd /root/
# tar zxf binary_pkg.tar.gz 
```

校验：

```shell
# 执行以下命令
# ls /root/

# 若出现以下信息即为已按要求下载软件
dpa_tools  binary_pkg
```



（4）注意：如安装环境不具备外网功能，可联系贝业思公司人员提供软件包。



#### 2、检查系统环境

1、在两个节点中运行check_os_status.sh脚本对Linux系统环境检查。

```shell
# cd /root/dpa_tools/k8s-install
# bash bayes_k8s_check.sh
```

本检查脚本可以实现以下功能： 

（1）设置防火墙为关闭的状态

（2）设置seLinux的为关闭的状态

（3）设置swap分区为关闭的状态

（4）设置自动同步时间



#### 3、修改ansible配置文件

（1）在master节点中修改项目中的hosts文件内容。

注意：仅需修改master、node、etcd的相关ip地址即可。

```shell
# cd /root/dpa_tools/k8s-install
# vim hosts

# 若不想使用自定义设置可选择执行以下命令对文本内容进行修改
sed -i 's/192.168.1.30/你的master节点的IP/g' hosts  #按实际修改你的master节点的IP
sed -i ‘s/192.168.1.31/你的node节点的IP/g' hosts    #按实际修改你的node节点的IP

```

校验：

```shell
# 执行以下命令可检查hosts文件内容
# cat /root/dpa_tools/k8s-install/hosts
```



（2）在master节点中修改group_vars/all.yml文件。

注意：仅需修改cert_hosts下k8s、etcd的ip地址即可。

```shell
# cd /root/dpa_tools/k8s-install
# vim group_vars/all.yml

# 若不想使用自定义设置可选择执行以下命令对文本内容进行修改
sed -i 's/192.168.1.30/你的master节点的IP/g' hosts   #按实际修改你的master节点的IP
sed -i ‘s/192.168.1.31/你的node节点的IP/g' hosts     #按实际修改你的node节点的IP
```

校验：

```shell
# 执行以下命令可检查group_vars/all.yml文件内容
# cat /root/dpa_tools/k8s-install/group_vars/all.yml
```



#### 4、执行自动部署脚本

在master节点主机上执行ansible.sh开展部署工作。

```shell
# cd /root/dpa_tools/k8s-install
# bash bayes_k8s_install.sh
```

**注意**：执行上述脚本时会自动通过外网安装ansible软件，如安装环境不具备外网环境，可联系贝业思公司人员获取ansible软件安装包并执行以下步骤，再行执行ansible.sh开展部署工作。

```
# 将ansible_pkgs放置于/root/目录下
# tar -zxvf ansible.tar.gz
# cat > /etc/yum.repos.d/ansible.repo << EOF
[ansible]
name=ansible
baseurl=file:///root/ansible_pkgs
enabled=1
gpgcheck=0
EOF
# yum install ansible -y
```



#### 5、验证集群功能

（1）查看集群状态

```shell
# 执行以下命令可获取集群所有主机的相应状态，如STATUS为Ready，即说明集群完成正常部署
# kubectl get nodes
NAME          STATUS     ROLES    AGE     VERSION
k8s-master1   Ready      <none>   2d21h   v1.16.0
k8s-node1     Ready      <none>   2d21h   v1.16.0

# 执行以下命令可以获取集群内相关组件的启动状态，如如STATUS为Ready，即说明集群组件均启动正常
root@ecs-6919:~# kubectl get pod --all-namespaces
NAMESPACE              NAME                                         READY   STATUS    RESTARTS   AGE
ingress-nginx          nginx-ingress-controller-cjfg2               1/1     Running   1          2d22h
ingress-nginx          nginx-ingress-controller-dtxl6               1/1     Running   1          2d22h
kube-system            coredns-6d8cfdd59d-5lq25                     1/1     Running   1          2d22h
kube-system            kube-flannel-ds-amd64-qcfww                  1/1     Running   1          2d22h
kube-system            kube-flannel-ds-amd64-vjtjl                  1/1     Running   1          2d22h
kubernetes-dashboard   dashboard-metrics-scraper-566cddb686-zsnrf   1/1     Running   1          2d22h
kubernetes-dashboard   kubernetes-dashboard-c4bc5bd44-mmfv9         1/1     Running   1          2d22h
```



（2）使用命令行启动nginx容器进行检测

```shell
# 可以使用以下命令创建nginx容器进行测试
# kubectl create deployment web --image=nginx:1.15

# 可以使用以下命令检查nginx容器创建的情况
# kubectl get pod -n default
NAME                   READY   STATUS    RESTARTS   AGE
web-5886dfbb96-zzp5w   1/1     Running   0          55s
# kubectl get pod -n default -o wide
NAME                   READY   STATUS    RESTARTS   AGE     IP           NODE          NOMINATED NODE   READINESS GATES
web-5886dfbb96-zzp5w   1/1     Running   0          3m40s   10.244.1.2   k8s-master1   <none>           <none>

# 若上述STATUS状态为Runing即为正常状态。
```



#### 6、基础环境中新增node部署方法

（1）修改ansible配置文件，参考步骤第三点第（四）款。

（2）执行新增node命令

```shell
# ansible-playbook -i hosts add-node.yml -uroot -k
```



#### 7、注意事项

（1）部分版本ubuntu系统出现coredns报错处理方法

```shell
# 执行以下命令修改configmap
# kubectl edit cm coredns -n kube-system

# 将configmap文件中的proxy参数进行修改
原：   proxy . /etc/resolv.conf
改为：  proxy . 8.8.8.8
```

（2）停止kubernetes集群服务

```shell
# master节点执行以下命令
systemctl stop kube-apiserver kube-controller-manager kube-scheduler docker

# node节点执行以下命令
systemctl stop kubelet kube-proxy docker
```

（3）系统环境恢复方法

dpa_tool目录中并已提供undo_os_status.sh，可以恢复Linux防火墙、seLinux、swap分区的原始状态

```shell
# cd /root/dpa_tools/k8s-install
# bash bayes_k8s_undo.sh
```

