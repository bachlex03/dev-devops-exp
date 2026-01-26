Đề: Trong namespace exam, tạo:

Deployment web (image: httpd, replicas: 2)
Service web-svc (ClusterIP, port 8080→80)
Service web-ext (NodePort, port 80→80, nodePort: 30081)