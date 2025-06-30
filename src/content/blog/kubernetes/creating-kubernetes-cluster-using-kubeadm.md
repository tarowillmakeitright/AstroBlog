---
author: Taro Gray
pubDatetime: 2025-06-30T08:00:00.00Z
title: GCPでkubeadmを使ってKubernetesクラスタを構築する手順
postSlug: creating-kubernetes-cluster-using-kubeadm
featured: true
tags:
  - kubernetes
description: Google Cloud Platform上で仮想マシンを作成し、kubeadmを使用してKubernetesクラスタを手動で構築する方法について、事前準備・構成ファイル・初期化手順を含めて解説します。
---

## 質問

GCP上で `kubeadm config` を用いてKubernetesクラスタを構築するにはどうすればいいですか？  
具体的な手順と構成ファイルの例を含めて教えてください。

---

## ✅ 回答：**GCP上でkubeadmを用いたクラスタ構築は、VMを手動で用意し、初期化設定を行うプロセス**

---

## 🧱 構築の概要ステップ

### ✅ 1. GCP VM インスタンスの作成

```bash
gcloud compute instances create master-node \
  --zone=us-central1-a \
  --machine-type=e2-medium \
  --image-family=ubuntu-2004-lts \
  --image-project=ubuntu-os-cloud \
  --boot-disk-size=20GB \
  --tags=k8s,master
```

```
gcloud compute instances create worker-node \
  --zone=us-central1-a \
  --machine-type=e2-medium \
  --image-family=ubuntu-2004-lts \
  --image-project=ubuntu-os-cloud \
  --boot-disk-size=20GB \
  --tags=k8s,worker
```

---

✅ 2. 各ノードで必要なパッケージをインストール

```
sudo apt update && sudo apt install -y apt-transport-https curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt update
sudo apt install -y kubelet kubeadm kubectl containerd
sudo systemctl enable kubelet
```

---

✅ 3. containerdの設定と起動

```
sudo mkdir -p /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml
sudo systemctl restart containerd
```

---

✅ 4. スワップを無効化

```
sudo swapoff -a
sudo sed -i '/ swap / s/^/#/' /etc/fstab
```

---

⚙️ kubeadm構成ファイル例（YAML）

```
kubeadm-config.yaml

apiVersion: kubeadm.k8s.io/v1beta3
kind: InitConfiguration
localAPIEndpoint:
  advertiseAddress: 10.128.0.10  # Masterノードの内部IP
  bindPort: 6443
```

```
apiVersion: kubeadm.k8s.io/v1beta3
kind: ClusterConfiguration
kubernetesVersion: "v1.30.0"
networking:
  podSubnet: "192.168.0.0/16"  # Calico等に対応
controllerManager:
  extraArgs:
    node-cidr-mask-size: "24"
```

---

✅ 5. Control Planeを初期化

```
sudo kubeadm init --config=kubeadm-config.yaml
```

---

✅ 6. kubectlの設定

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

---

✅ 7. Podネットワークをインストール（例：Calico）

```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

---

✅ 8. Workerノードをクラスタに参加させる

Control Plane側で出力されたコマンドを実行：

```
sudo kubeadm join 10.128.0.10:6443 --token <TOKEN> --discovery-token-ca-cert-hash sha256:<HASH>
```

---

✅ まとめ

```
手順	内容
VM作成	GCP上にUbuntu VMを作成
パッケージ導入	kubeadm/kubelet/kubectl/containerd をインストール
構成	kubeadm-config.yamlで設定を明示的に管理
初期化	kubeadm init --config でControl Planeを構築
Join	Workerノードをkubeadm joinで接続
```

---

関連リンク - Kubeadm公式ドキュメント [https://kubernetes.io/docs/reference/setup-tools/kubeadm/] - GCP Compute Engine ドキュメント [https://cloud.google.com/compute/docs/]
