# Assegurando que o runtime do processo crie o arquivo pid

## Pare o serviço zabbix-agent ou zabbix-agent2
```bash
systemctl stop zabbix-agent2.service
```

## Edite o systemd do zabbix:

No systemd, os serviços são gerenciados por arquivos .service. Verifique o arquivo de configuração do serviço do Zabbix Agent, geralmente localizado em /lib/systemd/system/zabbix-agent.service ou /etc/systemd/system/zabbix-agent.service.

```bash
sudo nano /lib/systemd/system/zabbix-agent2.service
```
- 📌 **Agent:** `/lib/systemd/system/zabbix-agent2.service`
- 📌 **Server:** `/lib/systemd/system/zabbix-server.service`
- 📌 **Zabbix-Proxy:** `/lib/systemd/system/zabbix-proxy.service`


### Adicione o seguinte na seção service:
```text
[Service]
RuntimeDirectory=zabbix
```

### Atualize systemd com a nova configuração e inicie:

```bash
systemctl daemon-reload
systemctl start zabbix-agent2.service
```
Agora, o usuário zabbix terá permissão para criar o PID file: 
* /run/zabbix/zabbix_agent2.pid para o Agent
* /run/zabbix/zabbix_server.pid para o Server
* /run/zabbix/zabbix_proxy.pid para o Zabbix-Proxy
