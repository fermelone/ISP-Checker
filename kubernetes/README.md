# ISP-Checker on Kubernetes
`ISP-Checker` was ported to run in Kubernetes (`1.18.0`) in a Raspberry Pi cluster (_It's all I have_).

<center>
<img src="../img/cluster.jpeg" width="450">
</center>

The following configuration files are used to deploy this stack in Kubernetes, they can widely improved but so far let's say it works.

> You need to update them before running in your cluster.

> ***NOTE***: The Kubernetes deployment is in *BETA* version. Don't worry if you see something wrong here.

## Installing, the quick way:

1) Apply the `ISP-Checker-deploy.yaml`
```bash
$: kubectl apply -f https://raw.githubusercontent.com/fmdlc/ISP-Checker/master/kubernetes/ISP-Checker-deploy.yaml
```

### Configuration

1) Edit `secrets.yaml` in order to initialize your InfluxDB database.
2) Edit `configmap.yaml` to configure Telegraf.
3) Apply the other `YAML` files.
4) Expose your deployment or create a LoadBalancer/IngressRule to access Grafana.

### Accesing
#### LoadBalancer
If you want to use a `LoadBalancer` to access Grafana, run:
```bash
$: kubectl expose deployments/grafana --type=LoadBalancer --name=grafana-svc
```
#### port-foward
If you can't use a LoadBalancer, you can use a `ClusterIP` service and forward to your local port.

```
$: kubectl expose deployments/grafana --type=ClusterIP --name=grafana-svc
```

And finally use your IngressController to access the service or a `port-forward`:

```
$: kubectl port-forward svc/grafana-svc 3000:3000 -n monitoring
```
