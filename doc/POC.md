## Proof of Concept. ArgoCD  

`Мета:` Показати реалізацію ідеї практично.

`Інструменти для розгортання застосунків:`  
Для автоматизації процесу CI обрано репозиторій [AsciiArtify](https://github.com/astergam/SciiArtify).  
Для CD обрано підхід "one application - one cluster" з "single host kubernetes cluster".  
ArgoCD обрано для системи Delivery і Deploy. ArgoCD - контролер Kubernetes який відстежує запущені додатки, порівнює поточний стан з бажаним та інформує через візуалізацію про відмінності, чим надає можливість для ручної або автоматичної синхронізації бажаного стану.  
  
Створимо окремий локальний кластер argo для ArgoCD:  
```bash
$ k3d cluster create argo
```  
Створюємо псевдоним k який вказує на команду cubectl
```bash
$ alias k=kubectl
```  
Виведемо версію cubectl, інструменту керування Kubernetes, щоб перевірити його поточну версію
```bash
$ k version
```  
Виведемо інформацію про кластер Kubernetes
```bash
$ k cluster-info
```  
Створимо namespace argocd в якому буде встановлено систему  
```bash
$ k create namespace argocd
```  
Виведемо список всіх просторів імен (namespaces) в кластері Kubernetes  
```bash
$ k get ns
```  
Застосуємо конфігураційний файл для створення ресурсів ArgoCD у просторі імен argocd  
```bash
$ k apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```  
Виведемо інформацію про всі ресурси з простору імен argocd в кластері Kubernetes  
```bash
$ k get all -n argocd
```  
Виведемо список всіх pods у просторі імен argocd.  
```bash
$ k get pod -n argocd -w
```  
Отримаємо доступ до інтерфейсу ArgoCD GUI.