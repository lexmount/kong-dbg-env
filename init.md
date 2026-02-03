
## 创建账户
```SQL
create database  k8s_kong_dbg;
\c k8s_kong_dbg;

CREATE USER k8s_kong_dbg_user WITH PASSWORD 'qYs21KT62BqyMGeW70U9';
GRANT ALL PRIVILEGES ON DATABASE k8s_kong_dbg TO k8s_kong_dbg_user;
GRANT ALL ON SCHEMA public TO k8s_kong_dbg_user;
```

## 连接数据库
```bash
psql -h 10.2.62.142 -p 5432 -U k8s_kong_dbg_user -d k8s_kong_dbg
```

# kube port forward
```bash
kubectl port-forward --address 0.0.0.0 -n system-dbg svc/kong-admin 8002:8002
kubectl port-forward --address 0.0.0.0 -n system-dbg svc/kong-admin 8001:8001
```


### cli相关
清理所有数据重新bootstrap
```bash
kong migrations reset
kong migrations bootstrap
```
### api相关

#### 列出所有service

```bash
curl http://kong-admin.system-dbg.svc.cluster.local:8001/services
```

#### 列出所有plugin
```bash
curl http://kong-admin.system-dbg.svc.cluster.local:8001/plugins
```