We hebben nu één pod draaien en kunnen deze bereiken. Dat is natuurlijk niet handig. Als er verkeer komt, of hij crasht, dan is je applicatie (tijdelijk) niet meer bereikbaar.

We kunnen in k8s op meerdere manieren schalen. We zouden in de deployment de `replicas` kunnen ophogen, dan doe je dit statisch. We kunnen echter ook een `auto scaler` maken. Dan kunnen we schalen aan de hand van criteria zoals CPU gebruik of memory consumptie. Dat gaan we in deze stap doen.

Maak een nieuw bestand in de `podinfo` folder met de naam `hpa.yaml` en voeg de volgende inhoud toe:

```
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: podinfo
  namespace: podinfo
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: podinfo
  minReplicas: 2
  maxReplicas: 4
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        # scale up if usage is above
        # 99% of the requested CPU (100m)
        averageUtilization: 99
```{{copy}}

In dit bestand maken we een `autoscaler` die definieert dat we standaard 2 replicas hebben, en opschalen naar maximaal 4 replicas als het CPU gebruik boven de 99% komt.

Voer dit bestand weer uit en controleer met het volgende commando of de replicas zijn opgeschaald.

`kubectl get pods -o=wide`{{exec}}

Je ziet nu dat er twee instanties zijn, en deze ook verdeelt zijn over de twee nodes die we hebben.