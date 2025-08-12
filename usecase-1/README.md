## Deployment Configuration

- Nama deployment: web-app
- Namespace: production
- Replicas: 3
- Image: nginx:1.21
- Container port: 80
- Resource limits: CPU 200m, Memory 256Mi
- Resource requests: CPU 100m, Memory 128Mi
- Environment variable: ENV=production
- Labels: app=web, tier=frontend

## Service Configuration

- Nama service: web-service
- Type: ClusterIP
- Port: 80 (target port 80)
- Selector harus mengarah ke deployment web-app
- Namespace: production

## Ingress Configuration

- Nama ingress: web-ingress
- Host: myapp.local
- Path: / (pathType: Prefix)
- Backend service: web-service port 80
- Namespace: production
- Annotation untuk nginx ingress controller
