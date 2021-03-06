# Развертывание

* Зафиксируйте изменения в Git-репозитории через `git commit` — Chill развертывает только неизменяемые конфигурации сервисов.
* Введите `chill-cli freeze` — если все пройдет успешно, в Git зафиксируется метка с версией. Если возникнут какие-то конфликты, вернется сообщение об ошибке.

## Локальное развертывание

* Введите `chill-cli deploy` — в результате выполнения команды
    * Соберется Docker-образ сервиса
    * Образ загрузится в container registry
    * Сервис развернется в кластере

## Удаленное развертывание

* Запушьте изменения в удаленный Git-репозиторий. В результате 
    * Если обнаружится конфликт версий из-за работы других людей, система контроля версий не позволит загрузить изменения. В таком случае выполнение `chill-cli sync`, `git commit` и `chill freeze` решит проблему.
    * После загрузки по признаку метки с версией запустится CI-пайплайн, который сделает то же самое, что команда `chill-cli deploy`.

## Получение статуса

После выполнения команды развертывания вы можете ввести `chill-cli status`, чтобы оследить адрес и состояние службы.