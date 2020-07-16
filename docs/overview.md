#### overview

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: private-reg
spec:
  containers:
  - name: private-reg-container
    image: <your-private-image>
  imagePullSecrets:   #增加此字段
  - name: aliyun-acr-soundbus-rd-secret
```