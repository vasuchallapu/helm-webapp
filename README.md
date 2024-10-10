# helm-webapp

**1. Create the helmchart**

	helm create webapp1

**2. Install the first one**

	helm install mywebapp-release webapp1/ --values webapp1/values.yaml
  helm ls --all-namespace

**3. Upgrade after templating**

	helm upgrade mywebapp-release webapp1/ --values webapp1/values.yaml

**4. Accessing it**

	minikube tunnel

**5. Create dev/prod**

	kubectl create namespace dev
	kubectl create namespace prod
	helm install mywebapp-release-dev webapp1/ --values webapp1/values.yaml -f webapp1/values-dev.yaml -n dev
	helm install mywebapp-release-prod webapp1/ --values webapp1/values.yaml -f webapp1/values-prod.yaml -n prod
	helm ls --all-namespaces
	
**6. put port-ward script .txt file for output**

	kubectl port-forward service/myhelmapp 8888:80 --namespace dev
	kubectl port-forward service/myhelmapp 8888:80 --namespace prod
	
**7. Uninstall helm Charts**

	helm uninstall mywebapp-release-dev -n dev
	helm uninstall mywebapp-release-prod -n prod


Basic Commands for Helm

1. Install Helm

  curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
  sudo apt-get install apt-transport-https --yes
  echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
  sudo apt-get update
  sudo apt-get install helm
  helm version
  
 2. helm add repository and install prometheus helm chart
 
  helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
  helm repo ls
  helm install my-prometheus prometheus-community/prometheus --version 25.27.0
  kubuctl get all
  
 3. Check helm list
 
  helm ls --all-namespaces
  
 4. access prometheus url
 
  helm status my-prometheus
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=prometheus,app.kubernetes.io/instance=my-prometheus" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9090
  
5. Install helm on dev namespace
  
  helm ls --all-namespaces
  kubectl create namespace dev
  helm install my-prometheus-dev prometheus-community/prometheus --version 25.27.0 --namespace dev
  helm ls
  helm ls --all-namespaces

6. Uninstall helm with --keep-history  
  
  helm uninstall my-prometheus --keep-history
  helm ls --all-namespaces
  helm ls --all-namespaces -a
  
7. Upgrde existing helm chart  

  helm upgrade my-prometheus-dev prometheus-community/prometheus --version 25.26.0 --namespace dev
  helm ls --all-namespaces
  helm ls --all-namespaces -a

8. Check the helm history

  helm history -n dev
  helm history my-prometheus-dev -n dev
  
9. Rollback the required version
  
  helm rollback my-prometheus-dev -n dev
  helm history my-prometheus-dev -n dev
