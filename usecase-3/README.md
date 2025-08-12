## Deployment Configuration

- Nama deployment: mysql-database
- Namespace: database
- Replicas: 1
- Image: mysql:8.0
- Container port: 3306
- Environment variables:
  - MYSQL_ROOT_PASSWORD=rootpass123
  - MYSQL_DATABASE=inventory
  - MYSQL_USER=dbuser
- Labels: app=mysql, role=database

## Service Configuration

- Nama service: mysql-service
- Type: ClusterIP
- Port: 3306 (target port 3306)
- Selector harus mengarah ke deployment mysql-database
- Namespace: database

## Ingress Configuration

- Nama ingress: db-admin-ingress
- Host: dbadmin.company.local
- Path: / (pathType: Exact)
- Backend service: mysql-service port 3306
- Namespace: database
- Annotation: nginx.ingress.kubernetes.io/ssl-redirect: "false"
