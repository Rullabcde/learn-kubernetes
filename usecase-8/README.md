## ConfigMap Configuration

- Nama: tokokita-config
- Namespace: tokokita-prod
- Data:
  - database.host: postgres.tokokita-prod.svc.cluster.local
  - database.port: 5432
  - redis.host: redis.tokokita-prod.svc.cluster.local
  - api.gateway.url: http://api-gateway:80
  - app.env: production

## Secret Configuration

- Nama: tokokita-secret
- Namespace: tokokita-prod
- Type: Opaque
- Data (encode ke base64):
  - db.username: tokokita_user
  - db.password: TokoProd2024!
  - jwt.secret: myJWTSecretKey123
  - payment.api.key: pk_live_abc123xyz

## Multi-Container Deployment

- Nama deployment: user-service
- Namespace: tokokita-prod
- Replicas: 2

  ### Container 1:

- Name: user-app
- Image: node:16-alpine
- Port: 3000
- Environment dari Secret: DB_USER, DB_PASS, JWT_SECRET
- Environment dari ConfigMap: DB_HOST, REDIS_HOST

  ### Container 2:

- Name: redis-cache
- Image: redis:7-alpine
- Port: 6379
- Labels: app=user-service, tier=backend
