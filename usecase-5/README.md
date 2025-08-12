## ConfigMap Configuration

- Nama: web-config
- Namespace: webapp
- Data:
  - app.properties: debug=true\nlog_level=info\nmax_connections=100
  - database.host: mysql-db.webapp.svc.cluster.local
  - redis.host: redis-cache

## Secret Configuration

- Nama: web-secret
- Namespace: webapp
- Type: Opaque
- Data (encode ke base64):
  - db.username: webapp_user
  - db.password: secure_pass_123
  - api.key: abc123xyz789

## Multi-Container Deployment

- Nama deployment: webapp-stack
- Namespace: webapp
- Replicas: 2

  ### Container 1 (Main app):

- Name: web-app
- Image: nginx:1.21
- Port: 80
- Mount ConfigMap web-config ke /etc/config
- Environment dari Secret: DB_USER dan API_KEY

  ### Container 2 (Sidecar cache):

- Name: redis-cache
- Image: redis:6.2-alpine
- Port: 6379
- Labels: app=webapp, tier=frontend

## Service Configuration

- Nama: webapp-service
- Type: ClusterIP
- Port 80 → target 80 (nginx)
- Port 6379 → target 6379 (redis)
- Namespace: webapp
