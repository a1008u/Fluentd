```
docker build ./ -t td-bq
docker run --name test1 -it -p 24224:24224 td-bq /bin/bash
```

gcloud auth login --no-launch-browser