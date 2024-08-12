# Funktionsweise

Traefik hört auf Port 443 und fungiert als Load Balancer.  
Der Traffic wird intern an einen NodePort 32443 weitergeleitet.  
Der NodePort-Service leitet den Traffic schließlich an den ContainerPort (z.B. 8443) des eigentlichen Traefik-Containers weiter.
