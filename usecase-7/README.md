## ConfigMap Configuration

- Nama: healthcare-config
- Namespace: medical
- Data:
  - api.properties: server.port=9000\napi.version=v3\nmax.patients=5000
  - db.config: host=postgres-primary.medical.svc\nport=5432\nssl=enabled
  - smtp.host: mail.hospital.com
  - og.level: INFO

## Secret Configuration

- Nama: healthcare-secret
- Namespace: medical
- Type: Opaque
- Data (encode ke base64):
  - db.user: medical_system
  - db.password: HealthSecure@2024
  - smtp.password: mailPass456
  - encryption.key: AES256_SECRET_KEY_HEALTH

## Multi-Container Deployment

- Nama deployment: healthcare-system
- Namespace: medical
- Replicas: 3

  ### Container 1 (API Server):

- Name: api-server
- Image: springio/gs-spring-boot-docker:latest
- Port: 9000
- Environment dari Secret: DATABASE_USER, DATABASE_PASS
- Environment dari ConfigMap: LOG_LEVEL, SMTP_HOST
- Mount ConfigMap ke /app/config
- Mount shared volume ke /app/reports

  ### Container 2 (Report Generator):

- Name: report-gen
- Image: node:16-alpine
- Port: 3001
- Mount shared volume ke /reports

  ### Container 3 (File Backup):

- Name: backup-service
- Image: alpine:3.16
- Mount shared volume ke /backup/files
- Shared Volume: report-storage (emptyDir)
- ConfigMap Volume: app-config
- Labels: app=healthcare, tier=backend, department=medical

## Service Configuration

- Nama: healthcare-service
- Type: ClusterIP
- Port 9000 → target 9000 (api-server)
- Port 3001 → target 3001 (report-gen)
- Namespace: medical

## Ingress Configuration

- Nama: healthcare-ingress
- Host: api.hospital.local
- Path: /health (pathType: Prefix)
- Backend service: healthcare-service port 9000
- Namespace: medical
- Annotations:
  - nginx.ingress.kubernetes.io/rewrite-target: /
  - nginx.ingress.kubernetes.io/cors-allow-origin: "\*"
