# Service

Nu we de pods met onze applicatie hebben draaien, moeten we een manier hebben om toegang tot onze applicatie te krijgen. Normaal zou je een load balancer, of een ingress zoals `nginx` gebruiken, maar op dit platform hebben we geen extern IP adres. Dus we maken gebruik van de tools die we hebben.

In de `yaml` hieronder specificeren we dat we een `service` willen definiëren, en welk type: `NodePort`. Daarnaast geven we aan hoe de routing moet lopen: vanaf poort `9898` naar de http poort van de pod en naar alle instanties die aan de selector voldoen.

```
apiVersion: v1
kind: Service
metadata:
  name: podinfo
  namespace: podinfo
spec:
  type: NodePort
  selector:
    app: podinfo
    version: v1
  ports:
    - name: http
      nodePort: 32676
      port: 9898
      protocol: TCP
      targetPort: 9898
```{{copy}}

Sla het bestand op als `service.yaml` en voer dit weer uit met met `kubectl apply`.

Nu kunnen we de applicatie bereiken via de volgende link: [podinfo app]({{TRAFFIC_HOST1_32676}}) <small>(of [door hier de poort te selecteren]({{TRAFFIC_SELECTOR}}))</small>.