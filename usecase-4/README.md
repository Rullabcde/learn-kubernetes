## Deployment Configuration

- Nama deployment: grafana-dashboard
- Namespace: monitoring
- Replicas: 1
- Image: grafana/grafana:9.0.0
- Container port: 3000
- Environment variables:
  - GF_SECURITY_ADMIN_PASSWORD=admin123
  - GF_USERS_ALLOW_SIGN_UP=false
- Labels: app=grafana, component=dashboard

## Service Configuration

- Nama service: grafana-svc
- Type: LoadBalancer
- Port: 80 (target port 3000)
- Selector harus mengarah ke deployment grafana-dashboard
- Namespace: monitoring

## Ingress Configuration

- Nama ingress: grafana-web
- Host: monitoring.mycompany.com
- Path: /grafana (pathType: Prefix)
- Backend service: grafana-svc port 80
- Namespace: monitoring
- Annotations:
  - nginx.ingress.kubernetes.io/rewrite-target: /
  - nginx.ingress.kubernetes.io/use-regex: "true"
