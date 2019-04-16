# kboom

Think of `kboom` as the Kubernetes equivalent of [boom](https://github.com/tarekziade/boom), allwoing you to create short-term load for scale-testing and long-term load for soak-testing. Supported load out of the box are namespaces, pods, services, and deployments as well as custom resource via CRDs.

Here's how you'd use `kboom` to do some scale-testing, creating 100 pods and 200 services:

```bash
$ kboom --mode=scale --load=pods:100,services:200
API Server: v1.12.6-eks-d69f1b
Ping distance: 0.540 sec
Generating 1000 pods and 200 services 
[***********************************************]

-------- Results --------
Overall pods         94 (100)    
Overall services     200 (200)

Total time pods      988 sec
p50 pods             10 sec
p90 pods             23 sec

Total time services  534 sec
p50 pods             2 sec
p90 pods             19 sec
-------------------------
```

Now let's do some soak testing:

```bash
$ kboom --mode=soak --period=200h --load=./crd-of-my-resource.yaml
```