# Componenten

Naast het cluster en de nodes, bestaat Kubernetes uit een aantal componenten om je containers en applicaties te draaien.

## Pods

De kleinste en eenvoudigste Kubernetes-objecten. Een pod kan één of meerdere containers bevatten die samen draaien en resources delen.

Laten we eens kijken welke pods er allemaal standaard in een k8s cluster draaien, voer het volgende commando uit:

`kubectl get pods --all-namespaces`{{exec}}

## Deployments

Beheert de implementatie en schaling van pods. Deployments zorgen ervoor dat het gewenste aantal pods altijd draait.

Om te demonstreren hoe dit werkt, kan je de volgende commando in de terminal uitvoeren:

`kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1`{{exec}}

Controleer met het volgende commando of de deployment gelukt is. Je zou onder het kopje **READY** de waarde `1/1` moeten zien.

`kubectl get deployments`{{exec}}

Pods die binnen Kubernetes draaien, draaien op een privé, geïsoleerd netwerk. Standaard zijn ze zichtbaar voor andere pods en services binnen hetzelfde Kubernetes-cluster, maar niet buiten dat netwerk. Wanneer we `kubectl` gebruiken, communiceren we via een API endpoint.

Om onze applicatie te kunnen benaderen, moeten we deze beschikbaar maken op het netwerk. Normaal zou je hiervoor een loadbalancer gebruiken, maar voor nu gebruiken we het volgende commando.

**Note:** Voer dit uit op een nieuwe terminal tab.

`kubectl proxy`{{exec}}

In je originele tab kun je dan met `curl` de API aanroepen die we net gedeployed hebben:

`curl http://localhost:8001/version`{{exec}}

## Services

Maakt de communicatie tussen verschillende onderdelen van een applicatie mogelijk en zorgt ervoor dat pods kunnen worden bereikt, zowel binnen de cluster als van buitenaf.
