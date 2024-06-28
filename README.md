# kubectl-tokensshtunnel

## Installation

To install it you just need to copy `kubectl-tokensshtunnel` anywhere within your `PATH` with execution permissions.

## Configuration

The script supports the following command-line options:

- `-c <ssh command>`: Set the SSH command to use. This is the command used to establish an SSH connection to the remote server.
- `-k <kube config>` (optional): Set the remote kube config file location. Default: `/etc/rancher/k3s/k3s.yaml`.
- `-L <ssh tunnel>` (optional): Set the SSH tunnel configuration. The format is `[<local_bind>:]<local_port>:<remote_host>:<remote_port>`. Use this option to forward a local port to the remote Kubernetes API server.
- `-s` (optional): Add `sudo` to the SSH command. Use this option if `sudo` access is required for the SSH connection.
- `-t <tmp pattern>` (optional): Set the location to store the cached credentials. This is the location where the generated Kubernetes config file will be stored.
- `-d <tunnel duration>` (optional): Set the duration for which the SSH tunnel will be available. Specify the duration in a format compatible with the `date` command. Default: 1 hour.

## Kubeconfig

To configure your kubeconfig file, add the following configuration to the users section, update accordingly to your needs:

```
- name: sshtunnel
  user:
    exec:
      apiVersion: client.authentication.k8s.io/v1beta1
      args:
      - tokensshtunnel
      - -c
      - ssh bastion
      - -s
      - -L
      - 127.0.0.1:7443:127.0.0.1:6443
      - -T
      - /etc/rancher/k3s/k3s.yaml
      command: kubectl
      env: null
      interactiveMode: IfAvailable
      provideClusterInfo: false
```
