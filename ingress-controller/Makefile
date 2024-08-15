KUBECTL := kubectl
ISTIODIR := istio-1.22.2
ISTIOCTL := $(ISTIODIR)/bin/istioctl
WORKLOAD_NS := workload
INFRASTRUCTURE_NS := infrastructure

download-istio:
	curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.22.2 TARGET_ARCH=x86_64 sh -

install-istio-ingress:
	$(ISTIOCTL) install -f ./istio-gateway.yaml -y

create-workload-ns:
	$(KUBECTL) create ns $(WORKLOAD_NS)

deploy-workload:
	$(KUBECTL) -n $(WORKLOAD_NS) apply -f $(ISTIODIR)/samples/bookinfo/platform/kube/bookinfo.yaml

create-istio-ingress-resources:
	$(KUBECTL) -n $(WORKLOAD_NS) apply -f $(ISTIODIR)/samples/bookinfo/platform/kube/bookinfo-ingress.yaml

remove-istio-ingress-resources:
	$(KUBECTL) -n $(WORKLOAD_NS) delete -f $(ISTIODIR)/samples/bookinfo/platform/kube/bookinfo-ingress.yaml

remove-istio-ingress:
	$(ISTIOCTL) uninstall -f $(ISTIODIR)/samples/bookinfo/demo-profile-no-gateways.yaml -y

remove-workload:
	$(KUBECTL) -n $(WORKLOAD_NS) delete -f $(ISTIODIR)/samples/bookinfo/platform/kube/bookinfo.yaml

remove-workload-ns:
	$(KUBECTL) delete ns $(WORKLOAD_NS)


apply: download-istio install-istio-ingress create-workload-ns deploy-workload create-istio-ingress-resources

destroy: remove-istio-ingress-resources remove-workload remove-workload-ns remove-istio-ingress