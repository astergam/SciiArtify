## Proof of Concept. ArgoCD  

`Мета:` Показати реалізацію ідеї практично.

`Інструменти для розгортання застосунків:`  
Для автоматизації процесу CI обрано репозиторій [AsciiArtify](https://github.com/astergam/SciiArtify).  
Для CD обрано підхід "one application - one cluster" з "single host kubernetes cluster".  
ArgoCD обрано для системи Delivery і Deploy. ArgoCD - контролер Kubernetes який відстежує запущені додатки, порівнює поточний стан з бажаним та інформує через візуалізацію про відмінності, чим надає можливість для ручної або автоматичної синхронізації бажаного стану.  
  
1. Створимо окремий локальний кластер для ArgoCD:  
```bash
$ k3d cluster create argo
```