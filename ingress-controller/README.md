CLUSTER IP
```sh
    kubectl -n default run --rm -it --restart=Never --image=curlimages/curl tmp -- --max-time 3 -iv -- $(kubectl -n infrastructure get svc istio-ingressgateway -o jsonpath='{.spec.clusterIP}'):80/productpage
```


EXTERNAL IP
```sh
    kubectl -n default run --rm -it --restart=Never --image=curlimages/curl tmp -- --max-time 3 -iv -- $(kubectl -n infrastructure get svc istio-ingressgateway -o jsonpath='{.status.loadBalancer.ingress[0].ip}'):80/productpage
```
