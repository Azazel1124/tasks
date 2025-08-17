# Helm-чарты для DevOps-проекта

В этой директории находятся Helm-чарты для деплоя всех основных сервисов проекта в Kubernetes-кластер:

- flask-chart — Flask-приложение


---

## Структура каждого чарта

```
<service>-chart/
├── Chart.yaml           # Метаинформация Helm-чарта
├── values.yaml          # Основные параметры (образ, порты, переменные окружения)
└── templates/
    ├── deployment.yaml  # Deployment для сервиса
    ├── service.yaml     # Service для доступа к поду
    └── configmap.yaml   # (если нужно) Конфиг для сервиса
```

---

## Как установить сервис в кластер

1. Перейдите в папку с нужным чартом, например:
   ```bash
   cd K8s-K0s/flask-chart
   ```
2. Отредактируйте `values.yaml` под свои нужды (например, укажите свой образ).
3. Установите чарт:
   ```bash
   helm install <release-name> .
   # Например:
   helm install flask-app .
   ```
4. Проверьте, что поды и сервисы запущены:
   ```bash
   kubectl get pods
   kubectl get svc
   ```

---

## Пример values.yaml для Flask

```yaml
replicaCount: 1
image:
  repository: <ваш-dockerhub-логин>/flask-app
  tag: latest
  pullPolicy: IfNotPresent
service:
  type: ClusterIP
  port: 5000
env:
  DB_HOST: "db"
  DB_NAME: "project1_db"
  DB_USER: "postgres"
  DB_PASSWORD: "yourpass"
  SECRET_KEY: "yourkey"
```

---


---

## Важно
- Для работы всех сервисов в одной сети используйте общую namespace или настройте networkPolicy.


---

## Полезные команды

- Обновить релиз:
  ```bash
  helm upgrade <release-name> .
  
  ```
- Удалить релиз:
  ```bash
  helm uninstall <release-name>
  ```
- Просмотреть логи пода:
  ```bash
  kubectl logs <pod-name>
  ```

---

