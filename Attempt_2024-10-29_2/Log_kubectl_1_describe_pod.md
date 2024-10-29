## `kubectl describe pod dev-backend-79bdf87454-kmdmc`

```bash
user@machine:~/capella-collab-manager$ kubectl describe pod dev-backend-79bdf87454-kmdmc
Name:             dev-backend-79bdf87454-kmdmc
Namespace:        collab-manager
Priority:         0
Service Account:  dev-backend
Node:             k3d-collab-cluster-server-0/172.19.0.4
Start Time:       Tue, 29 Oct 2024 15:54:26 +0100
Labels:           id=dev-deployment-backend
                  pod-template-hash=79bdf87454
Annotations:      checksum/config-backend: 34507fe48746744a8bf0cc7ccdb6c442ff329f8e57994baef9d0d57095b6f428
                  checksum/config-promtail: dd348929d67fcb6414b328992fde988c74864b4c06df7401e29273ddc745f3b2
Status:           Running
IP:               10.42.0.36
IPs:
  IP:           10.42.0.36
Controlled By:  ReplicaSet/dev-backend-79bdf87454
Containers:
  dev-backend:
    Container ID:   containerd://ff72d5918a7e59089d22864ac1f9e37f76170a98ab55f8b556c5ee8c7a6b2f51
    Image:          ghcr.io/dsd-dbs/capella-collab-manager/backend:v4.10.0
    Image ID:       ghcr.io/dsd-dbs/capella-collab-manager/backend@sha256:1a1adb676ee1c9c7edf8817288c0685b296629b85724f568a21d3ccc40ead1c4
    Port:           8000/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 29 Oct 2024 15:57:07 +0100
    Last State:     Terminated
      Reason:       Error
      Exit Code:    137
      Started:      Tue, 29 Oct 2024 15:55:45 +0100
      Finished:     Tue, 29 Oct 2024 15:57:06 +0100
    Ready:          False
    Restart Count:  1
    Limits:
      cpu:                250m
      ephemeral-storage:  2Gi
      memory:             500Mi
    Requests:
      cpu:                60m
      ephemeral-storage:  1Gi
      memory:             20Mi
    Liveness:             http-get http://:http/healthcheck delay=30s timeout=1s period=10s #success=1 #failure=3
    Readiness:            http-get http://:http/healthcheck delay=0s timeout=1s period=10s #success=1 #failure=3
    Environment:
      OAUTHLIB_INSECURE_TRANSPORT:  1
      CLUSTER_DEVELOPMENT_MODE:     1
      no_proxy_additional:          
    Mounts:
      /.local/share/capellacollab from data (rw)
      /etc/capellacollab from config (ro)
      /var/log/backend from logs (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-m779p (ro)
  promtail:
    Container ID:  containerd://d7b68a676fb87e18ca3f8a11e394c32ebfa28610fc492976c14665df63fbda3b
    Image:         docker.io/grafana/promtail
    Image ID:      docker.io/grafana/promtail@sha256:47c3488971ca1e115df050835882399044fbd7c89f3970ae6f8ee8e713774302
    Port:          3101/TCP
    Host Port:     0/TCP
    Args:
      --config.file=/etc/promtail/promtail.yaml
      -log-config-reverse-order
    State:          Running
      Started:      Tue, 29 Oct 2024 15:55:46 +0100
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
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-m779p (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
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
  kube-api-access-m779p:
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
  Type     Reason                           Age                  From               Message
  ----     ------                           ----                 ----               -------
  Normal   Scheduled                        3m18s                default-scheduler  Successfully assigned collab-manager/dev-backend-79bdf87454-kmdmc to k3d-collab-cluster-server-0
  Normal   Pulling                          3m17s                kubelet            Pulling image "ghcr.io/dsd-dbs/capella-collab-manager/backend:v4.10.0"
  Normal   Pulling                          119s                 kubelet            Pulling image "docker.io/grafana/promtail"
  Normal   Pulled                           119s                 kubelet            Successfully pulled image "ghcr.io/dsd-dbs/capella-collab-manager/backend:v4.10.0" in 1m17.266s (1m17.267s including waiting)
  Normal   Created                          119s                 kubelet            Created container dev-backend
  Normal   Started                          119s                 kubelet            Started container dev-backend
  Normal   Pulled                           118s                 kubelet            Successfully pulled image "docker.io/grafana/promtail" in 1.514s (1.514s including waiting)
  Normal   Created                          118s                 kubelet            Created container promtail
  Normal   Started                          118s                 kubelet            Started container promtail
  Warning  FailedToRetrieveImagePullSecret  68s (x4 over 3m18s)  kubelet            Unable to retrieve some image pull secrets (test); attempting to pull the image may not succeed.
  Warning  Unhealthy                        68s (x3 over 88s)    kubelet            Liveness probe failed: Get "http://10.42.0.36:8000/healthcheck": dial tcp 10.42.0.36:8000: connect: connection refused
  Normal   Killing                          68s                  kubelet            Container dev-backend failed liveness probe, will be restarted
  Warning  Unhealthy                        58s (x9 over 117s)   kubelet            Readiness probe failed: Get "http://10.42.0.36:8000/healthcheck": dial tcp 10.42.0.36:8000: connect: connection refused
```