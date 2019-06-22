```
docker run -itd --rm --name go-gcp --mount type=bind,src=$(pwd)/go-functions,dst=/go/src/go-functions docker-go-gcp_go-gcp /bin/sh
docker exec -it go-gcp sh
docker stop go-gcp && docker rm go-gcp
```

export GOOGLE_APPLICATION_CREDENTIALS = my.json

GCPへの認証は下記の2タイプあります。
  - Authorization Code (User Account)
  - JWT Bearer (Service Account)

|            | Cloud SDK | Server Application |
|:-----------|------------:|:------------:|
| User Account | 1.gcloud auth login | 3.gcloud auth application-default login |
| Service Account | 2.gcloud auth active-serice-account | 4.Application Default Credentials |

#Cloud SDKの利用
## 1.gmail accountでのログインUser Account-gmail-)
```GCP
gcloud auth login --no-launch-browser
gsutil ls
```

## 2.service accountでのログイン(gsutilの利用まで)
```GCP
gcloud auth activate-service-account [SA-NAME]@[PROJECT-ID].iam.gserviceaccount.com --key-file ./my.json --project ck-how-2-use
gcloud auth list
gsutil ls
```

## accountの変更
```GCP
gcloud auth list
gcloud config set account [変更対象アカウント]
```

# 3.Server Application
## gcloud auth application-default login(User Account-gmail-)
```GCP
gcloud auth application-default login
```
## 4.Application Default Credentials(Service Account)
下記のルールに従うこと。(おすすめは１を利用した管理かな。。。)
  1.環境変数(GOOGLE_APPLICATION_CREDENTIALS)のパスにあるService Accountを探す
  2.なければ ~/.config/gcloud/application_default_credentials.jsonを探す
  3.なければ環境ごとの個別のやり方で探す (例: GAE なら App Identity を使う, GCE なら Metadata Server を使う)


## cloud functions
```GCP
export GO111MODULE=on
go mod init

gcloud functions deploy HelloWorldDocker --runtime go111 --trigger-http
```