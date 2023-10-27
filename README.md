rabbitmq
---

Configure and run RabbitMQ from Docker image as systemd.service.


### Links
- <https://rabbitmq.com>
- <https://hub.docker.com/_/rabbitmq>


### Variables
- **`rabbitmq_docker_image`** *(type=string, default=rabbitmq:latest)* - Docker image for using into systemd.service.

- **`rabbitmq_docker_network`** *(type=string, default=bridge)* - Connect a container to a network as `docker run --network=...`.
- **`rabbitmq_docker_publish_ports`** *(type=string, default=["5672:5672"])* - List of strings for publish a container’s ports to the host as `docker run --publish=...`.

- **`rabbitmq_docker_labels`** *(type=string, default=[])* - List of objects in format `{key: value}` for set meta data on a container as `docker run --label=...`.

- **`rabbitmq_uid`** & **`rabbitmq_gid`** *(type=number, default=5672)* - System user and group for run RabbitMQ and store data.

- **`rabbitmq_admin_password`** *(type=string, mandatory)* - RabbitMQ admin password.

- **`rabbitmq_main_config`** *(type=string, mandatory)* - Multiline string with content for RabbitMQ main config (`/etc/rabbitmq/rabbitmq.conf`).
- **`rabbitmq_advanced_config`** *(type=string, default="[].")* - Multiline string with content for RabbitMQ advanced config (`/etc/rabbitmq/advanced.config`).

- **`rabbitmq_ssl_files`** *(type=list, default=[])* - List of objects in format `{filename: "", content: ""}`, where `filename` - filename in `/etc/rabbitmq/ssl/` and `content` - multiline string with certificate (certificate chain) or private key, needed for SSL.

- **`rabbitmq_plugins`** *(type=list, default=[])* - List of RabbitMQ plugins for enabling.

- **`rabbitmq_vhosts`** *(type=list, default=[])* - List of objects in format `{*name: "", state: "present|absent"}`, when `*` is require, for RabbitMQ vhosts management.  
  Detailes in <https://docs.ansible.com/ansible/latest/collections/community/rabbitmq/rabbitmq_vhost_module.html>.

- **`rabbitmq_users`** *(type=list, default=[])* - List of objects in format `{*username: "", *password: "", tags: [], vhost: "", read_priv: "", write_priv: "", configure_priv: "", topic_permissions: "", state: "present|absent"}`, when `*` is require, for RabbitMQ users management.  
  Detailes in <https://docs.ansible.com/ansible/latest/collections/community/rabbitmq/rabbitmq_user_module.html>.


### Examples
```yaml
rabbitmq_docker_image: rabbitmq:3.12.7-alpine
rabbitmq_docker_network: host
rabbitmq_admin_password: !vault |
  $ANSIBLE_VAULT;1.1;AES256
  ...
rabbitmq_main_config: |
  log.file = false
  log.console = true
  log.console.level = debug
  log.console.formatter = plaintext
rabbitmq_plugins: [rabbitmq_management]
rabbitmq_users:
  - username: test
    password: !vault |
      $ANSIBLE_VAULT;1.1;AES256
      ...
    tags: [administrator, management]
    read_priv: .*
    write_priv: .*
    configure_priv: .*
```
