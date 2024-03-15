# 自動化準備全離線安裝包

## 描述

可自動化準備指定的產品及對應的版本，包含 Harbor、Rancher Kubernetes Engine 2 ( RKE2 )、Rancher、Neuvector 和 K3S 全離線安裝所需的檔案和 Container Images。
全離線安裝所需的檔案和 Container Images 會被壓縮成一個壓縮檔，並儲存在 `~/work/compressed_files` 目錄底下。

## Usage

```
Usage:
  ENV_VAR=... $(basename "${BASH_SOURCE[0]}") [options]

Available options:

all        一次準備 Harbor、RKE2、Rancher 的全離線安裝包
harbor     只準備 Harbor 的全離線安裝包
rke2       只準備 RKE2 的全離線安裝包
rancher    只準備 Rancher 的全離線安裝包
neuvector  只準備 Neuvector 的全離線安裝包
k3s        只準備 K3S 的全離線安裝包

Environment variables:

   - Harbor_Version
     定義 Harbor 的版本
     預設是 'v2.10.0'。

   - Docker_Compose_Version
     定義 docker-compose 的版本
     預設是 'v2.24.7'。

   - RKE2_Version
     定義 RKE2 的版本
     預設是 'v1.27.11'。

   - Rancher_Version
     定義 Rancher 的版本
     預設是 'v2.8.2'。

   - Helm_Version
     定義 Helm 的版本
     預設是 'v3.14.2'。

   - Cert_Manager_Version
     定義 Cert-manager 的版本
     預設是 'v1.11.0'。

   - K3S_Version
     定義 K3S 的版本
     預設是 'v1.27.11'。

   - Neuvector_Version
     定義 Neuvector 的版本
     預設是 '5.3.0'。

   - Private_Registry_Name
     定義企業內部私有 Image Registry 的名稱
     預設是 'harbor.example.com'。

   - Command_log_file
     將命令執行後的輸出重新導向到 /tmp/prepare_message.log
     預設是 '/tmp/prepare_message.log'。

   - Command_Output_log_file
     將命令執行後的輸出重新導向到 /tmp/prepare_output_message.log
     預設是 '/tmp/prepare_output_message.log'。
```

## Example:
  ### 一次準備 Harbor、RKE2、Rancher 的全離線安裝包，並且指定安裝 Harbor 特定版本
  ```
  Harbor_Version=v2.7.0 ./prepare.sh all
  ```
  ### 只準備 Rancher 的全離線安裝包，並且指定安裝 Rancher v2.7.9 版本
  ```
  Rancher_Version=v2.7.9 ./prepare.sh rancher
  ```
  ### 準備 Neuvector 的全離線安裝包，並且指定安裝 Neuvector 5.2.0 版本
  ```
  Neuvector_Version=5.2.0 ./prepare.sh neuvector
  ```

  ### 同時準備 Rancher、Harbor 和 K3S 的全離線安裝包，分別指定安裝 v2.7.9、v2.7.0 和 v1.25.9 版本，並設定私有 Image Registry 的名稱
  ```
  Rancher_Version=v2.7.9 Harbor_Version=v2.7.0 K3S_Version=v1.25.9 \
  Private_Registry_Name="antony-harbor.example.com" \
  ./prepare.sh rancher harbor k3s
  ```

## 範例目錄結構
```
~/work/
├── compressed_files
│   ├── harbor-offline-v2.10.0.tar.gz   --> Harbor v2.10.0 版本的全離線安裝包
│   ├── k3s-airgap-v1.27.11.tar.gz      --> K3S v1.27.11 版本的全離線安裝包
│   ├── neuvector-airgap-5.3.0.tar.gz   --> Neuvector 5.3.0 版本的全離線安裝包
│   └── rancher-airgap-v2.8.2.tar.gz    --> Rancher v2.8.2 版本的全離線安裝包
│   └── rke2-airgap-v1.27.11.tar.gz     --> RKE2 v1.27.11 版本的全離線安裝包
├── harbor
│   ├── v2.10.0
│   └── v2.7.0
├── k3s
│   └── v1.27.11
├── neuvector
│   └── 5.3.0
├── rancher
│   └── v2.8.2
└── rke2
    └── v1.27.11
```

## Log
### 檢視程式執行了哪些命令

```
$ tail -f /tmp/prepare_message.log
```

### 檢視程式執行命令的執行結果

```
$ tail -f /tmp/prepare_output_message.log
```


