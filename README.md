# Istio VirtualService example for Canary Deployments

```bash
# creating resources
kubectl -n development apply -f client-deployment.yaml
kubectl -n development apply -f service.yaml
kubectl -n development apply -f server1-deployment.yaml
kubectl -n development apply -f server2-deployment.yaml
kubectl -n development apply -f virtualservice.yaml
kubectl -n development apply -f destinationrule.yaml

# server monitoring
kubectl -n development logs -f deployment/service-v1
kubectl -n development logs -f deployment/service-v2

# running a client
kubectl -n development exec deployment/client -it -- sh -c 'for i in $(seq 50); do printf "This is a very long message $i\n" | nc -q0 -w10 service.development.svc.cluster.local 8888; done'
```