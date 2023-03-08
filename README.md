Kubernetes cluster kurulumu için kind kullandım.  
Öncelikle bilgisayarımızda kind kurulu olması lazım.
Kind kurulumu için https://kind.sigs.k8s.io/docs/user/quick-start/ adresi incelenebilir. Bilgisayarımıza kind'ı kurduktan sonra.

    kind create cluster --config=dreamconfig.yaml

komutu ile kubernetes cluster'ı kurulur.  
  

Proje olarak https://github.com/SampleJavaApp/app kullanılmıştır.  
app-main içerisine Dockerfile eklenmiştir.

    docker build -t dream:1.0.0 ./app-main/

Komutu ile image'ımız kurulur.  
  
    kind load docker-image dream:1.0.0 --name dreamgames

Komutu ile image'ımız cluster'a aktarılır.  

    kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml

Komutu ile Nginx ingress conrtoller kind cluster'ımıza kurulur

    kubectl apply -f manifast/deployment.yaml

Komutu ile uygulamamızın namespace, service, deployment ve ingress 'i kurulur.

# Proje Sonu

En sonunda http://dream.social/api/foos?val=TEST adresi ile kontrol sağlanır.
### Not
---

deployment.yaml içerisindeki ingress kısmında host olarak dream.social eklenmiştir. dream.social adresi bize ait olmadığından bu kısımda bilgisaramızın bu adresi çözerken localhost'u kullanması için

    vim /etc/host

komutu ile 
    
    127.0.0.1       dream.social

satırı eklenir.














