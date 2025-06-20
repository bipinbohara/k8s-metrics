# k8s-metrics

### Run bash script to log metrices to Redis
Step 1: 
```
kubectl proxy 
curl -s http://localhost:8001/api/v1/nodes/$(hostname)/proxy/stats/summary | jq
```

Step 2:
```
## to remove previous build of go programs
rm -rf go.sum
rm -rf go.mod

go mod init kube-metrics
go get github.com/go-redis/redis/v8
go get golang.org/x/net/context

## to run the program
# go run kube-metrics.go
```

Step 3:
```
export NODE_NAMES="ubuntu24-worker2,ubuntu24-worker5,ubuntu24-worker6"
./run-metrics.sh
```

Step 4:
```
redis-cli
> keys *
```

To see logs of individual containers
```
ZRANGE util:<pod>:<container> 0 -1 WITHSCORES
```

#### To delete db records
```
redisc-cli
> flushall
```
