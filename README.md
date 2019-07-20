# k3d-on-docker

```

                        ##         .
                  ## ## ##        ==
               ## ## ## ## ##    ===
           /"""""""""""""""""\___/ ===
      ~~~ {~~ ~~~~ ~~~ ~~~~ ~~~ ~ /  ===- ~~~
           \______ o           __/
             \    \         __/
              \____\_______/


docker is configured to use the default machine with IP 192.168.99.104
For help getting started, check out the docs at https://docs.docker.com

Biradars-Air-4:~ sangam$ k3d
NAME:
   k3d - Run k3s in Docker!

USAGE:
   k3d [global options] command [command options] [arguments...]

VERSION:
   v1.2.2

AUTHORS:
   Thorsten Klein <iwilltry42@gmail.com>
   Rishabh Gupta <r.g.gupta@outlook.com>
   Darren Shepherd

COMMANDS:
     check-tools, ct  Check if docker is running
     shell            Start a subshell for a cluster
     create, c        Create a single- or multi-node k3s cluster in docker containers
     delete, d, del   Delete cluster
     stop             Stop cluster
     start            Start a stopped cluster
     list, ls, l      List all clusters
     get-kubeconfig   Get kubeconfig location for cluster
     help, h          Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --verbose      Enable verbose output
   --help, -h     show help
   --version, -v  print the version
Biradars-Air-4:~ sangam$ k3d create 
2019/07/21 03:40:41 Created cluster network with ID db592e60d27228db7bbd3a29a1a54074e08884910fedb537901d1b31c41a0aea
2019/07/21 03:40:41 Add TLS SAN for 192.168.99.104
2019/07/21 03:40:41 Creating cluster [k3s-default]
2019/07/21 03:40:41 Creating server using docker.io/rancher/k3s:v0.5.0...
2019/07/21 03:40:41 Pulling image docker.io/rancher/k3s:v0.5.0...
2019/07/21 03:41:04 SUCCESS: created cluster [k3s-default]
2019/07/21 03:41:04 You can now use the cluster with:

export KUBECONFIG="$(k3d get-kubeconfig --name='k3s-default')"
kubectl cluster-info
Biradars-Air-4:~ sangam$ export KUBECONFIG="$(k3d get-kubeconfig --name='k3s-default')"
Biradars-Air-4:~ sangam$ kubectl cluster-info
Kubernetes master is running at https://192.168.99.104:6443
CoreDNS is running at https://192.168.99.104:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
Biradars-Air-4:~ sangam$ kubectl get node
NAME                     STATUS   ROLES    AGE   VERSION
k3d-k3s-default-server   Ready    <none>   87s   v1.14.1-k3s.4
Biradars-Air-4:~ sangam$ kubectl get pods --all-namespaces 
NAMESPACE     NAME                         READY   STATUS             RESTARTS   AGE
kube-system   coredns-695688789-d86pm      1/1     Running            1          2m50s
kube-system   helm-install-traefik-xnsdd   0/1     CrashLoopBackOff   4          2m51s 
Biradars-Air-4:~ sangam$ kubectl run mynginx --image=nginx --replicas=3 --port=80
kubectl run --generator=deployment/apps.v1 is DEPRECATED and will be removed in a future version. Use kubectl run --generator=run-pod/v1 or kubectl create instead.
deployment.apps/mynginx created 
Biradars-Air-4:~ sangam$ kubectl get po
NAME                       READY   STATUS    RESTARTS   AGE
mynginx-74bc69fc95-79nmx   1/1     Running   0          42s
mynginx-74bc69fc95-brtqs   1/1     Running   0          42s
mynginx-74bc69fc95-zkrcd   1/1     Running   0          42s
Biradars-Air-4:~ sangam$ kubectl expose deployment mynginx --port 80
service/mynginx exposed
Biradars-Air-4:~ sangam$ kubectl get endpoints mynginx
NAME      ENDPOINTS                                AGE
mynginx   10.42.0.4:80,10.42.0.5:80,10.42.0.6:80   24s
Biradars-Air-4:~ sangam$ curl 10.42.0.4:80
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

Biradars-Air-4:~ sangam$ k3d d
2019/07/21 04:13:24 Removing cluster [k3s-default]
2019/07/21 04:13:24 ...Removing server
2019/07/21 04:13:25 SUCCESS: removed cluster [k3s-default]
Biradars-Air-4:~ sangam$ 


```
