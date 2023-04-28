### configMap 생성

- rest-board-configmap.yaml

``` yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: rest-board-config
data:
  DB_HOST: "rest-board-db-dns.default.svc.cluster.local"
  DB_USER: [ DB USER ]
  DB_PASSWORD: [ DB PASSWORD ]
  DB_NAME: [ DB NAME]
  DB_PORT: [ DB PORT ]
```

### ExternalName 수정 

- rest-board-externalname.yaml
``` yaml
apiVersion: v1
kind: Service
metadata:
  name: rest-board-db-dns
spec:
  type: ExternalName
  externalName: [ 실제 DB 주소 ]
```


## 배포

``` shell
kubectl create -f rest-board-configmap.yaml
kubectl create -f rest-board-externalname.yaml
kubectl create -f rest-board-nodeport.yaml
kubectl create -f rest-board-deployment.yaml
```
