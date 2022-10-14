# zhaodemo
How to make a docker for dotnet
```
dotnet new mvc -o zhaodemo
dotnet run
dotnet publish -c release -o app/ .

docker build -t zhaodemo .

docker run -p 8181:80 zhaodemo


az group create --name zhaodemo --location eastus
az acr create -g zhaodemo --name zhaocontainerdemo --sku Basic --admin-enable true
az acr credential show -n zhaocontainerdemo

docker tag zhaodemo zhaocontainerdemo.azurecr.io/zhaodemo:v1

docker login https://zhaocontainerdemo.azurecr.io -u zhaocontainerdemo -p +xZqRkxuk1Bd680dE4pSZuJuLwlJsAQI
docker push zhaocontainerdemo.azurecr.io/zhaodemo:v1

az appservice plan create -n demoplan -g zhaodemo --sku S1 --is-linux

az webapp create -g zhaodemo -p demoplan -n zhaodockerdemo --runtime "DOTNETCORE|6.0"

az webapp config container set -n zhaodockerdemo -g zhaodemo --docker-custom-image-name zhaocontainerdemo.azurecr.io/zhaodemo:v1 --docker-registry-server-url https://zhaocontainerdemo.azurecr.io --docker-registry-server-user zhaocontainerdemo --docker-registry-server-password +xZqRkxuk1Bd680dE4pSZuJuLwlJsAQI
```

* https://www.youtube.com/watch?v=q8nXv56gWms&list=PL4NfFPd0l1UbefowxrzvQ23NvshNwNB4p&index=34
