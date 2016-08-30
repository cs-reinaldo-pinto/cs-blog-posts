# TESTE CERTIFICACAO


```shell
mem=$(ps -C sshd -O rss | \
        gawk '{ count ++ ; sum += $2 }; \
        END { count --; print sum/1024 ;};')
```

```shell
instance_id=$(curl -s -w '\n' \
        http://169.254.169.254/latest/meta-data/instance-id)
```
