### Вступ

- Minikube - це інструмент для створення середовища Kubernetes на локальному комп'ютері або ноутбуці. Технічно це дистрибутив Kubernetes, але оскільки він призначений для іншого типу використання, ніж більшість інших дистрибутивів 
(таких як Rancher, OpenShift та EKS), частіше можна почути, що люди називають його інструментом, а не дистрибутивом. Minikube підтримує всі основні операційні системи - Windows, Linux та macOS. (На жаль, він не працює на мобільних пристроях). minikube можна розгортати як віртуальну машину, контейнер або на чисте залізо за допомогою спеціального драйвера.

- kind - інструмент для запуску локальних кластерів Kubernetes з використанням «вузлів» - контейнерів Docker. В першу чергу kind був розроблений для тестування самого Kubernetes, але може бути використаний для локальної розробки або CI. Це призводить до швидшого налаштування Kubernetes у порівнянні з Kubernetes на основі віртуальних машин, таких як minikube та microk8s.

- k3d - це обгортка, яка дозволяє створювати швидші та високодоступні кластери k3s у контейнерах Docker. k3d покриває багато недоліків k3s, таких як швидкість, складність створення декількох кластерів та масштабованість.  k3d дозволяє легко створювати одно- та багатовузлові кластери k3s для безперешкодної локальної розробки та тестування Kubernetes додатків, забезпечуючи при цьому легке масштабування робочих навантажень. Він також надає прості команди, які полегшують керування.

- Всі три інструменти підтримують інтеграцію з Podman, проте, для Minikube та k3d цей функціонал експериментальний. 

### Характеристики
                    
Х-ка  | kind | k3d | minikube
------------- | ------------- |------------- | ------------- 
Підтримка ОС  | Linux, macOS, Windows  | Linux, macOS, Windows  | Linux, macOS, Windows
Підтримувані архітектури  | x86_64, ARM  | x86_64, ARM64, ARMhf  | x86_64, ARM64, ARMv7, ppc64, s390x
Функціонал  | Запуск кластера в контейнерах Docker  | Запуск кластера в контейнерах Docker  | Запуск кластера в контейнерах Docker, VM, Bare metal
Масштабування  | Горизонтальне масштабування, підтримка багатокластерних конфігурацій  | Горизонтальне масштабування, підтримка багатокластерних конфігурацій, можливість додання нод до запущеного кластеру  | Обмежена підтримка багатокластерних конфігурацій, підтримка багатовузлових кластерів через драйвер.
Висока доступність  | Підтримується  | Підтримується  | Обмежена підтримка
Управління кластером | kubectl | kubectl | minikube, kubectl, dashboard
Моніторинг | можливість інтеграції з Prometheus, Grafana | інтегрований моніторинг k3s, можливість інтеграції з Prometheus, Grafana | dashboard, можливість інтеграції з Prometheus

### Переваги і недоліки

#### Minikube
##### Переваги:

1. **Легкість встановлення та використання**: Minikube дуже легко встановити та налаштувати. Він підтримує різні операційні системи, такі як Linux, macOS та Windows, і дозволяє швидко розгорнути локальний кластер Kubernetes.

2. **Підтримка різних гіпервізорів**: Minikube підтримує різні гіпервізори, такі як VirtualBox, KVM, HyperKit, Docker та інші, що робить його дуже гнучким у використанні.

3. **Аддони для розширення функціональності**: Minikube має вбудовану підтримку аддонів, які можна легко встановити для додаткових функцій, таких як Kubernetes Dashboard, Nginx Ingress, Helm та інші.

4. **Ефективне використання ресурсів**: Minikube є легковажним рішенням, що дозволяє ефективно використовувати ресурси вашого комп'ютера для локального тестування та розробки.

5. **Швидкі цикли розробки**: Завдяки можливості швидко розгортати та тестувати Kubernetes додатки в локальному середовищі, Minikube сприяє швидким циклам розробки та налагодження.

###### Недоліки

1. **Обмежені ресурси**: Minikube працює на одній машині, що обмежує кількість доступних ресурсів. Це може бути проблемою для тестування великих або ресурсомістких додатків.

2. **Відсутність високої доступності**: Minikube не підтримує високої доступності, оскільки працює лише на одному вузлі. Це означає, що він не підходить для тестування сценаріїв з відмовостійкістю.

3. **Обмежена масштабованість**: Через те, що Minikube працює на одній машині, можливості масштабування обмежені. Це може бути проблемою для тестування додатків, які потребують горизонтального масштабування.

4. **Відмінності від реальних кластерів**: Minikube може не повністю відображати поведінку реальних кластерів Kubernetes, особливо в контексті мережевих налаштувань та інтеграції з іншими сервісами.

5. **Проблеми з продуктивністю**: Використання Minikube може призвести до зниження продуктивності на локальній машині, особливо якщо вона має обмежені ресурси.


#### k3d
##### Переваги:
1. **Швидкість та легкість налаштування:** k3d дозволяє швидко розгортати кластери Kubernetes завдяки легковажності k3s. Це робить його ідеальним для локального розвитку та тестування.
2. **Мінімальні вимоги до ресурсів:** k3d використовує k3s, який є легковажною версією Kubernetes. Це означає, що він споживає менше ресурсів і може працювати на менш потужних машинах.
3. **Інтеграція з Docker:** k3d використовує Docker для запуску кластерів, що робить його зручним для розробників, які вже знайомі з Docker.
4. **Гнучкість та масштабованість:** k3d дозволяє легко створювати та видаляти кластери, що робить його зручним для тестування різних конфігурацій та сценаріїв.
5. **Підтримка багатокластерних середовищ:** k3d дозволяє запускати кілька кластерів на одній машині, що корисно для тестування багатокластерних сценаріїв.

##### Недоліки:
1. **Обмежена підтримка високої доступності:** k3d не забезпечує вбудовану підтримку розподіленої бази даних для високої доступності контрольної площини. Для досягнення високої доступності потрібно налаштовувати зовнішню базу даних, таку як etcd, PostgreSQL або MySQL1.
2. **Обмежена масштабованість:** k3d підходить для локального розвитку та тестування, але може бути менш ефективним для великих виробничих середовищ через обмеження Docker.
3. **Залежність від Docker:** k3d використовує Docker для запуску кластерів Kubernetes, що може бути проблемою, якщо у вас є обмеження на використання Docker або якщо ви використовуєте інші контейнерні платформи.
4. **Менша спільнота та підтримка:** порівняно з іншими рішеннями, такими як Minikube або Kind, k3d має меншу спільноту користувачів і менше доступних ресурсів для вирішення проблем.

### Демонстрація
![demo](https://github.com/vitali-o/AsciiArtify/blob/main/images/demo.gif?raw=true)

### Висновки:
k3d є найбільш універсальним інструментом, завдяки легкості, швидкій роботі, можливості масштабування і підтримці ingress

#### Установка:
```
wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
k3d cluster create -p "80:30080@agent:0" --agents 2
export KUBECONFIG="$(k3d kubeconfig write k3s-default)"
kubectl create deployment asciiartify --image=vitaliio/asciiartify:v1.0.0
kubectl autoscale deployment asciiartify --cpu-percent=50 --min=2 --max=10
kubectl apply -f nodeport.yaml

```

файл nodeport.yaml:

```
apiVersion: v1
kind: Service
metadata:
  labels:
    app: nginx
  name: nginx
spec:
  ports:
  - name: 80-80
    nodePort: 30080
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: nginx
  type: NodePort

```
