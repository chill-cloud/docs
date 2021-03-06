# Установка

## Пререквизиты

### Локальный кластер
Chill работает в любой стандартной установке Kubernetes, в том числе локальном окружении.

1. [Установите minikube](https://minikube.sigs.k8s.io/docs/start/) — инструмент для запуска кластера Kubernetes, работающий поверх Docker.

2. [Установите Knative CLI](https://knative.dev/docs/getting-started/quickstart-install/#install-the-knative-cli).

3. Выполните команду `kn quickstart minikube` для установки Knative в локальный кластер.

4. Выполните команду `minikube tunnel -p knative` в отдельной вкладке терминала для того, чтобы иметь возможность совершать запросы в сервисы, которые развернете.

### Удаленный кластер

Достаточно получить файл конфигурации Kubernetes для доступа к удаленному кластеру.

 Chill будет искать его по стандартному пути `~/.kube/config` либо его можно будет передать по ключу `--kubeconfig` тем командам, которым это требуется.