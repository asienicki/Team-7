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


