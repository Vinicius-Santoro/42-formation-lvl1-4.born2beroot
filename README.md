<h1>42-formation-lvl1-4.born2beroot</h1>

### _Project 4: born2beroot - Fourth project for the formation of software engineers at school 42 São Paulo._

- This project consists of configuring a debian operating system without a graphical interface.

<h1></h1>
### _Para entender o projeto, primeiro deve-se saber alguns termos importantes, sendo eles:_
- <b>CentOS</b>: é uma das distribuições `Linux®`. Comumente usada para administração de servidores.
- <b>KDump</b>: serve para o monitoramento do sistema. É um mecanismo de despejo do travamento do kernel. Esse despejo do travamento seria uma captura de informações do sistema que podem ser valiosas ao determinar a causa do travamento. Ou seja, são informações das causas que levaram o sistema a travar. (Para o CentOS).
- <b>SELinux</b>: o `Security-Enhanced Linux®`, também conhecido como `SELinux`, é uma arquitetura de segurança para sistemas Linux® que permite que administradores tenham mais controle sobre quem pode acessar o sistema. Usaremos isso para construir nossa política de segurança das senhas do sistema. (Para o CentOS).
- <b>Debian</b>: é uma das distribuições `Linux®` open-source. É a mãe de todas as outras distribuições. É como se fosse o C das linguagens de programação.
- <b>AppArmor</b>:  tem o mesmo funcionamento do `SELinux`, só que para o `Debian`.
- <b>LVM</b>: o `Logical Volume Manager` é um método de alocar espaço do disco rígido em volumes lógicos que podem ser facilmente redimensionados, ao contrário das partições.
- <b>Particionamento</b>: é quando há uma particão de um disco, podendo ser lógico ou rígido. Exemplo: <br>
200GB (disco rígido) ->  150GB (disco rígido) 50GB (partição específica);



---


### _0.Instalando o sudo:_
| Ordem |               Descrição                    |        Comando       |
|-------|--------------------------------------------|----------------------|
|   1º  | Entrar como root                           | `su -`               |
|   2º  | Instalar o sudo no sistema operacional     | `apt install sudo`   |
|   3º  | Dar permissão para o usuário             | `usermod -aG sudo <user42>`|


---


### _1.Criando um particionamento encriptado:_

<img align="center" src="https://github.com/cadetes-42/born2beroot/blob/main/Images/1.Particionamento-Encriptado.png" widht="350"/>


---


### _2.Configurando o sistema operacional com o firewall UFW (Uncomplicated Firewall ou Firewall descomplicado) e deixando apenas a porta 4242 aberta:_
Primeiro, devemos saber o que é o `firewall UFW`. O `firewall UFW` é um gerenciador simplificado de firewall que esconde a complexidade das tecnologias de filtragem de pacotes de baixo nível. Se desejamos começar a proteger a rede, mas não temos certeza sobre qual ferramenta usar, o UFW é a escolha certa para nós.
Para fazermos isso, devemos usar os seguintes comandos:

| Ordem |               Descrição                    |        Comando       |
|-------|--------------------------------------------|----------------------|
|   1º  | Instalar o ufw no sistema operacional                  | `sudo apt install ufw`|
|   2º  | Ativar o ufw no sistema operacional                  | `ufw enable` |
|   3º  | Permitir a execução do ufw no sistema operacional    | `systemctl enable ufw` |
|   4º  | Deixar apenas a porta 4242 aberta                    | `ufw allow 4242` |
|   5º  | Checar as portas abertas (Aparecerá os protocolos IPV4 e IPV6) | `ufw status `|


---


### _3.Criando chave ssh:_
| Ordem |               Descrição                    |        Comando       |
|-------|--------------------------------------------|----------------------|
|   1º  | Instalar o ufw no sistema operacional                  | `sudo apt install ufw`|
|   2º  | Ativar o ufw no sistema operacional                  | `ufw enable` |

---

### _4.Implementando política de senha forte:_
| Ordem |               Descrição                    |        Flag       |
|-------|--------------------------------------------|----------------------|
|   01º | Expiração da senha a cada 30 dias.       | `sudo apt install ufw`|
|   02º | Modificação de senha deve ser no mínimo 2 dias. | `fgh`|
|   03º | Pelo menos 10 caracteres. |`f`|
|   04º | Pelo menos um letras maiúscula.| `fgh` |
|   05º | Pelo menos 1 número.| `f` |
|   06º | Não deve conter 3 caracteres idênticos consecutivos.| `f` |
|   07º | Não deve incluir o nome do usuário.| `f` |
|   08º | A autenticação usando sudo deve ser limitada a 3 tentativas no caso de um erro senha correta. | `f` |
|   09º | Mensagem personalizada de erro ao usar o sudo. | `f` |
|   10º | Cada ação usando o sudo deve ser salva na pasta: /var/log/sudo/ | `f` |
|   11º |  O modo TTY deve ser ativado por motivos de segurança. | `f` |

---

### _5.Criação do monitoring.sh:_
A cada 10 minutos, o script deve exibir as seguintes informações:
- A arquitetura do seu sistema operacional e sua versão do kernel.
- O número de processadores físicos.
- O número de processadores virtuais.
- A RAM disponível atualmente em seu servidor e sua taxa de utilização como uma porcentagem.
- A memória atual disponível em seu servidor e sua taxa de utilização como uma porcentagem.
- A taxa de utilização atual de seus processadores como uma porcentagem.
- A data e hora da última reinicialização.
- Se o LVM está ativo ou não.
- O número de conexões ativas.
- O número de usuários usando o servidor.
- O endereço IPv4 do seu servidor e seu endereço MAC (Media Access Control).
- O número de comandos executados com o programa sudo.


---


### _5.Modificando o nome do host - `user42` (Apenas durante a avaliação):_
| Ordem |               Descrição                    |        Comando       |
|-------|--------------------------------------------|----------------------|
|   1º  | Entrar como root                           | `su -`               |
|   2º  | Entrar como root                           | `su -`               |
|   3º  | Entrar como root                           | `su -`               |
