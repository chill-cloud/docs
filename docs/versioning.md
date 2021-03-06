# Версионирование

Версионирование — ключевая особенность Chill, позволяющая избегать развертывания несовместимых версий. Chill придерживается спецификации вида v`major`.`minor`.`patch`, аналогичной семантическому версионированию.

* *Мажорная (major)* версия увеличивается при внесении несовместимых изменений.
* *Минорная (minor)* версия увеличивается при развертывании новой `production`-версии сервиса.
* *Патч (patch)*-версия увеличивается системой Chill автоматически при каждом развертывании `development`-версии сервиса.

## Части версии

### Мажорная версия

Смысл увеличения мажорной версии заключается в том, чтобы при внесении несовместимых изменений клиенты — как внешние, так и другие зависимые сервисы — не перешли автоматически на эту версию.

Случаи, когда увеличивается мажорная версия:

* При внесении обратно не совместимых изменений в API сервиса: в этом случае при синхронизации (`chill-cli sync`) мажорная версия увеличится автоматически.
* Не все несовместимые изменения могут быть описаны только в декларации API: например, метод сервиса может начать возвращать в новой версии другой код ошибки в той же ситуации, что и в старой версии, и на это может быть завязана логика работы зависящих от этого сервиса клиентов. В этом случае разработчик может вручную увеличить мажорную версию через `chill-cli force major`.

!!! note "Заметка"

    Новая мажорная версия развертывается как отдельная Knative-служба.

### Минорная версия

Смысл увеличения минорной версии — в том, чтобы переключить клиентов (всех или некоторую часть) на новую production-версию сервиса, обратно совместимую со старой.

Она увеличивается автоматически при развертывании новой версии, для который вызвано `chill-cli stage production`.

### Патч-версия

Патч-версия увеличивается автоматически при каждой публикации development-версии.

## Контракт увеличения версий

Исходя из сказанного выше, в системе Chill выполняется следующий контракт для версий:

* Мажорные версии в общем случае не совместимы друг с другом.
* В рамках одной мажорной версии для минорных версий с патч-версией 0 отношение совместимости рефлексивно, транзитивно и антисимметрично; таким образом,
    * `v1.5.0` совместима с `v1.3.0`,
    * `v1.3.0` совместима с `v1.1.0`,
    * `v1.5.0` совместима с `v1.1.0`,
    * `v1.1.0` не совместима с `v1.3.0`.
* Патч-версии в рамках одной мажорной и минорной в общем случае совместимы с патч-версией 0, но не совместимы друг с другом.