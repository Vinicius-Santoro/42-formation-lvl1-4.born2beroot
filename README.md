<h1>42-formation-lvl1-3.printf</h1>

### _Project 4: born2beroot - Fourth project for the formation of software engineers at school 42 São Paulo._

- This project consists of create my first machine in VirtualBox under specific instructions. 

<h1></h1>

### _Como este projeto é voltado para o aprendizado de administração de sistemas operacionais, decidi colocar tudo o que usei para desenvolvê-lo. Boa leitura :)_

<h1></h1>

### _O que é uma Maquina virtual, como ela funciona e qual a utilidade_

   - <b>O que é</b>: é um recurso de computação que usa software em vez de um computador físico para executar programas e implantar aplicativos.
   - <b>Como funciona</b>: funciona trabalhando por meio da tecnologia de `virtualização`. A virtualização usa software para simular hardware virtual que permite VMs para execução em uma única máquina host.
   - <b>Qual a utilidade</b>: as VMs podem ser implantadas para acomodar diferentes níveis de necessidades de poder de processamento, para executar software que requer um diferente sistema operacional ou para testar aplicativos em um ambiente seguro em área restrita.

<h1></h1>

### _Quais as diferenças entre o Debian e o CentOS_
  
Os dois sistemas são de distribuição `Linux`, logo de código aberto, porém possuem algumas
diferenças.
   - <b>Debian</b>: é considerado mais de classe pessoal/doméstica, já que é utilizado pela maioria da
comunidade nesse ambiente.
   - <b>CentOs</b>: é considerado mais de classe empresarial, isso pelo fato de receber atualizações
com pouca frequência, o que torna ele um sistema mais estável que o Debian.

<h1></h1>

### _Quais as diferenças entre apt e aptitude_

`Aptitude` e `apt-get` são duas das ferramentas populares que tratam do gerenciamento de pacotes. Ambos são capazes de lidar com todos os tipos de atividades em pacotes, incluindo instalação, remoção, pesquisa, etc. 

   - <b>apt</b>: é um gerenciador de pacotes padrão do `debian`, e é mais antigo. 
   - <b>aptitude</b>: é um gerenciador de pacotes `front-end` para uma ferramenta de empacotamento avançada que adiciona uma interface de usuário à funcionalidade, permitindo ao usuário pesquisar interativamente por um pacote e instalá-lo ou removê-lo. 
 
 Ou seja, apt é raíz e o aptitude é mais amigável.

<h1></h1>

### _Quais as diferença entre SELinux e AppArmor_

   - <b>SELinux:</b> o `Security-Enhanced Linux®`, também conhecido como `SELinux`, é uma arquitetura de segurança para sistemas `Linux®` que permite que administradores tenham mais controle sobre quem pode acessar o sistema (Para o `CentOS`).
   - <b>AppArmor</b>: tem o mesmo funcionamento do `SELinux,` só que para o `Debian`.

<h1></h1>

### _O que é UFW?_

É uma ferramenta de configuração de firewall, que é um dispositivo de segurança de
rede que cuida do trafego de informações bloqueando ou permitindo passagens de dados
dependendo das regras configuradas.

<h1></h1>

### _O que é SSH?_

É um protocolo utilizado pra troca de dados entre cliente e servidor remoto de forma
segura e dinâmica. Ele possibilita a comunicação criptografada através da rede permitindo
acessar e fazer alterações em outro computador através do terminal.

---


### _0.Instalando o sudo:_
| Ordem |               Descrição                   	|		Comando			|
|-------|-----------------------------------------------|---------------------------------------|
|   1º  | Entrar como root                           	| `su - `               		|
|   2º  | Instalar o sudo no sistema operacional     	| `apt install sudo`			|
|   3º  | Dar permissão para o usuário			| `usermod -aG sudo <seu usuário>`	|
|   4º  | Criar um novo grupo				| `groupadd user42` 			|
|   4º  | Adcionando o usuário ao novo grupo		| `usermod -aG user42 <seu usuário>`	|

---


### _1.Criando um particionamento encriptado:_

<img align="center" src="https://github.com/cadetes-42/born2beroot/blob/main/Images/1.Particionamento-Encriptado.png" widht="350"/>

