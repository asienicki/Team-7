### Polecenia
Pobranie działających podów:
`kubectl -n openhack07 get po`

Sprawdzenie konfiguracji czy działa:
`kubectl kustomize .`

Zaaplikowanie zmian, które zrobiliśmy w konfiguracji:
`kubectl apply -k`

Wyświetlenie logów:
`kubectl -n openhack07 logs -l app=poi`

Wejście do środka do pod'a:
`kubectl -n openhack07 exec -it poi-deploy-7f8cb7df5b-626lc -- env`

Sprawdzenie uprawnień:
```
az aks get-credentials --name newChallenge3 --resource-group teamResources -f ./challenge3 && kubelogin --kubeconfig ./challenge3 convert-kubeconfig -l azurecli
```

Pobranie uprawnień dla naszego klastra:
```
az aks get-credentials --name newChallenge3 --resource-group teamResources -f ~/.kube/config
```

### Historia poleceń

Pobranie istniejących namespaców:
```
kubectl get ns
```
Skrót dla:
```
kubectl get namespace
```

Pokaż informację o wersji:
```
kubectl version
```

Ładniejsze pokazywanie wersji:
```
kubectl version --output=yaml
```

Zaaplikuj zmiany z aktualnego folderu ".":
```
kubectl apply -k .
```

Wyświetl listę podów w namespace openhack07:
```
kubectl -n openhack07 get po
```

Wejście do pod'a:
```
kubectl exec -it poi-deploy-f59d65d87-nhckf -n api -- sh
```
Wylistowanie wszystkich ról:
```
kubectl get role -A
```
Usunięcie konkretnej roli:
```
kubectl -n api delete role dev-user-full-access
```
Usunięcie konfiguracji z folderu RBAC:
```
kubectl delete -f RBAC
```
Zaaplikowanie konfiguracji z folderu RBAC:
```
kubectl apply -f RBAC
```
Pobranie podów z namespace o nazwie api:
```
kubectl get pods -n api
```
Pobranie podów z namespace o nazwie web:
```
kubectl get pods -n web
```

Instalujemy KeyVault:
```
az aks enable-addons --addons azure-keyvault-secrets-provider --name newChallenge3 --resource-group teamResources
```

az keyvault create -n Team7KeyVault -g teamResources -l northeurope

az keyvault secret set --vault-name Team7KeyVault -n SqlServer --value MyAKSExampleSecret

az keyvault secret set --vault-name Team7KeyVault -n SqlServer --file poi.env