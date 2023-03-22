# 部署过程中遇到的错误



**kubelet**:Image garbage collection failed once. Stats initialization may not have completed yet: failed to get imageFs info: unable to find data in memory cache

```
docker system prune
systemctl stop kubelet
systemctl stop docker
systemctl start docker
systemctl start kubelet
```
**calico**:Connection to the datastore is unauthorized error=connection is unauthorized: Unauthorized
```
kubectl delete -f calico.yaml
kubectl apply  -f calico.yaml
```

**calico**: hostPath type check failed: /sys/fs/bpf is not a directory"
```text
某博客记录了此错误，说是系统内核版本较低导致的，升级内核试下；
并且该博客中建议使用centos7.9,而我当前的系统版本为：CentOS Linux release 7.2.1511 (Core)
```

calio: Error syncing pod, skipping" err="failed to \"StartContainer\" for \"install-cni\" with CrashLoopBackOff: \"back-off
```text
yum install -y *rhsm*


没能解决
```

r
查看日志：

journalctl -u kubelet
journalctl -n 20 --no-pager
kubectl describe pod calico-node-rcrqb -n kube-system


kubelet启动之后果断时间挂掉，日志显示：

Failed to start ContainerManager failed to initialize top level QOS containers: failed to update top level Burstable QOS cgroup : failed to set supported cgroup subsystems for cgroup [kubepods burstable]: failed to find subsystem mount for required subsystem: pids

````
解决方法： 暂时reboot机器是有用的，后续再关注下
````

