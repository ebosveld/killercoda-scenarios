# Introductie

Kubernetes (of k8s) is een open source platform ontworpen om het beheer van gecontaineriseerde applications te automatiseren. Denk aan containers als lichte, geïsoleerde omgevingen waarin je applicaties kunt draaien. Het werd oorspronkelijk ontwikkeld door Google en wordt nu beheerd door de Cloud Native Computing Foundation (CNCF). Kubernetes helpt je om deze containers efficiënt te beheren, vooral als je er veel hebt.

## Componenten

Kubernetes bestaat uit een groep van één of meer **nodes** die samen een **cluster** vormen. **Nodes** zijn machines waar containers op draaien. In de terminal rechts op het scherm heb je verbinding met een K8s cluster met twee nodes.

Het brein van Kubernetes wordt de **control plane** genoemd, die draait op één van de nodes. Over het algemeen zullen hier geen applicatie containers op draaien. Voor deze workshops hebben we echter de **control plane** geconfigureerd dat deze ook work loads kan plaatsen.

Laten we eens kijken of het cluster goed werkt. Toon de nodes in het cluster met de volgende commando:

```
kubectl get nodes
```{{execute}}

Je zult nu een lijstje krijgen met twee nodes, waarvan één de rol `control-plane` heeft.

```
$ kubectl get nodes
NAME STATUS ROLES AGE VERSION
controlplane Ready control-plane 18d v1.30.0
node01 Ready <none> 18d v1.30.0
```