<!--
### _Adicionando os volumes lógicos:_

<a src="https://github.com/cadetes-42/born2beroot/blob/main/Images/LVM.mp4"><\a>

-->

<a href="https://youtu.be/fWlsaIOYoJo" target="_blank">
 <img src="https://github.com/cadetes-42/born2beroot/blob/main/Images/mq2.jpg" alt="Watch the video" width="240" height="180" border="10" />
</a>

<!--
https://youtu.be/fWlsaIOYoJo
-->

### _2.Configurando o sistema operacional com o firewall UFW (Uncomplicated Firewall ou Firewall descomplicado) e deixando apenas a porta 4242 aberta:_
Primeiro, devemos saber o que é o `firewall UFW`. O `firewall UFW` é um gerenciador simplificado de firewall que esconde a complexidade das tecnologias de filtragem de pacotes de baixo nível. Se desejamos começar a proteger a rede, mas não temos certeza sobre qual ferramenta usar, o UFW é a escolha certa para nós.
Para fazermos isso, devemos usar os seguintes comandos:

| Ordem |               Descrição 					|        Comando      	 |
|-------|---------------------------------------------------------------|------------------------|
|   1º  | Instalar o ufw no sistema operacional				| `sudo apt install ufw` |
|   2º  | Ativar o ufw no sistema operacional                 		| `ufw enable`		 |
|   3º  | Permitir a execução do ufw no sistema operacional		| `systemctl enable ufw` |
|   4º  | Deixar apenas a porta 4242 aberta                 		| `ufw allow 4242`	 |
|   5º  | Checar as portas abertas (Aparecerá os protocolos IPV4 e IPV6)| `ufw status `		 |


---


### _3.Permitindo acesso ssh:_
| Ordem |               Descrição                  	|        Comando	|
|-------|-----------------------------------------------|-----------------------|
|   1º  | Instalar o SSH no sistema operacional		| `sudo apt install ssh openssh-server openssh-client`	|
|   2º  | Ativar o SSH no sistema operacional		| `systemctl enable sshd` 				|
|   3º  | Editar as confiurações do ssh			| `nano /etc/ssh/sshd_config` 				|
|   4º  | Alterar a porta de acesso padrão		| `#Port 22` >> `Port 4242`				|
|   5º  | Reiniciando o serviço				| `systemctl restart sshd`				|
|   6º  | Checando os soquetes				| `ss -tunlp`						|
|   7º  | Testando a conexão				| `ssh <seu usuário>@<seu ip> -p 4242`			|
 				
---

### _4.Implementando política de senha forte:_

#### _4.1.Alterando a data de expiração_
| Ordem |               Descrição                   		|        Flag			|
|-------|-------------------------------------------------------|-------------------------------|
|   1º	| Encontrar no arquivo de login e alterar as flags	| `sudo nano /etc/login.defs/`	|
|   2º 	| Expiração da senha a cada 30 dias			| `PASS_MAX_DAYS 30`		|
|   3º 	| Modificação de senha deve ser no mínimo 2 dias 	| `PASS_MIN_DAYS 2`		|
|   4º	| Receber um alerta 7 dias antes da expiração		| `PASS_WARN_AGE 7`		|
|   5º	| Entra como root		| `su -`		|
|   6º	| Aplicar alteração nos usuarios existentes	(fora de login.defs)	| `chage -M30 -m2 -W7 <usúario>`|
|   7º  | Verificando as mudanças				| `chage -l <usúario>`		|

<h1></h1>

#### _4.2.Definindo uma senha forte_
| Ordem |               Descrição                   		|        Flag   			|
|-------|-------------------------------------------------------|---------------------------------------|
|   1º	| Instalar o pacote libpam-security para facilitar	| ```sudo apt install libpam-pwquality```	|
|   2º	| Fazer alterações no seguinte arquivo			|`sudo nano /etc/security/pwquality.conf`|
|   3º	| Pelo menos 10 caracteres 				| `minlen = 10`		|
|   4º	| Pelo menos um letras maiúscula			| `ucredit = -1`	|
|   5º	| Pelo menos 1 número				| `dcredit = -1` 	|
|   6º	| Não deve conter 3 caracteres idênticos consecutivos	| `maxrepeat = 3`	|
|   7º	| Não deve incluir o nome do usuário			| `usercheck = 1`	|
|   8º	| A autenticação usando sudo deve ser limitada a 3 tentativas	| `retry = 3`	|
|   9º	| Para aplicar toda a política acima para o root	| `retry = 3`	|

