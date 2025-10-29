# Atividade1 / CISCO PACKET TRACER
Configurando roteador CISCO (2911) com VLAN e DHCP para cada VLAN


Configurar roteador CISCO (2911) com VLAN e DHCP para cada VLAN
A. Passo 1 - Ligação dos componentes.
1. Faça a ligação dos computadores, switch e roteador, conforme a tabela disponibilizada.
B. Passo 2 – Configuração das VLANs no Switch
2. No Switch, em Config, selecione a opção VLAN Database.
3. Adicione as três VLANs, conforme a figura. (10 Financeiro, 20 Vendas, 30 Diretoria)
4. Ainda em config, selecione as interfaces e insira as VLANs conforme tabela baixo.
Interface
VLAN
FastEthernet0/1 a 0/5
VLAN 10 - Financeiro
FastEthernet0/6 a 0/10
VLAN 20 - Vendas
FastEthernet0/11 a 0/15
VLAN 30 - Diretoria
5. Já a interface GigabitEthernet0/1, vamos deixa-la com opção trunk e deixaremos marcado todas as VLANs que queremos deixar passar por essa interface. Essa ação deve ser realizada, pois queremos que as três VLANs acessem o roteador.
C. Passo 3 - Configuração do roteador
1. Vá em CLI no roteador.
2. Coloque o roteador no modo configuração digitando os seguintes comandos:
enable
configure terminal
3. Entre na configuração da interface Gig0/0 digitando o seguinte comando:
int Gig0/0
4. Habilite a interface Gig0/0, digitando o seguinte comando:
no shutdown
5. Crie a subinterface
Digite o comando exit
Para criar a primeira subinterface digite:
int Gig0/0.1
6. Informe informar à subinterface, a qual VLAN ela pertence (VLAN 10), como o comando:
encapsulation dot1Q 10
7. Insira um IP para a subinterface (tem que ser um IP da VLAN). Digite o comando:
ip address 192.168.10.1 255.255.255.0
8. Crie o pool de DHCP
Digite o comando exit.
Digite o mando abaixo para criar o pool com o nome VLAN-10:
ip dhcp pool VLAN-10
9. Forneça a rede em que o DHCP irá fornecer IPs, conforme o comando abaixo:
network 192.168.10.0 255.255.255.0
10. Informe o gateway padrão da rede, com o comando:
default-router 192.168.10.1
11. Informe o servidor DNS desse pool. Pode ser informado mais de um DNS. Digite o comando abaixo:
dns-server 8.8.8.8
12. Reserve os IPs que não devem ser fornecidos pelo DHCP.
Digite exit, e depois:
ip dhcp excluded-address 192.168.10.1 192.168.10.10
Clique em ctrl + c para encerrar a configuração.
OBS:
Para adicionar as demais subinterfaces e os novos pools de DHCP, deixe o roteador no modo de configuração (Router (config)#) e repita os passos a partir do item 5, com o comando int Gig0/0.x (onde o x é a nova subinterface).
13. Verifique se os computadores estão recebendo as configurações de IP de forma dinâmica.
D. Comandos interessantes.
a) Ver IPs reservados, digite:
show running-config | include excluded-address
b) Ver o status do DHCP no roteador, digite:
show running-config | section dhcp
c) Ver os IPs distribuídos, digite:
show ip dhcp binding
d) Mostrar os pool de DHCP, digite:
show ip dhcp pool
e) Desfazer a reserva de IP, digite:
no ip dhcp excluded-address 192.168.10.1 192.168.10.10
f) Para apagar o pool criado, digite:
Digite config e depois
no ip dhcp pool <nome_do_pool>
