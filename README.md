<p><b>01.</b> Criar uma máquina virtual linux ubuntu 22.04 LTS no VirtualBox.</p>

[🔗 Criando uma Máquina Linux no VirtualBox](https://www.youtube.com/watch?v=7FCYFy0J4NQ) | [🔗 UBUNTU 22.04.1 LTS](https://ubuntu.com/download/desktop)
<p><b>02.</b> O usuário root deve vir configurado com a senha "unip".</p>
<p><b>03.</b> Cadastrar como usuários desta máquina virtual cada um dos integrantes do grupo, onde o usuário é definido como a primeira letra do nome concatenada ao sobrenome. Exemplo: João da Silva --> jsilva.</p>
<p><b>04.</b> A senha de cada usuário deve ser o código correspondente ao seu RA na UNIP.</p>
<p><b>05.</b> Configure os parâmetros de rede para que a máquina tenha acesso a internet.</p>
<p><b>06.</b> Instalar o serviço de firewall de modo que ele suba na inicialização do SO e configure o mesmo para <b><i>bloquear todas a portas</i></b> menos as 80, 8080 e 422.</p>

[🔗 Como utilizar o Iptables (Netfilter)](https://terminalroot.com.br/2014/11/como-utilizar-o-iptables-netfilter.html)

```
iptables -A INPUT -p tcp --destination-port 80 -j ACCEPT
iptables -A INPUT -p tcp --destination-port 8080 -j ACCEPT
iptables -A INPUT -p tcp --destination-port 422 -j ACCEPT
iptables -A INPUT -p tcp --syn -j DROP

# para ver se funcionou
iptables -L
```

<p><b>07.</b> Criar um script (/home/root/monitor.sh) que colete informações do sistema como: hora atual da coleta dos dados; tempo decorrido desde o último reboot; ocupação do disco e suas partições; memória total e ocupada; usuários logados sistema.</p>

```
# Linux Terminal
touch monitor.sh
nano monitor.sh
```
------------
```
# Arquivo Shell Script
# !/bin/bash
now=$(date)
echo "Data e Hora atuais: $now"
last_reboot=$(awk '{print int($1/3600)":"int(($1%3600)/60)":"int($1%60)}' /proc/uptime)
echo "Tempo decorrido desde o último reboot: "
disk_usage=$(df -H --output=source,size,used,avail,pcent)
echo -e "Uso de Disco: \n$disk_usage"
user_login=$(who)
echo -e "Usuários que estão logados:\n$user_login"
```

<p><b>08.</b> Faça o agendamento deste script usando o serviço cron/crontab para que a partir do boot do sistema, ele colete estas informações periodicamente a cada 10 minutos, somente nos dias uteis de trabalho (segunda a sexta-feira). As informações atuais coletadas, devem ser concatenadas às coletadas em iterações anteriores. Estas informações devem ser persistidas no arquivo /var/log/monitor.log.</p>
<p><b>09.</b> Instalar o serviço de proxy usando o squid e crie regras de bloqueio dos sites de redes sociais como: facebook; youtube; instagram.</p>

