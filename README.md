# Knative-101

# Knative Install on Google Kubernetes Engine

## Installing the Google Cloud SDK and kubectl

### gcloud コマンドのインストール（Google Cloud SDK のインストール）

以下の URL から対話的インストールを実施。
https://cloud.google.com/sdk/docs/downloads-interactive

1. コマンド プロンプトで次のコマンドを入力します。

```
curl https://sdk.cloud.google.com | bash
```

2. シェルを再起動します。

```
exec -l $SHELL
```

3. gcloud init を実行して gcloud 環境を初期化します。

```
gcloud init
```

### Kubernetes のコンポーネントを GCloud にインストール

```
gcloud components install kubectl
```

![image.png (471.2 kB)](https://img.esa.io/uploads/production/attachments/3909/2018/12/30/11755/a1690902-6b1e-42f6-9318-33ad5528ce9e.png)

### GCloud へのログイン

```
gcloud auth login
```

## Setting environment variables

### 新規プロジェクトの作成

`my-knative-project`という名前の GCP プロジェクトを作成する。注意点として、GCP のプロジェクト名は全ユーザ間でユニークでなければならない。

ユニークなプロジェクト名でない場合、以下のようなエラーが発生する。

```bash
$ export PROJECT=my-knative-project
$ gcloud projects create $PROJECT --set-as-default
ERROR: (gcloud.projects.create) Project creation failed.
The project ID you specified is already in use by another project.
Please try an alternative ID.
```

自分の名前などを組み合わせて、ユニークなプロジェクト名を指定するようにする。

```bash
export PROJECT=imamachi-knative-project
gcloud projects create $PROJECT --set-as-default
```

### 作成したプロジェクトをデフォルトに設定

```bash
gcloud config set core/project $PROJECT
```

### 必要な API を有効化する

```bash
gcloud services enable \
  cloudapis.googleapis.com \
  container.googleapis.com \
  containerregistry.googleapis.com
```
