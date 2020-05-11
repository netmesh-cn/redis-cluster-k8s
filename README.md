# 使用
* 生成StatefulSet：`kubectl create -f redis-sts.yaml`
* 生成Service：`kubectl create -f redis-svc.yaml`
* 启动redis集群：`kubectl exec -it redis-cluster-0 -- redis-cli --cluster create --cluster-replicas 1 $(kubectl get pods -l app=redis-cluster -o jsonpath='{range.items[*]}{.status.podIP}:6379 ')`  
或者手工执行  
得到所有节点ip和端口  
kubectl get pods -l app=redis-cluster -o jsonpath='{range.items[*]}{.status.podIP}:6379 '    


redis-cli --cluster create --cluster-replicas 1 172.18.66.92:6379 172.18.48.203:6379 172.18.78.157:6379 172.18.48.67:6379 172.18.148.1:6379 172.18.62.197:6379  

* 状态查看  
kubectl exec -it redis-cluster-0 redis-cli cluster nodes -n redis  

# 说明
* 需要使用`StorageClass`动态创建pv
* `StatefulSet`中的serviceName要和Service的metadata中name保持一致