<h1></h1>

#### _4.3.Configurando a segurança de login_
| Ordem |               Descrição                   		|        Flag   			|
|-------|-------------------------------------------------------|---------------------------------------|
|   1º | Adicionar as configurações no arquivo			| `sudo nano /etc/sudoers`              |
|   2º | Mensagem personalizada de erro ao usar o sudo 	| `Defaults     badpass_message="<sua mensagem>"` |
|   3º | Cada ação usando o sudo deve ser salva na pasta:	| `Defaults	logfile="/var/log/sudo/sudo.log"`<br>`Defaults	log_input,log_output`	|
|   4º | O modo TTY deve ser ativado por motivos de segurança	| `Defaults        requiretty`		|
|   5º | Limitando o maximo de tentativa a 3			| `Defaults     passwd_tries=3`		|

---

### _5.Criação do monitoring.sh:_

O PDF pede para criarmos um script de monitoramento chamado: monitoring.sh. Esse script deverá exibir as seguintes informações:

- A arquitetura do seu sistema operacional e sua versão do kernel;
- O número de processadores físicos;
- O número de processadores virtuais;
- A RAM disponível atualmente em seu servidor e sua taxa de utilização como uma porcentagem;
- A memória de disco (HD) atual disponível em seu servidor e sua taxa de utilização como uma porcentagem;
- A taxa de utilização atual de seus processadores como uma porcentagem;
- A data e hora da última reinicialização;
- Se o LVM está ativo ou não;
- O número de conexões ativas;
- O número de usuários usando o servidor;
- O endereço IPv4 do seu servidor e seu endereço MAC (Media Access Control);
- O número de comandos executados com o programa sudo.

Veja como o código ficou:

```bash
#!bin/bash
ARCHITECTURE=$(uname -a)
CPU=$(cat /proc/cpuinfo | grep 'physical id' | wc -l)
VIRTUALCPU=$(cat /proc/cpuinfo | grep 'processor' | wc -l)
TOTALRAM=$(free -m | grep "Mem.:" | awk '{print $3}')
USAGERAM=$(free -m | grep "Mem.:" | awk '{print $2}')
PERCENTRAM=$(free -m | grep "Mem.:" | awk '{printf("%.2f"), $3/$2*100}')
DSK1=$(df -m --total | grep "total" | awk '{print $3}')
DSK2=$(df -h --total | grep "total" | awk '{printf ("%.0f"), $2}')
DSK3=$(df -h --total | grep "total" | awk '{print $5}')
LCPU=$(top -bn1 | grep '^%Cpu' | awk '{printf("%.1f%%"), $2 + $4}')
LASTBOOT=$(who -b | awk '{print $4 " " $5 }')
USAGELVM=$(lsblk | if grep -q "lvm";then echo "yes"; else echo "no"; fi)
TCP=$(netstat | grep "tcp" | wc -l)
TCPM=$(netstat | if grep -q "tcp";then echo "ESTABLISHED";else echo "NOT ESTABLISHED"; fi)
LOGGEDUSERS=$(users |wc -w)
NET=$(hostname -I | awk '{print $1}')
MAC=$(ip link show | awk '$1 == "link/ether" {print $2}')
SUDO=$(cat /var/log/sudo/sudo.log | grep 'COMMAND' | wc -l)

wall "
        #Architecture: $ARCHITECTURE
        #CPU physical: $CPU
        #vCPU: $VIRTUALCPU
        #Memory Usage: $TOTALRAM/${USAGERAM}MB ($PERCENTRAM%)
        #Disk Usage: $DSK1/${DSK2}GB ($DSK3)
        #CPU load: $LCPU
        #Last boot: $LASTBOOT
        #LVM use: $USAGELVM
        #Connections TCP: $TCP $TCPM
        #User log: $LOGGEDUSERS
        #Network: IP $NET $MAC
        #Sudo: $SUDO cmd

"
```

