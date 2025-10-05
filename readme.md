# Podsumowanie projektu Kubernetes

## Zakres
- Manifesty w katalogu `k8s` przygotowują przestrzeń nazw oraz wdrożenie statycznej aplikacji Nginx.
- Dodatkowy plik `app.yaml` zawiera przykładową aplikację "hello-app" z usługą i wejściem Ingress.

## Zasoby
- `00-namespace.yaml`: deklaruje przestrzeń nazw `nginx-demo`.
- `10-configmap-index.yaml`: tworzy ConfigMap z plikiem `index.html` serwowanym przez Nginx.
- `20-deployment.yaml`: uruchamia dwie repliki kontenera `nginx:1.27-alpine`, montuje stronę z ConfigMapa i definiuje sondy `readiness` i `liveness`.
- `30-service-loadbalancer.yaml`: publikuje aplikację jako `Service` typu `LoadBalancer` pod nazwą `web`.
- `30-service-nodeport.yaml`: alternatywny manifest usługi `web`; obecnie również typu `LoadBalancer` mimo nazwy pliku.
- `app.yaml`: komplet manifestów dla demo `hello-app` (Deployment, Service, Ingress) z hostem `hello.local` i klasą `nginx`.

## Uwagi
- Jeśli potrzebny jest prawdziwy wariant NodePort, zmień `spec.type` na `NodePort` i ustaw `nodePort`.
- Do walidacji względem klastra użyj `kubectl apply --dry-run=client -f <plik>` lub `kubectl diff`.
