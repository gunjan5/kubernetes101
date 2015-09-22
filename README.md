- Run etcd:

- docker run --net=host -d gcr.io/google_containers/etcd:2.0.9 /usr/local/bin/etcd --addr=127.0.0.1:4001 --bind-addr=0.0.0.0:4001 --data-dir=/var/etcd/data

- Run master:

- docker run --net=host -d -v /var/run/docker.sock:/var/run/docker.sock  gcr.io/google_containers/hyperkube:v0.21.2 /hyperkube kubelet --api_servers=http://localhost:8080 --v=2 --address=0.0.0.0 --enable_server --hostname_override=127.0.0.1 --config=/etc/kubernetes/manifests

- Run proxy service:

- docker run -d --net=host --privileged gcr.io/google_containers/hyperkube:v0.21.2 /hyperkube proxy --master=http://127.0.0.1:8080 --v=2

- SSH into boot2docker:

- boot2docker ssh -L8080:localhost:8080

- deploy replicas:
-
kubectl create -f output/



- scale up/down replicas:
-
kubectl scale rc NAME --replicas=COUNT \
-     [--current-replicas=COUNT] \
-     [--resource-version=VERSION]



-
- kubectl get rc
- start service: kubectl create -f service.yaml
- kubectl get services
- curl <service IP>/path/to/html
