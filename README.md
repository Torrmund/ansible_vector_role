Роль для установки и настройки Vector
===============================================================

Позволяет установить Vector и сконфигурировать отправку логов из файлов через него в Clickhouse

По умолчанию рассматривается кейс, когда через Vector в Clickhouse отправляются логи nginx из /var/log/nginx/access.log

Соответственно, для использования роли на вашем хосте должен быть установлен nginx.

Requirements
------------

* Ansible >= 2.9

Установка Vector при помощи данной роли должна выполняться через учетную запись с sudo правами.

Совместимость роли проверена только для платформ, указанных в meta.

Role Variables
--------------

| Name                                           | Default Value              | Description                                                                                                                                                                                                       |
| ---------------------------------------------- | -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `vector_systemd_user`                        | vector                     | Пользователь, от имени которого будет запускаться Vector                                                                                                               |
| `vector_systemd_group`                       | vector                     | Группа от имени которой будет запускаться Vector                                                                                                                              |
| `vector_version`                             | "0.42.0"                   | Версия Vector для установки                                                                                                                                                                     |
| `vector_sources`                             | см. в defaults/main.yml | Перечень источников логов, в роли которых выступают файлы.<br />Этот перечень в последствии передается в конфиг Vector. |
| `vector_transforms`                          | см. в defaults/main.yml | Перечень трансформирования логов для отправки в Clickhouse                                                                                                              |
| `vector_clickhouse_connection_ip`            | "localhost"                | IP адрес сервера Clickhouse для подключения к нему Vector                                                                                                                          |
| `vector_clickhouse_connection_database_name` | "logs"                     | Имя базы данных Clickhouse в которую будут отправляться логи.                                                                                                           |
| `vector_clickhouse_connection_table_name`    | "logs"                     | Имя таблицы Clickhouse, в которую будут отправляться логи.                                                                                                                 |
| `vector_clickhouse_auth_required`            | false                      | Ключ. Указывает, требуется ли аутентификация при подключении к Clickhouse                                                                                    |
| `vector_clickhouse_connection_user`          | ""                         | Имя пользователя при аутентификатции в Clickhouse                                                                                                                               |
| `vector_clickhouse_connection_password`      | ""                         | Пароль при аутентификации в Clickhouse                                                                                                                                                    |
| `vector_config_custom`                       | false                      | Ключ. Указывает, использовать ли кастомную конфигурацию Vector или применить<br />конфигурацию по умолчанию.                   |

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: vector
      roles:
         - vector

License
-------

MIT
