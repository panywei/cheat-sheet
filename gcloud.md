### Account
gcloud auth list : Show active Credentialed Accounts.  
gcloud config set account `ACCOUNT` : Set the active account

### Project
gcloud config list project  
gcloud config set project <PROJECT_ID>  
gcloud config set compute/zone [northamerica-northeast1-c](https://cloud.google.com/compute/docs/regions-zones/)  


### cluster
gcloud container clusters create \<cluster-name\> --enable-kubernetes-alpha --machine-type=n1-standard-2 --num-nodes=4 --zone=\<zone\> --no-enable-legacy-authorization --cluster-version=1.9.1-gke.0 --project \<project-name\>   
gcloud container clusters get-credentials \<cluster-name\> --zone \<zone\> --project \<project-name\>  
  
### Kubectl    
kubectl get deployment|ingress|namespace|nodes|pod|pods|services --all-namespaces -o wide istio-injection=enabled     
kubectl delete pod  
kubectl api-versions | grep admissionregistration
kubectl label namespace default istio-injection=enabled

minikube start \
	--extra-config=controller-manager.ClusterSigningCertFile="/var/lib/localkube/certs/ca.crt" \
	--extra-config=controller-manager.ClusterSigningKeyFile="/var/lib/localkube/certs/ca.key" \
	--extra-config=apiserver.Admission.PluginNames=NamespaceLifecycle,LimitRanger,ServiceAccount,PersistentVolumeLabel,DefaultStorageClass,DefaultTolerationSeconds,MutatingAdmissionWebhook,ValidatingAdmissionWebhook,ResourceQuota \
	--kubernetes-version=v1.9.0

### Istio
istioctl create|replace -f samples/bookinfo/kube/route-rule-all-v1.yaml
istioctl get routerules -o yaml  
istioctl kube-inject -f samples/bookinfo/kube/bookinfo.yaml
