# Aan de slag

Nu we de crash course Kubernetes hebben gehad, laten we starten met wat leuks: een applicatie deployen. We gebruiken hiervoor de [podinfo](https://github.com/stefanprodan/podinfo) applicatie.

Hiervoor hebben we alles met commando's gedaan, maar dat is natuurlijk niet zoals het echt hoort. Dat is niet reproduceerbaar en in veel organisaties is _click ops_ uit den boze. Daarom gaan we de rest doen met `yaml` files.

## Namespace

Om alles een beetje georganiseerd te houden, kan je in K8s **namespaces** gebruiken. Laten we er een maken voor onze **podinfo** applicatie. In de map _podinfo_ in de root van deze vm, vind je de `namespace.yaml`. Je kan hem via `vim` of de editor in de tabs aan de bovenkant bekijken.

Via het volgende commando kan je de _state_ van Kubernetes wijzigen naar de _target state_ volgens de `yaml` file.

`kubectl apply -f podinfo/namespace.yaml`{{exec}}

Via de `kubectl get` commando kan je vervolgens bekijken of het gelukt is:

`kubectl get namespaces`{{exec}}
