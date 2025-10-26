# Kubernetes & Docker Integration - R3F Game

## Übersicht

Diese R3F (React Three Fiber) Game Anwendung ist vollständig für Kubernetes und Docker optimiert und integriert den verifizierten MCP Kubernetes Server für erweiterte Cluster-Verwaltung.

## 🏗️ Architektur

```
┌─────────────────────────────────────┐
│           Load Balancer             │
├─────────────────────────────────────┤
│              Service                │
├─────────────────────────────────────┤
│         Pod 1        Pod 2          │
│    ┌─────────────┐ ┌─────────────┐   │
│    │ R3F Game    │ │ R3F Game    │   │
│    │ Container   │ │ Container   │   │
│    └─────────────┘ └─────────────┘   │
├─────────────────────────────────────┤
│        MCP Kubernetes Server        │
│      (Cluster Management)           │
└─────────────────────────────────────┘
```

## 🐳 Docker

### Lokale Entwicklung mit Docker Compose

```bash
# Starte alle Services
npm run docker:compose:up

# Zeige Logs
npm run docker:compose:logs

# Stoppe alle Services
npm run docker:compose:down
```

### Manueller Docker Build

```bash
# Baue das Image
npm run docker:build

# Führe Container aus
npm run docker:run
```

## ☸️ Kubernetes

### Schnellstart

```bash
# Deploye alles nach Kubernetes
npm run k8s:deploy

# Überprüfe den Status
npm run k8s:status

# Zeige Logs
npm run k8s:logs
```

### Manuelle Deployment-Schritte

1. **Konfiguration anwenden:**
   ```bash
   kubectl apply -f k8s/config.yaml
   ```

2. **Hauptanwendung deployen:**
   ```bash
   kubectl apply -f k8s/deployment.yaml
   kubectl apply -f k8s/service.yaml
   ```

### Zugriff auf die Anwendung

- **NodePort (lokal):** http://localhost:30000
- **LoadBalancer (Cloud):** Automatisch zugewiesene externe IP
- **Port-Forwarding:** `kubectl port-forward service/r3f-game-service 3000:80`

## 📋 Verfügbare Services

| Service | Port | Beschreibung |
|---------|------|--------------|
| r3f-game-service | 80→3000 | Hauptanwendung (NodePort) |
| r3f-game-loadbalancer | 80→3000 | Hauptanwendung (LoadBalancer) |

## 🔧 Konfiguration

### Environment Variables (ConfigMap)

```yaml
NODE_ENV: "production"
PORT: "3000"
HOSTNAME: "0.0.0.0"
GAME_TITLE: "R3F Mario Game"
MAX_PLAYERS: "4"
GAME_MODE: "multiplayer"
NEXT_TELEMETRY_DISABLED: "1"
LOG_LEVEL: "info"
```

### Ressourcen-Limits

- **R3F Game Container:**
  - Memory: 256Mi (request) / 512Mi (limit)
  - CPU: 250m (request) / 500m (limit)

## 🔍 Monitoring & Health Checks

### R3F Game Health Checks

```yaml
livenessProbe:
  httpGet:
    path: /
    port: 3000
  initialDelaySeconds: 30
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /
    port: 3000
  initialDelaySeconds: 5
  periodSeconds: 5
```

## 🔐 Sicherheit

### Container Security

- **Non-root User:** Container läufen als User 1000
- **Read-only Root Filesystem:** Verhindert Schreibzugriffe
- **Dropped Capabilities:** Alle Capabilities entfernt
- **Security Context:** Privilege Escalation deaktiviert

## 🚀 Deployment-Strategien

### Lokale Entwicklung

1. **Docker Desktop Kubernetes:** Aktiviere Kubernetes in Docker Desktop
2. **Deploy:** `./deploy.sh`
3. **Zugriff:** http://localhost:30000

### Cloud-Deployment

1. **Cluster vorbereiten:** AWS EKS, GKE, oder AKS
2. **kubectl konfigurieren:** Verbindung zum Cluster
3. **Deploy:** `./deploy.sh`
4. **DNS konfigurieren:** LoadBalancer IP mit Domain verknüpfen

## 🛠️ Troubleshooting

### Häufige Probleme

1. **Pod startet nicht:**
   ```bash
   kubectl describe pod <pod-name>
   kubectl logs <pod-name>
   ```

2. **Service nicht erreichbar:**
   ```bash
   kubectl get endpoints
   kubectl describe service r3f-game-service
   ```

### Nützliche Debug-Befehle

```bash
# Alle Ressourcen anzeigen
kubectl get all -l app=r3f-game

# Events anzeigen
kubectl get events --sort-by='.lastTimestamp'

# Pod-Details
kubectl describe pod <pod-name>

# In Container einsteigen
kubectl exec -it <pod-name> -- /bin/sh
```

## 📈 Skalierung

### Horizontale Pod-Skalierung

```bash
# Replicas erhöhen
kubectl scale deployment r3f-game-deployment --replicas=5

# Auto-Scaling aktivieren
kubectl autoscale deployment r3f-game-deployment --cpu-percent=70 --min=2 --max=10
```

## 🔄 CI/CD Integration

Das Setup ist bereit für CI/CD-Pipelines:

1. **Build:** `docker build -t r3f-game:${VERSION} .`
2. **Push:** `docker push registry/r3f-game:${VERSION}`
3. **Deploy:** `kubectl set image deployment/r3f-game-deployment r3f-game=registry/r3f-game:${VERSION}`

## 📚 Weiterführende Ressourcen

- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Docker Documentation](https://docs.docker.com/)
- [Next.js Deployment](https://nextjs.org/docs/deployment)
- [React Three Fiber](https://docs.pmnd.rs/react-three-fiber)