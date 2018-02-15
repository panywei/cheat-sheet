### Account
gcloud auth list : Show active Credentialed Accounts.  
gcloud config set account `ACCOUNT` : Set the active account

### Project
gcloud config list project  
gcloud config set project <PROJECT_ID>  
gcloud config set compute/zone [us-central1-f](https://cloud.google.com/compute/docs/regions-zones/)  


### Cluster
gcloud container clusters create \<cluster-name\> --enable-kubernetes-alpha --machine-type=n1-standard-2 --num-nodes=4 --zone=\<zone\> --no-enable-legacy-authorization --cluster-version=1.9.1-gke.0 --project \<project-name\>   
gcloud container clusters get-credentials \<cluster-name\> --zone \<zone\> --project \<project-name\>  
gcloud compute instances list  
gcloud container clusters delete \<cluster-name\>
  
### Kubectl    
kubectl get [(-o|--output=)json|yaml|wide|custom-columns=...|custom-columns-file=...|go-template=...|go-template-file=...|jsonpath=...|jsonpath-file=...] (TYPE [NAME | -l label] | TYPE/NAME ...) [flags] [options]  
kubectl get deployment|ingress|namespace|nodes|pod|pods|services --all-namespaces -o wide istio-injection=enabled     
kubectl get pods -n namespaceName -l "app=monolith,secure=enabled" --show-labels   
kubectl run nginx --image=nginx:1.10.0
kubectl expose deployment nginx --port 80 --type LoadBalancer
kubectl api-versions | grep admissionregistration
kubectl label namespace default istio-injection=enabled
kubectl label pods secure-monolith 'secure=enabled'
kubectl port-forward $(kubectl get pod -l app=servicegraph -o jsonpath='{.items[0].metadata.name}') 8088:8088 &
kubectl describe services monolith | grep Endpoints

# Minikube
minikube start \
	--extra-config=controller-manager.ClusterSigningCertFile="/var/lib/localkube/certs/ca.crt" \
	--extra-config=controller-manager.ClusterSigningKeyFile="/var/lib/localkube/certs/ca.key" \
	--extra-config=apiserver.Admission.PluginNames=NamespaceLifecycle,LimitRanger,ServiceAccount,PersistentVolumeLabel,DefaultStorageClass,DefaultTolerationSeconds,MutatingAdmissionWebhook,ValidatingAdmissionWebhook,ResourceQuota \
	--kubernetes-version=v1.9.0  
source <(minikube completion bash) # shell completion	
minikube config get/set/unset/view    


### Istio
istioctl create|replace -f samples/bookinfo/kube/route-rule-all-v1.yaml
istioctl get routerules -o yaml  
istioctl kube-inject -f samples/bookinfo/kube/bookinfo.yaml
