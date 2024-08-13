KUBECTL := kubectl
ISTIODIR := istio-1.22.2
ISTIOCTL := $(ISTIODIR)/bin/istioctl
WORKLOAD_NS := workload


install-gw-api:
	$(KUBECTL) get crd gateways.gateway.networking.k8s.io &> /dev/null || \
  { $(KUBECTL) kustomize "github.com/kubernetes-sigs/gateway-api/config/crd?ref=v1.1.0" | $(KUBECTL) apply -f -; }

download-istio:
	curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.22.2 TARGET_ARCH=x86_64 sh -

install-istio:
	$(ISTIOCTL) install -f $(ISTIODIR)/samples/bookinfo/demo-profile-no-gateways.yaml -y

create-workload-ns:
	$(KUBECTL) create ns $(WORKLOAD_NS)

deploy-sample-app:
	$(KUBECTL) -n $(WORKLOAD_NS) apply -f $(ISTIODIR)/samples/bookinfo/platform/kube/bookinfo.yaml

create-gtw-resources:
	$(KUBECTL) -n $(WORKLOAD_NS) apply -f $(ISTIODIR)/samples/bookinfo/gateway-api/bookinfo-gateway.yaml



remove-gtw-resources:
	$(KUBECTL) -n $(WORKLOAD_NS) delete -f $(ISTIODIR)/samples/bookinfo/gateway-api/bookinfo-gateway.yaml

remove-sample-app:
	$(KUBECTL) -n $(WORKLOAD_NS) delete -f $(ISTIODIR)/samples/bookinfo/platform/kube/bookinfo.yaml

remove-workload-ns:
	$(KUBECTL) delete ns $(WORKLOAD_NS)

remove-istio:
	$(ISTIOCTL) uninstall -f $(ISTIODIR)/samples/bookinfo/demo-profile-no-gateways.yaml -y

remove-gw-api:
	$(KUBECTL) kustomize "github.com/kubernetes-sigs/gateway-api/config/crd?ref=v1.1.0" | $(KUBECTL) delete -f -




apply: install-gw-api download-istio install-istio create-workload-ns deploy-sample-app create-gtw-resources

destroy: remove-gw-api remove-sample-app remove-workload-ns remove-istio remove-gw-api 