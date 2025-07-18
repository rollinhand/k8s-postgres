# Postgres mit PgAdmin

Kubernetes Konfiguration mit Postgres 17.5 und PgAdmin 4.

|Datei|Zweck|
|---|---|
|ConfigMap|enthält nicht-sensible Umgebungsvariablen wie Benutzername oder Hostname
|Secret|enthält sensible Daten wie Passwörter – Rancher zeigt diese sicher an
|PVC|sorgt für persistente Daten für Postgres und PgAdmin
|Deployments|erstellen jeweils einen Pod (postgres, pgadmin), mit Umgebung und Storage
|Services|ermöglichen Kommunikation und externe Erreichbarkeit über Port-Forward oder NodePort

## Installation

```bash
kubectl apply -f k8s/configmap.yaml
kubectl apply -f k8s/secrets.yaml
kubectl apply -f k8s/postgres-pvc.yaml
kubectl apply -f k8s/pgadmin-pvc.yaml
kubectl apply -f k8s/postgres-deployment.yaml
kubectl apply -f k8s/pgadmin-deployment.yaml
kubectl apply -f k8s/services.yaml
```

## Zugriff PgAdmin
Wenn du NodePort nutzt, kannst du mit `kubectl get svc pgadmin` die externe Portnummer sehen, z. B.:

```bash
pgadmin   NodePort   10.43.52.104   <none>        8081:30080/TCP
```

Dann kannst du aufrufen: http://localhost:30080

**Login in PgAdmin:**
Benutzername: admin@example.com
Passwort: pgadmin123

**Neuen Server angeben:**
Name: postgres
Host name: postgres
Username: postgres
Password: postgres123