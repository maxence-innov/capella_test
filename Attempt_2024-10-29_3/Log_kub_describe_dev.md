## `kubectl describe pod dev-backend-649d7964c9-s2c65`

```bash
user@machine:~/capella-collab-manager$ kubectl describe pod dev-backend-649d7964c9-s2c65   
Name:             dev-backend-649d7964c9-s2c65
Namespace:        collab-manager
Priority:         0
Service Account:  dev-backend
Node:             k3d-collab-cluster-server-0/172.19.0.4
Start Time:       Tue, 29 Oct 2024 16:46:15 +0100
Labels:           id=dev-deployment-backend
                  pod-template-hash=649d7964c9
Annotations:      checksum/config-backend: 34507fe48746744a8bf0cc7ccdb6c442ff329f8e57994baef9d0d57095b6f428
                  checksum/config-promtail: dd348929d67fcb6414b328992fde988c74864b4c06df7401e29273ddc745f3b2
Status:           Running
IP:               10.42.0.36
IPs:
  IP:           10.42.0.36
Controlled By:  ReplicaSet/dev-backend-649d7964c9
Containers:
  dev-backend:
    Container ID:   containerd://5aed72fbf0c760d6f81600e13dc1831b240443021f481f204d3100f2a97fe326
    Image:          ghcr.io/dsd-dbs/capella-collab-manager/backend:v4.10.0
    Image ID:       ghcr.io/dsd-dbs/capella-collab-manager/backend@sha256:1a1adb676ee1c9c7edf8817288c0685b296629b85724f568a21d3ccc40ead1c4
    Port:           8000/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 29 Oct 2024 16:47:28 +0100
    Ready:          True
    Restart Count:  0
    Limits:
      cpu:                250m
      ephemeral-storage:  2Gi
      memory:             500Mi
    Requests:
      cpu:                60m
      ephemeral-storage:  1Gi
      memory:             20Mi
    Environment:
      OAUTHLIB_INSECURE_TRANSPORT:  1
      CLUSTER_DEVELOPMENT_MODE:     1
      no_proxy_additional:          
    Mounts:
      /.local/share/capellacollab from data (rw)
      /etc/capellacollab from config (ro)
      /var/log/backend from logs (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-f9rln (ro)
  promtail:
    Container ID:  containerd://b80baee3f9d9f86df4605107bc3e8b43b7c1e4abb07b2ba02cfcf6938e5ec1e5
    Image:         docker.io/grafana/promtail
    Image ID:      docker.io/grafana/promtail@sha256:47c3488971ca1e115df050835882399044fbd7c89f3970ae6f8ee8e713774302
    Port:          3101/TCP
    Host Port:     0/TCP
    Args:
      --config.file=/etc/promtail/promtail.yaml
      -log-config-reverse-order
    State:          Running
      Started:      Tue, 29 Oct 2024 16:47:29 +0100
    Ready:          True
    Restart Count:  0
    Limits:
      cpu:                100m
      ephemeral-storage:  2Gi
      memory:             50Mi
    Requests:
      cpu:                20m
      ephemeral-storage:  1Gi
      memory:             5Mi
    Environment:          <none>
    Mounts:
      /etc/promtail from prom-config (rw)
      /var/log/backend from logs (ro)
      /var/log/promtail from prom-position (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-f9rln (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       True 
  ContainersReady             True 
  PodScheduled                True 
Volumes:
  config:
    Type:      ConfigMap (a volume populated by a ConfigMap)
    Name:      dev-backend
    Optional:  false
  data:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  dev-backend-data
    ReadOnly:   false
  logs:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
  prom-config:
    Type:      ConfigMap (a volume populated by a ConfigMap)
    Name:      dev-promtail
    Optional:  false
  prom-position:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  dev-backend-promtail
    ReadOnly:   false
  kube-api-access-f9rln:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason                           Age                 From               Message
  ----     ------                           ----                ----               -------
  Normal   Scheduled                        31m                 default-scheduler  Successfully assigned collab-manager/dev-backend-649d7964c9-s2c65 to k3d-collab-cluster-server-0
  Normal   Pulling                          31m                 kubelet            Pulling image "ghcr.io/dsd-dbs/capella-collab-manager/backend:v4.10.0"
  Normal   Pulled                           30m                 kubelet            Successfully pulled image "ghcr.io/dsd-dbs/capella-collab-manager/backend:v4.10.0" in 1m11.38s (1m11.38s including waiting)
  Normal   Created                          30m                 kubelet            Created container dev-backend
  Normal   Started                          30m                 kubelet            Started container dev-backend
  Normal   Pulling                          30m                 kubelet            Pulling image "docker.io/grafana/promtail"
  Normal   Pulled                           30m                 kubelet            Successfully pulled image "docker.io/grafana/promtail" in 832ms (832ms including waiting)
  Normal   Created                          30m                 kubelet            Created container promtail
  Normal   Started                          30m                 kubelet            Started container promtail
  Warning  FailedToRetrieveImagePullSecret  45s (x25 over 31m)  kubelet            Unable to retrieve some image pull secrets (test); attempting to pull the image may not succeed.
```