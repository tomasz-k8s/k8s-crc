Podstawowe komendy
--------

* GET
  ```bash
  kubectl get [typ_obiektu]           # Lista obiektów
  kubectl get [typ_obiektu] -o wide   # Rozszerzona lista
  kubectl get [typ_obiektu] -o yaml   # Pełna definicja w YAML
  ```
* DESCRIBE
  ```bash
  kubectl describe [typ_obiektu] [nazwa]
  ```
* DELETE 
  ```bash
  kubectl delete [typ_obiektu] [nazwa]
  ```

Stwórz i uruchom POD nginx
```bash
kubectl run nginx-pod-XX --image=nginx:latest --port=80 --restart=Never
```

Prześlij komende do PODa i otrzymaj wynik
```bash
kubectl exec nginx-pod-XX -- nginx -v
```

Podłącz się bezpośrednio do shella PODa
```bash
kubectl exec -it nginx-pod-XX -- bash
```

Przekieruj port lokalny
```bash
kubectl port-forward nginx-pod-XX 8080:80
```

Kopiowanie plików do PODa
```bash
kubectl cp index.html nginx-pod-XX:/usr/share/nginx/html/
```

Kopiowanie plików z PODa
```bash
kubectl cp nginx-pod-XX:/etc/nginx/nginx.conf ./nginx.conf
```

Podglądanie logów PODa
```bash
kubectl logs nginx-pod-XX
```

Śledzenie logów
```bash
kubectl logs -f nginx-pod-XX
```

Ilość wyświetlanych wpisów
```bash
kubectl logs --tail=100 nginx-pod-XX
```

Logi z ostatnich 10min
```bash
kubectl logs --since=10m nginx-pod-XX
```

Pokaż wszystkie namespace
```bash
kubectl get namespaces
```

Utworz namespace
```bash
kubectl create namespace dev-XX
```

Utworz POD w podanym namespace
```bash
kubectl run nginx-pod-XX --image=nginx:latest --namespace=dev-XX
```

Definicja namespace
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: test-XX
```

Utworzenie namespace z pliku
```bash
kubectl apply -f [nazwa_pliku]
```

ustaw domyślny namespace
```bash
kubectl config set-context --current --namespace=dev-XX
```

Usun wszystkie zasoby z podanego namespace
```bash
kubectl delete all --all --namespace=[nazwa_namespace]
```

Definicja PODa
```yaml
apiVersion: v1                # Wersja API Kubernetes której używamy dla Poda
kind: Pod                     # Typ zasobu który tworzymy
metadata:                     # Sekcja z metadanymi
  name: przyklad-pod         # Nazwa Poda - musi być unikalna w namespace
  labels:                    # Etykiety - pomagają organizować i wyszukiwać Pody
    app: frontend           # Przykładowa etykieta określająca aplikację
    env: dev               # Przykładowa etykieta określająca środowisko

spec:                        # Specyfikacja Poda - najważniejsza część!
  containers:               # Lista kontenerów w Podzie
  - name: nginx            # Nazwa kontenera
    image: nginx:1.14.2    # Obraz kontenera z wersją
    ports:                 # Lista portów do ekspozycji
    - containerPort: 80    # Port na którym aplikacja nasłuchuje w kontenerze
```