Veja detalhadamente como fizemos isso:

    #!bin/bash
    
_Esta informação é necessária para sabermos o caminho completo do interpretador desejamos utilizar para execução do comando. No nosso caso, sem ela também é possível executar o script, pois por default, o shell do Unix executa shell scripts._

<h1></h1>

    $(uname -a)
_Usamos este comando para exibir as informações da arquitetura do sistema operacional._

<img align="center" src="https://github.com/cadetes-42/born2beroot/blob/main/Images/2.Broadcast-Message.png" widht="350"/>

- **Vermelho:** _Nome do kernel_ 
- **Verde:** _Nome do host_ 
- **Azul Claro:** _Versão do kernel_ 
- **Rosa:** _Versão do SMP. O SMP significa Symmetric multiprocessing or shared-memory multiprocessing. É a versão do multiprocessamento simétrico do sistema operacional_
- **Amarelo:** _Data de criação do sistema operacional_ 
- **Azul Escuro:**  _Versão da arquitetura do sistema operacional_ 

<h1></h1>

    (cat /proc/cpuinfo \| grep 'physical id' \| wc -l)
    
_Usamos este comando para exibir a quantidade de CPU's físicas._    

- `cat /proc/cpuinfo`: _Acessa o arquivo proc e depois o cpuinfo;_
- `grep 'physical id' `:  _Busca a palavra chave 'physical id' no arquivo cpinfo;_
- `wc -l`: _Conta a quantidade de vezes que aparece as palavras 'physical id' e retorna essa quantidade._

<h1></h1>

    (cat /proc/cpuinfo \| grep 'processor' \| wc -l)
    
_Usamos este comando para exibir a quantidade de CPU's virtuais._

- `cat /proc/cpuinfo `: _Acessa o arquivo proc e depois o cpuinfo;_
- `grep 'processor'`:  _Busca a palavra chave 'processor' no arquivo cpinfo;_
- `wc -l`: _Conta a quantidade de vezes que aparece a palavra 'processor' e retorna essa quantidade._

<h1></h1>

    (free -m \| grep "Mem.:" \| awk '{print $3}')
    
_Usamos este comando para armazenara quantidade de memória RAM total._

- `free -m` _Os valores são exibidos em megabytes. Se quisessemos em gb, era só usar a flag -g;_
- `grep "Mem.:'` _Busca a palavra chave 'Mem.:' na saída de free -m;_
- `awk '{print $3}'` _O AWK é um processador de texto. Junto com o print, nós imprimimos o elemento na posição 3, que no caso é a memória._

<h1></h1>

    (free -m \| grep "Mem.:" \| awk '{printf("%.2f"), $3/$2*100}')

_Usamos este comando para armazenara quantidade de memória RAM usada._

- `free -m` _Os valores são exibidos em megabytes. Se quisessemos em gb, era só usar a flag -g;_
- `grep "Mem.:'` _Busca a palavra chave 'Mem.:' na saída de free -m;_
- `awk '{print $2}'` _O AWK é um processador de texto. Junto com o print, nós imprimimos o elemento na posição 2, que no caso é a quantidade de memória usada._

<h1></h1>

    (df -m --total \| grep "total" \| awk '{print $3}')

_Usamos este comando para exibir a quantidade de disco usado._
    
- `df -m --total`: _Exibir a quantidade de disco livre (-m: em megabytes |-Bm: em megabytes com o M no final);_
- `grep "total"`: _Busca a palavra chave 'total';_
- `3`: _Retorna o terceiro valor;_
- `-m`: _Output em megabytes;_
- `-Bm`: _Output em megabytes com símbolo 'M' no final;_
- `-h`: _Output para leitura humana (Divide por 1024);_
- DSK1: Mosta a quantidade de disco usado;
- DSK2: Mostra a quantidade de disco total;
- DSK3: Mostra a quantidade de disco usado em porcentagem.

<h1></h1>

    LASTBOOT=$(who -b | awk '{print $4 " " $5 }')
      
 _Usamos este comando para mostrar a última vez que a máquina foi bootada._ 
 
 <h1></h1>

    USAGELVM=$(lsblk | if grep -q "lvm";then echo "yes"; else echo "no"; fi)
      
 _Usamos este comando para verificar se o LVM está sendo usado ou não._
      
