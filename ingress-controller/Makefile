KUBECTL := kubectl
ISTIODIR := istio-1.22.2
ISTIOCTL := $(ISTIODIR)/bin/istioctl
WORKLOAD_NS := workload
INFRASTRUCTURE_NS := infrastructure

install-istio-ingress:
	$(ISTIOCTL) install -f $(ISTIODIR)/samples/bookinfo/demo-profile-no-gateways.yaml -y

create-infrastructure-ns:
	$(KUBECTL) create ns $(INFRASTRUCTURE_NS)

deploy-workload:
	$(KUBECTL) -n $(WORKLOAD_NS) apply -f $(ISTIODIR)/samples/bookinfo/platform/kube/bookinfo.yaml

create-istio-ingress-resources:
	$(KUBECTL) -n $(WORKLOAD_NS) apply -f $(ISTIODIR)/samples/bookinfo/platform/kube/bookinfo-ingress.yaml

remove-istio-ingress-resources:
	$(KUBECTL) -n $(WORKLOAD_NS) delete -f $(ISTIODIR)/samples/bookinfo/platform/kube/bookinfo-ingress.yaml

remove-istio-ingress:
	$(ISTIOCTL) uninstall -f $(ISTIODIR)/samples/bookinfo/demo-profile-no-gateways.yaml -y


apply: install-istio-ingress create-infrastructure-ns deploy-workload create-istio-ingress-resources

destroy: remove-istio-ingress-resources remove-istio-ingress