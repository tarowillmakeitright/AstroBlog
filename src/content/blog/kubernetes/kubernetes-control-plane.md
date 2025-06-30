---
author: Taro Gray
pubDatetime: 2025-06-30T08:00:00.00Z
title: KubernetesのControl Planeとは？構成要素と役割をわかりやすく解説
postSlug:
featured: true
tags:
  - kubernetes
description: Kubernetesクラスタを制御する中核コンポーネント群『Control Plane』の各要素（API Server、Scheduler、Controller Manager、etcd）の役割と通信の流れを整理して解説します。
---

## 質問

Kubernetesにおける「Control Plane」とは何を指し、どのようなコンポーネントで構成されているのですか？  
それぞれの役割も教えてください。

---

## ✅ 回答：**Control PlaneはKubernetesクラスタの“頭脳”**

Control Plane は Kubernetes クラスタ全体の制御と状態管理を担う中心的なコンポーネント群です。  
ユーザーのリクエストに応じて「いつ・どこで・どうやってPodを動かすか」などを判断します。

---

## 🧠 Control Planeを構成する主なコンポーネント

| コンポーネント             | 主な役割                                                     |
| -------------------------- | ------------------------------------------------------------ |
| `kube-apiserver`           | KubernetesのREST APIを提供。すべての操作の入口               |
| `etcd`                     | クラスタの状態（構成、Pod情報など）を保存するKey-Valueストア |
| `kube-scheduler`           | Podの実行場所（ノード）を決定                                |
| `kube-controller-manager`  | クラスタの状態をDesired Stateに保つコントローラー群を実行    |
| `cloud-controller-manager` | クラウド依存の操作（例：LB作成、ノード管理）を分離・実行     |

---

## 🔁 連携の流れ（例：Pod作成）

1. ユーザーが kubectl apply でPodを作成
   ↓
2. kube-apiserver がリクエストを受け取り、etcd に保存
   ↓
3. kube-scheduler が未割り当てのPodを検知し、実行ノードを選定
   ↓
4. kube-controller-manager がPod作成をNodeに指示
   ↓
5. Kubelet（Worker Node側）が実際にPodを起動

⸻

🏗️ 各コンポーネントの詳細

📍 1. kube-apiserver - REST APIの提供 - リクエストの認証・認可・検証・Admission処理を実施 - etcd との通信を担当

📍 2. etcd - Kubernetesの状態を保存（永続化）- 高可用性を実現するためにRaftアルゴリズムを使用

📍 3. kube-scheduler - Podに対して適切なノードを選択 - リソースの空き、Affinity、Taintsなどを考慮

📍 4. kube-controller-manager

複数のコントローラーを管理し、状態を維持

例：- Node Controller：ノード状態の監視 - Replication Controller：ReplicaSetの数の維持 - Endpoints Controller：Serviceのエンドポイント管理

📍 5. cloud-controller-manager（オプション）- クラウドプロバイダと連携するコントローラー群（GCP, AWS, etc.）- ノードの追加/削除、ロードバランサーの作成など

⸻

🏢 Control PlaneとWorker Nodeの違い

```
項目	Control Plane	Worker Node
主な役割	クラスタの制御	実際にPodを実行
代表コンポーネント	API Server, Scheduler, Controller	kubelet, kube-proxy, Container Runtime
管理対象	全体の状態・スケジューリング・制御	各ノード上のPod運用
```

⸻

✅ まとめ

```
用語	説明
Control Plane	Kubernetesクラスタを制御・管理する中心的な仕組み
コンポーネント	API Server, etcd, Scheduler, Controller Managerなど
主な役割	リソース管理、状態監視、スケジューリング、指令出し
対比	Worker Nodeは実行部隊、Control Planeは司令塔
```

⸻

関連リンク

- Kubernetes公式：Control Plane Components
- etcdとは何か
- Kubernetes Schedulerのドキュメント
