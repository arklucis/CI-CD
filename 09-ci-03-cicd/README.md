# Домашнее задание к занятию 9 «Процессы CI/CD»

## Подготовка к выполнению

1. Создайте два VM в Yandex Cloud с параметрами: 2CPU 4RAM Centos7 (остальное по минимальным требованиям).
2. Пропишите в [inventory](./infrastructure/inventory/cicd/hosts.yml) [playbook](./infrastructure/site.yml) созданные хосты.
3. Добавьте в [files](./infrastructure/files/) файл со своим публичным ключом (id_rsa.pub). Если ключ называется иначе — найдите таску в плейбуке, которая использует id_rsa.pub имя, и исправьте на своё.
4. Запустите playbook, ожидайте успешного завершения.
5. Проверьте готовность SonarQube через [браузер](http://localhost:9000).
6. Зайдите под admin\admin, поменяйте пароль на свой.
7.  Проверьте готовность Nexus через [бразуер](http://localhost:8081).
8. Подключитесь под admin\admin123, поменяйте пароль, сохраните анонимный доступ.

## Знакомоство с SonarQube

### Основная часть
9. Сделайте скриншот успешного прохождения анализа, приложите к решению ДЗ.
![Снимок](https://github.com/arklucis/CI-CD/assets/154414081/e5ba5cae-e556-457c-9ff3-fc607b4ac5cb)


## Знакомство с Nexus

### Основная часть

4. В ответе пришлите файл `maven-metadata.xml` для этого артефекта.

maven-metadata.xml file [here](https://github.com/arklucis/CI-CD/blob/c08ed054f1fbfaf9e7b3f8e866d8fac9644c3d16/09-ci-03-cicd/maven-metadata.xml).


### Знакомство с Maven

### Подготовка к выполнению

1. Скачайте дистрибутив с [maven](https://maven.apache.org/download.cgi).
2. Разархивируйте, сделайте так, чтобы binary был доступен через вызов в shell (или поменяйте переменную PATH, или любой другой, удобный вам способ).
3. Удалите из `apache-maven-<version>/conf/settings.xml` упоминание о правиле, отвергающем HTTP- соединение — раздел mirrors —> id: my-repository-http-unblocker.
4. Проверьте `mvn --version`.
5. Заберите директорию [mvn](./mvn) с pom.

### Основная часть

4. В ответе пришлите исправленный файл `pom.xml`.

pom.xml file [here](https://github.com/arklucis/CI-CD/blob/c08ed054f1fbfaf9e7b3f8e866d8fac9644c3d16/09-ci-03-cicd/mvn/pom.xml).


