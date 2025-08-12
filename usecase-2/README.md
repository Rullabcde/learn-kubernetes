## Deployment Configuration

- Nama deployment: ecommerce-api
- Namespace: backend
- Replicas: 2
- Image: node:16-alpine
- Container port: 3000
- Environment variables:
- NODE_ENV=production
- PORT=3000
- Labels: app=api, version=v1

## Service Configuration

- Nama service: api-service
- Type: NodePort
- Port: 80 (target port 3000)
- NodePort: 30080
- Selector harus mengarah ke deployment ecommerce-api
- Namespace: backend

## Ingress Configuration

- Nama ingress: api-ingress
- Host: api.ecommerce.local
- Path: /api (pathType: Prefix)
- Backend service: api-service port 80
- Namespace: backend
- Annotation: nginx.ingress.kubernetes.io/rewrite-target: /
