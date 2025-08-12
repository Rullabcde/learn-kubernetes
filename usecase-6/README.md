## ConfigMap Configuration

- Nama: learning-config
- Namespace: education
- Data:
  - server.properties: port=8080\ntimeout=30s\nmax_students=1000
  - database.url: postgresql://postgres:5432/learning_db
  - kafka.brokers: kafka-cluster:9092
  - file.upload.path: /app/uploads

## Secret Configuration

- Nama: learning-secret
- Namespace: education
- Type: Opaque
- Data (encode ke base64):
  - postgres.username: learning_admin
  - postgres.password: eduPass2024!
  - jwt.secret: mySuper$ecretJWT123
  - s3.access.key: AKIAEXAMPLE123

## Multi-Container Pod dengan Shared Volume

- Nama pod: learning-platform
- Namespace: education

  ### Container 1 (Main app):

- Name: learning-api
- Image: openjdk:11-jre
- Port: 8080
- Environment dari Secret: DB_USER, DB_PASS, JWT_SECRET
- Environment dari ConfigMap: KAFKA_BROKERS
- Mount shared volume ke /app/uploads
- Mount ConfigMap ke /app/config

  ### Container 2 (File processor):

- Name: file-processor
- Image: python:3.9-slim
- Mount shared volume ke /shared/files

  ### Container 3 (Log collector):

- Name: fluent-bit
- Image: fluent/fluent-bit:1.9
- Port: 2020

- Shared Volume: shared-storage (emptyDir)
- ConfigMap Volume: config-volume
- Labels: app=learning, version=v2, env=prod

## Service Configuration

- Nama: learning-svc
- Type: NodePort
- Port 80 → target 8080 (learning-api), NodePort: 30080
- Port 2020 → target 2020 (fluent-bit), NodePort: 30020
- Namespace: education
