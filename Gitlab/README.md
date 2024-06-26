# Gitlab, Gitlab_runner запуск и первоночальная настройка

1. Запуск Gitlab и Gitlab_runner c docker-compose.yaml файла (docker-compose up -d)
2. Если на серваке где запускается есть выход в инет и в публичные репозитории (если нет смотрим след. пункт 4), то все должно работать сразу кроме tls, путь к корневому серту укажем когда будем регистрировать раннер
3. Если нет домена для Гитлаба и не собираемся его регать, то можем просто в /etc/hosts давить запись ip и его хостнейм
```
192.168.1.2 gitlab.somevm.ru
```
4. В случае если нет выхода во внешнюю сеть в инет, то нужно скачать образы (это те образы которые нужны для старта Gitlab и Gitlab_runner а также для работы самого раннера)

Какие образы должны быть:

```
gitlab/gitlab-ce:latest     - образ Гитлаба
gitlab/gitlab-runner:alpine - образ раннера
ubuntu:latest               - для работы раннера
registry.gitlab.com/gitlab-org/gitlab-runner/gitlab-runner-helper:x86_64-v16.11.0 - для работы раннера
```

Если их нет то качаем их с той машины где сть выход в инет (например с локальной):

```
docker pull ubuntu:latest               - Загружаем все те образы которые требуются их 4 шт.
docker save -o ubuntu.tar ubuntu:latest - Сохраняем в архив образ, далее копируем архив *.tar на удаленную тачку где будем запускать контейнеры Гитлаба
docker load -i ubuntu.tar               - На удаленной машине загружаем скопированный образ из архива
docker images                           - Проверяем должны быть все 4
```

После стартуем контейнеры из docker-compose.yaml 

## Регистрация раннера
1. При создании нового раннер в GUI Гитлаба, Гитлаб выдаст шаги которые необходимо выполнить Step1, Step2 и т.д. по сути важен только 1-й степ регистрация раннера
```
gitlab-runner register  --url https://gitlab.somevm.ru:4432  --token glrt-HP6dXqSJ_my7Z1yt-3q9 --tls-ca-file /usr/local/share/ca-certificates/ca.crt
```
*В конце дополнительно добавляем параметр --tls с указанием пути до серта (тут поясню, корневой серт ca.crt должен уже быть в наличии сгенеренный и смонтированный в контейнер раннера он его будет испозовать при обращении к гитлабу, вольюмы уже указаны в композ файле откуда и куда монтировать, в любом случаен можете проверить смонтировался ли корневой серт в контейнере по пути который указан в композ файле), на случай если общение раннера с гитлабом будет через https, если по http то не нужно передавать параметр --tls*

Даллее указываем все необходимые параметры при регистрации: URl гитлаба, имя раннера, среда выполнения пайплайна - docker, и образ указываем тот который скачали ubuntu:latest

2. После добавления раннера сформируется конфиг который используется раннером 'config.toml' по пути /data/docker/gitlab/etc/gitlab-runner/, открываем его на редактирование, в конце файла доб. след.:
```
pull_policy = ["never"] - чтоб раннер не шел на публичные репо и пытался пулить образы которые ему нужны (напоминаю это настройка только для закрытой сети когда нет выхода в инет), тем самы он будет искать образы локально
network_mode = "host"   - это решает ошибку с резолвом dns имени гитлаба, не является обязательной нужно смотреть лог пайплайна при сборке или же просто указать и не думать про лог
```
3. После рестартим докер композ, (заново останавливаем и стратуем) чтоб перечитался конфиг раннером

## Запуск тестовго CI
В корне репо создаете файлик с именем .gitlab-ci.yml и содержимым (в принципе можно любой тестовый пайплайн написать это как пример, проверить работу раннера):
```
build-job:
  stage: build
  script:
    - echo "Hello, $GITLAB_USER_LOGIN!"

test-job1:
  stage: test
  script:
    - echo "This job tests something"

test-job2:
  stage: test
  script:
    - echo "This job tests something, but takes more time than test-job1."
    - echo "After the echo commands complete, it runs the sleep command for 20 seconds"
    - echo "which simulates a test that runs 20 seconds longer than test-job1"
    - sleep 20

deploy-prod:
  stage: deploy
  script:
    - echo "This job deploys something from the $CI_COMMIT_BRANCH branch."
  environment: production
```
После коммита запуск пайплайна должен стартовать автоматически 

