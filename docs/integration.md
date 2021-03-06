# Интеграция со сторонними сервисами

## Интеграция с Git-хостингами

Chill использует Git-репозитории как источник правды для истории версий сервиса. Если над сервисом работают несколько человек, скорее всего, им нужно использовать один из Git-хостингов для синхронизации своей работы.

В этом случае Chill выносит работу по развертыванию в CI соответствующего хостинга; таким образом, для развертывания приложения разработчикам надо лишь делать `git push` в соответствующие репозитории.

### GitHub

Использование:

``` bash
chill-cli integrate github \
          -u    <имя пользователя> \
          -p    <GitHub-токен> \
          --url <адрес репозитория>
```

### GitLab

По умолчанию интеграция работает с публичным сервисом GitLab; для использования с локальным развертыванием можно указать его API-эндпоинт.

Использование:

``` bash
chill-cli integrate gitlab \
          -u    <имя пользователя> \
          -p    <GitLab-токен> \
          --url <адрес репозитория>
         [--api <адрес API-эндпоинта локального GitLab>]
```

## Интеграция с container registry

После интеграции с Git-хостингом по умолчанию будет активирован его container registry для доставки образов в кластер Kubernetes. Часто для уменьшения задержек при развертывании или для доступа на узлах без доступа к Интернету хочется воспользоваться registry, предоставляемым облаком. В таком случае можно переопределить настройку:

###

``` bash
chill-cli registry <адрес registry> -u <имя пользователя> -p <пароль>
```