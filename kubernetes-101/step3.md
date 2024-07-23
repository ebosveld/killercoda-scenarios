Eerste stap is om onze applicatie te deployen. Hiervoor gebruiken we het component `deployment`. Hieronder vind je de `yaml` die nodig is. Het bevat het type component, metadata zoals de naam, en de specificatie zoals het aantal instanties en de docker image. We kunnen nog veel meer toevoegen, zoals `readyness` en `healthiness` probes en omgevingsvariabelen, maar dat komt later.

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: podinfo
  namespace: podinfo
  labels:
    app: podinfo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: podinfo
      version: v1
  template:
    metadata:
      labels:
        app: podinfo
        version: v1
    spec:
      terminationGracePeriodSeconds: 30
      containers:
        - name: podinfo
          image: "stefanprodan/podinfo:6.7.0"
          imagePullPolicy: IfNotPresent
```{{copy}}

Sla het `yaml` bestand op als `deployment.yaml` in de `podinfo` map en laat het uitvoeren.

Hint: gebruik `kubectl apply`.

Controleer of de pods op zijn gekomen. Als je het volgende commando uitvoert, dan zul je als het goed is één pod zien. Deze zou de status `Running` moeten hebben met `1/1` onder `READY`.

`kubectl get pods -n podinfo`{{exec}}

## Kubectl
Je ziet dat we nu steeds de namespace moeten meegeven. We kunnen ook een context switch maken, waardoor we niet meer in de `default` namespace werken.

`kubectl config set-context --current --namespace=podinfo`{{exec}}

Nu kun je gewoon `kubectl get pods`{{exec}} uitvoeren.