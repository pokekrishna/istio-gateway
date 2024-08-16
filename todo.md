TGT
[ ] private ip association
[ ] L4 TCP load balancing (no ssl termination)
[ ] CLB Specs to expose Istio GW as ingress controller 
[ ] CLB specs to expose Istio GW as Gateway controller
[ ] Limits and Quota analysis for Tencent Cloud and CLB
[ ] Health check configuration
[ ] cross region access through CLB
[ ] cross zone load balacing 
[ ] O11y form CLB to Lens (using cloud managed prometheus)
[ ] multi AZ load balancer proxy presence
---
Tasks
[x] make destroy
[x] delete istio-system ns
[x] install istio gateway as gtw controller
[x] install dummy http service and ingress
[x] curl and access the service through cluster ip
[x] curl and access the service through ingress gtw
[x] send traffic through load balancer endpoint

[x] add allow by default annotation
[x] add security group annotation

[ ] add spsec for clb istance
[ ] add spec for clb listener
[ ] add spec for health check


[ ] install dummy h2c grpc service
[ ] install dummy https app and ssl termination on ingress gtw
[ ] cross zone load balacing 
[ ] Health check configuration
[ ] cross region access through CCN
---