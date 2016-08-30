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


```shell
aws cloudwatch put-metric-data \
        --namespace ServerMetrics \
        --metric-name SSHDMemUtilization \
        --dimension InstanceId=$instance_id \
        --value $mem \
        --unit "Megabytes"
```

```shell
aws cloudwatch get-metric-statistics \
       --metric-name SSHDMemUtilization \
       --start-time 2016-08-29T15:00:00 \
       --end-time 2016-08-29T19:00:00 \
       --namespace ServerMetrics 
       --dimension Name=InstanceId,Value=i-9eb16eaf \
       --period 3600 --statistics Maximum
```
