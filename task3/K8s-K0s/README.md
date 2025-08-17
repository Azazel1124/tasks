# Helm-чарты

В этой директории находятся Helm-чарты для деплоя всех основных сервисов проекта в Kubernetes-кластер:

- flask-chart — Flask-приложение




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

