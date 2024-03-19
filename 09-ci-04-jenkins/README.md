# Домашнее задание к занятию 10 «Jenkins»

## Подготовка к выполнению

1. Создать два VM: для jenkins-master и jenkins-agent.
2. Установить Jenkins при помощи playbook.
3. Запустить и проверить работоспособность.
4. Сделать первоначальную настройку.

## Основная часть

1. Сделать Freestyle Job, который будет запускать `molecule test` из любого вашего репозитория с ролью.
![Снимок экрана от 2024-03-16 04-40-38](https://github.com/arklucis/CI-CD/assets/154414081/c96da8ad-51b8-4cd3-a2d4-0e4aa4fd34e3)

2. Сделать Declarative Pipeline Job, который будет запускать `molecule test` из любого вашего репозитория с ролью.
![Снимок экрана от 2024-03-16 04-36-03](https://github.com/arklucis/CI-CD/assets/154414081/a2e0a8a8-4f72-4c87-a032-6baf7e981d0a)
![Снимок экрана от 2024-03-16 04-45-35](https://github.com/arklucis/CI-CD/assets/154414081/e4ccf5ac-ad46-423f-a789-6f02ad94e6e8)

3. Перенести Declarative Pipeline в репозиторий в файл `Jenkinsfile`.
![Снимок экрана от 2024-03-16 04-57-38](https://github.com/arklucis/CI-CD/assets/154414081/f39a0a74-6f4a-4ebd-969e-67b3c4ac54ae)
![Снимок экрана от 2024-03-16 04-58-45](https://github.com/arklucis/CI-CD/assets/154414081/fd8f38df-f34b-4bff-aa44-3f258c98b0f4)

5. Создать Multibranch Pipeline на запуск `Jenkinsfile` из репозитория.
![Снимок экрана от 2024-03-18 15-06-29](https://github.com/arklucis/CI-CD/assets/154414081/766c00c0-ea5d-4280-ac9f-976afe0dfdfa)

6. Создать Scripted Pipeline, наполнить его скриптом из [pipeline](./pipeline).
7. Внести необходимые изменения, чтобы Pipeline запускал `ansible-playbook` без флагов `--check --diff`, если не установлен параметр при запуске джобы (prod_run = True). По умолчанию параметр имеет значение False и запускает прогон с флагами `--check --diff`.
![Снимок экрана от 2024-03-19 16-48-59](https://github.com/arklucis/CI-CD/assets/154414081/ca015d15-da9f-4e0c-8e02-228160f29a14)

8. Проверить работоспособность, исправить ошибки, исправленный Pipeline вложить в репозиторий в файл `ScriptedJenkinsfile`.
![Снимок экрана от 2024-03-19 17-02-53](https://github.com/arklucis/CI-CD/assets/154414081/03b97029-3d03-4eea-b29f-5ad67b28304b)

9. Отправить ссылку на репозиторий с ролью и Declarative Pipeline и Scripted Pipeline.

[Declarative Pipeline](https://github.com/arklucis/Ansible.git)

[Scripted Pipeline](https://github.com/arklucis/JAVA.git)

10. Сопроводите процесс настройки скриншотами для каждого пункта задания!!

## Необязательная часть

1. Создать скрипт на groovy, который будет собирать все Job, завершившиеся хотя бы раз неуспешно. Добавить скрипт в репозиторий с решением и названием `AllJobFailure.groovy`.
2. Создать Scripted Pipeline так, чтобы он мог сначала запустить через Yandex Cloud CLI необходимое количество инстансов, прописать их в инвентори плейбука и после этого запускать плейбук. Мы должны при нажатии кнопки получить готовую к использованию систему.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---
