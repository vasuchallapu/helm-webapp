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
