rabbitmq
---

Configure and run RabbitMQ from docker image as systemd.service.


### Links:
- <https://rabbitmq.com>
- <https://hub.docker.com/_/rabbitmq>


### Variables:
- **`rabbitmq_docker_image`** *(type=string, default=rabbitmq:latest)*
- **`rabbitmq_docker_network`** *(type=string, default=bridge)*
- **`rabbitmq_docker_publish_ports`** *(type=string, default=bridge)*
- **`rabbitmq_docker_labels`** *(type=string, default=bridge)*

- **`rabbitmq_uid`**, **`rabbitmq_gid`** *(type=number, default=5672)*

- **`rabbitmq_admin_password`** *(type=string, mandatory)*

- **`rabbitmq_config`** *(type=string, default="")*
- **`rabbitmq_config_advanced`** *(type=string, default="")*

- **`rabbitmq_ssl_files`** *(type=list, default=[])*

- **`rabbitmq_users`** *(type=list, default=[])*
- **`rabbitmq_plugins`** *(type=list, default=[])*
