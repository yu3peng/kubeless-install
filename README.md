### 1. 登录免费 Kubernetes 资源

登录以下网址
https://www.katacoda.com/courses/kubernetes/guestbook

认证后，点击 ***START SCENARIO*** 按钮

### 2. 安装 helm 3

Helm3 不需要安装tiller，下载到 Helm 二进制文件直接解压到 $PATH 下就可以使用了。

```
$ cd /opt && wget https://get.helm.sh/helm-v3.1.0-linux-amd64.tar.gz
$ tar -xvf helm-v3.1.0-linux-amd64.tar.gz
$ mv linux-amd64/helm /usr/local/bin/

$ helm version
```

### 3. 安装 kubeless

```
$ helm repo add incubator https://kubernetes-charts-incubator.storage.googleapis.com/
$ kubectl create namespace kubeless
$ helm install --namespace kubeless --set ui.enabled=true \
--set expose.type=nodePort \
--set expose.tls.enabled=false \
--set externalURL=http://127.0.0.1:8080 \
kubeless incubator/kubeless 
```

### 4. 根据提示，键入以下命令，获取 UI 端口

```
$ export NODE_PORT=$(kubectl get --namespace kubeless -o jsonpath="{.spec.ports[0].nodePort}" services kubeless-kubeless-ui)
$ export NODE_IP=$(kubectl get nodes --namespace kubeless -o jsonpath="{.items[0].status.addresses[0].address}")
$ echo http://$NODE_IP:$NODE_PORT
```

### 5. 输入 UI 端口，登录页面

点击页面上的 Guestbook

在端口输入框中输入 echo 中显示的端口号，然后点击 Display Port 按钮

此时即会出现 kubeless 的 UI 界面

### 6. 在页面中创建函数

点击 create function 按钮




