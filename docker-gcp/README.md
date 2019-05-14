```
docker-compose up --build -d && docker exec -it docker-gcp_fluentd_1 sh
```

gcloud auth login --no-launch-browser


echo "222.8.209.248 - - [2019/05/11 04:02:07 +0900] \"GET /cgi-bin/isatV2/soulberry/entryV2.cgi?rk=0100khxr00imkr&nid=h4898821214&rurl=https%3A%2F%2Fwww.soulberry.jp%2F&media=http%3A%2F%2Fotokushop234.xyz%2F2019%2F02%2F13%2Fsoulberry%25E3%2580%259C%25E3%2582%25BD%25E3%2582%25A6%25E3%2583%25AB%25E3%2583%2599%25E3%2583%25AA%25E3%2583%25BC%25E3%2580%259C%2F%3Fgclid%3DEAIaIQobChMI8dCkjNOR4gIVyQYqCh34zAwtEAAYASAAEgL55fD_BwE&atss=0100khxr00imkr-56c09a4bac41155698d433c131e6d117 HTTP/1.1\" 302 337 \"http://otokushop234.xyz/2019/02/13/soulberry%E3%80%9C%E3%82%BD%E3%82%A6%E3%83%AB%E3%83%99%E3%83%AA%E3%83%BC%E3%80%9C/?gclid=EAIaIQobChMI8dCkjNOR4gIVyQYqCh34zAwtEAAYASAAEgL55fD_BwE\" \"Mozilla/5.0 (iPhone; CPU iPhone OS 12_1_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0 Mobile/15E148 Safari/604.1\"" >> /fluentd/file/tmp.log


fluentd -c ./fluentd/etc/fluentd.conf -vv && fluent-cat example

export GOOGLE_APPLICATION_CREDENTIALS = my.json
