# R3F Game Kubernetes 🎮

Ein React Three Fiber Game mit vollständiger Kubernetes und Docker Integration - Mario-ähnliches 3D Spiel

## 🚀 Features

- **React Three Fiber** - 3D Grafiken und Spiel-Engine
- **Next.js 14** - Full-Stack React Framework mit Turbo
- **TypeScript** - Type-safe Entwicklung
- **Kubernetes Integration** - Vollständige Container-Orchestrierung
- **Docker Compose** - Lokale Entwicklungsumgebung
- **MCP Kubernetes Server** - Erweiterte Cluster-Verwaltung
- **PlayroomKit** - Multiplayer Funktionalität
- **@react-three/rapier** - Physics Engine

## 🎯 Game Components

- **Character.tsx** - Spielercharakter Steuerung
- **Scene.tsx** - 3D Szenen Management
- **Experience.tsx** - Haupt-Spiel-Loop
- **Map.tsx** - Level und Umgebung
- **Coin.tsx** - Sammelbare Objekte
- **Enemy.tsx** - Gegner AI
- **PowerUp.tsx** - Power-Ups
- **FlagPole.tsx** - Level-Ende

## 🛠️ Installation

```bash
# Repository klonen
git clone https://github.com/Eksz3lsi0r/R3F-Game-Kubernetes.git
cd R3F-Game-Kubernetes

# Dependencies installieren
npm install

# Development Server starten
npm run dev
```

## 🐳 Docker Commands

```bash
# Docker Image bauen
npm run docker:build

# Container lokal starten
npm run docker:run

# Alle Services mit Docker Compose
npm run docker:compose:up

# Live-Logs anzeigen
npm run docker:compose:logs

# Services stoppen
npm run docker:compose:down
```

## ☸️ Kubernetes Commands

```bash
# Vollständiges K8s Deployment
npm run k8s:deploy

# Pod und Service Status
npm run k8s:status

# Live Application Logs
npm run k8s:logs

# Alle K8s Ressourcen löschen
npm run k8s:delete
```

## 🎮 Development

Das Spiel läuft standardmäßig auf `http://localhost:3000`

### Zugriffsmöglichkeiten

- **NodePort:** http://localhost:30000
- **LoadBalancer:** Automatisch zugewiesene Cloud-IP
- **Port-Forwarding:** `kubectl port-forward service/r3f-game-service 3000:80`
- **MCP Server:** Port 8080 für Cluster-Management

## 📋 Architektur

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

## 🔐 Features

- **Container Security** - Non-root User, Read-only Filesystem
- **Health Checks** - Liveness und Readiness Probes
- **Resource Limits** - Memory und CPU Beschränkungen
- **RBAC** - Role-Based Access Control für MCP Server
- **ConfigMaps** - Externalisierte Konfiguration
- **Graceful Shutdown** - Sauberes Herunterfahren

## 📚 Dokumentation

Vollständige Setup-Anleitung in `KUBERNETES_DOCKER_SETUP.md`

## 🚀 Deployment

### Lokal (Minikube)
```bash
minikube start
./deploy.sh
```

### Cloud (AWS/GKE/Azure)
```bash
# kubectl konfigurieren für Cloud-Cluster
./deploy.sh
```

## 🤝 Contributing

1. Fork das Repository
2. Erstelle einen Feature Branch
3. Committe deine Änderungen
4. Push zum Branch
5. Erstelle einen Pull Request

## 📄 License

MIT License - siehe LICENSE Datei für Details.