# kubectl-tokensshtunnel


```
- name: sshtunnel
  user:
    exec:
      apiVersion: client.authentication.k8s.io/v1beta1
      args:
      - tokensshtunnel
      - -c
      - awstools ec2 ssh bastion
      - -s
      - -L
      - 127.0.0.1:7443:127.0.0.1:6443
      command: kubectl
      env: null
      interactiveMode: IfAvailable
      provideClusterInfo: false
```