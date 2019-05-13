```
docker-compose up --build -d &&
docker exec -it docker-abridgededition_fluentd_1 /bin/sh

docker stop docker-abridgededition_fluentd_1 &&
docker rm docker-abridgededition_fluentd_1
```

----------------------------------------

```
fluentd -c ./fluentd/etc/fluentd.conf -vv &
echo '{"json":"message dayo"}' | fluent-cat apache.access
```

``` fluentd.conf
<source>
  type forward
</source>
<match apache.access>
  type file
  path /fluentd/log
</match>
```

----------------------------------------

``` fluentd.conf
<source>
  @type tail
  format none
  path /fluentd/file/tmp.log
</source>
<match apache.access>
  type file
  path /fluentd/log
</match>
```

```
fluentd -c ./fluentd/etc/fluentd.conf -vv && fluent-cat apache.access
```

```
<source>
  type tail
  format apache
  path /var/log/httpd-access.log
  tag apache.access
</source>
<match apache.access>
  type file
  path /var/log/fluent/access
</match>
```

```
fluentd -c ./fluentd/etc/fluentd.conf -vv && 
curl http://localhost/index.html -F 'json={"log":"test_dayo"}'
```