- Lista os blocos de partição: `lsblk`;
- Se nesse filtro, for encontrado a palavra chave `lvm`, então a saída é "yes", se não é "não";
- Para finalizar o script de condicional: `fi`;
- `-q` silenciar saída. Ou seja, não printar ela.

 <h1></h1>

    TCP=$(netstat | grep "tcp" | wc -l)
    
 _Usamos este comando para verificar se temos conexão TCP (Transmission Control Protocol)._
    
    TCPM=$(netstat | if grep -q "tcp";then echo "ESTABLISHED";else echo "NOT ESTABLISHED"; fi)
    
- Retorna a quantidade de ips;
- Se esse ip for maior ou igual a 1, então retorna "ESTABLISHED", se não retorna "NOT ESTABLISHED".

 <h1></h1>
 
     LOGGEDUSERS=$(users | wc -w)
     
_Usamos este comando para saber a quantidade de usuários logados_

- `wc -W`: word count;
- (1 linha, 2 palavras e 18 caracteres).

 <h1></h1>
 
    NET=$(hostname -I | awk '{print $1}')
       
_Usamos este comando para saber o IP da máquina virtual._

<h1></h1>
     
    MAC=$(ip link show | awk '$1 == "link/ether" {print $2}')
 
_Usamos este comando para saber os endereços MAC da máquina virtual._

<h1></h1>

   SUDO=$(cat /var/log/sudo/sudo.log | grep 'COMMAND' | wc -l)

_Usamos este comando para verificar a quantidade de comandos SUDO usados. Todos esses comando ficam na pasta `sudo.log.`_

- `wc -W`: word count;

---

_Um resumo geral:_

|       Comando         |                               Descrição                                                                                                |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `uname -a`            | _Imprime toda as informações do sistema `-s`, do kernel `-v`, e maquina `-m`_                                                          |
| `cat /proc/cpuinfo`   | _Concatena e imprime informações da CPU do pseudo-diretorio `/proc`, `PROC(5)`_                                                        |
| `grep "<padrão>"`     | _Imprime a linha de acordo com o padrão usado_                                                                                         |
| `wc -l`               | _Imprime no terminal a quantidade de linhas `-l`, palavras `-w` ou letras `-c`_                                                        |
| `free -m`             | _Mostra a quantidade de memoria livre da RAM e SWAP em mega -m, ou gigas -g_                                                           |
| `awk '{print $x}'`    | _AWK(1) é um processador de texto e de padrões.<br>É possivel imprimir um elemento na possição **x** usando a estrutura `'{print $x}'`_|
| `df -m`               | _Mostra um relatório do espaço usado no "disco". Em blocos de mega `-Bm` ou gigabits `-Bg`_                                            |
| `awk '{printf ("%.0f"), $2}'` | AWK(1) também permite a utilização de funções para imprimir formatado_                                                         |
| `top -bn1`            | _Mostra os processos do Linux com a opção de mostrar por lotes `-b` de tempo por `-n1` vezes_                                          |
| `who -b`              | _Expoe o nome do usuário que está logado e a data da ultima inicialização `-b`_                                                        |
| `lsblk`               | _Lista as partições (blocos) de armazenamento_                                                                                         |
| `Conditions`          | _É possivel usar condicionais no terminal, seguindo essa estrutura:<br><span style="color:red">if </span> 'comando' <span style="color:red">; then </span> 'comando' <span style="color:red">; fi </span>_                                                                                                          |
| `netstat`             | _`pip install netstat` Programa que imprime as conexões de rede, como a "tcp"_                                                         |
| `users`               | _Imprime os nomes dos usuários logados no hospedeiro ("Vm")_                                                                           |
| `hostname -I`         | _Imprime o nome do hospedeiro, com a opção `-i` imprime o ip e todos os ips com `-I`_                                                  |
| `ip link show`        | _Mostra os endereços de Ethernet e MAC (Controle de Acesso de Mídia)_                                                                  |
| `cat /var/log/sudo/sudo.log`  | _Imprime todos os comandos sudo registrados no arquivo `sudo.log`_                                                             |

---

