# Funktionsweise

1. Traefik hört auf Port 443 und fungiert als Load Balancer:
Traefik empfängt den eingehenden Traffic auf Port 443 (HTTPS). Es fungiert als Load Balancer und ist für das Routing des Traffics innerhalb des Kubernetes-Clusters verantwortlich.
2. Weiterleitung an NodePort (32443):
Der Traffic wird an einen internen NodePort-Service auf Port 32443 weitergeleitet. Dieser Service verteilt den Traffic auf die Nodes im Cluster.
3. NodePort leitet Traffic an den ContainerPort weiter:
Der NodePort-Service leitet den Traffic an den ContainerPort des Traefik-Containers weiter (z.B. Port 8443).
4. Traefik verarbeitet die Anfrage:
Traefik erhält den Traffic auf dem ContainerPort und überprüft das Gateway-Objekt, das als zentrale Steuerungseinheit für die Weiterleitung von Anfragen fungiert.
5. Gateway-Objekt:
Das Gateway-Objekt definiert, auf welchen Ports und auf welchen Domains Traefik Anfragen entgegennehmen soll. Es legt auch fest, welche HTTPRoutes mit welchen Hostnamen und Pfaden verknüpft sind.
Im Gateway-Objekt ist Traefik als GatewayClass konfiguriert, die angibt, dass Traefik für das Routing von Anfragen verantwortlich ist.
6. Ermittlung der HTTPRoute:
Basierend auf der Konfiguration des Gateway-Objekts sucht Traefik nach einer passenden HTTPRoute-Ressource. Die HTTPRoute enthält spezifische Routing-Regeln, die bestimmen, wie Anfragen verarbeitet und an Services weitergeleitet werden.
Die HTTPRoute spezifiziert beispielsweise, welche Pfade oder Hostnames an welche Kubernetes-Services weitergeleitet werden.
7. Weiterleitung an den entsprechenden Service:
Traefik leitet die Anfrage gemäß der HTTPRoute an den entsprechenden Kubernetes-Service weiter. Dieser Service könnte ein ClusterIP-, NodePort- oder LoadBalancer-Service sein, der den Traffic an den richtigen Pod weiterleitet.
8. Service leitet Traffic an den Pod weiter:
Der Kubernetes-Service empfängt die Anfrage und verteilt sie an den entsprechenden Pod, der mit dem Service verknüpft ist.
9. Pod verarbeitet die Anfrage:
Der Pod empfängt den Traffic und die Anwendung im Container innerhalb des Pods verarbeitet die Anfrage.
