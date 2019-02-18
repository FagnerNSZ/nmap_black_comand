# nmap_black_comand



Truques mágicos com o Nmap
10/09/2018
O Nmap é uma ferramenta muito utilizada no mundo da segurança da informação para fazer análises em redes tanto de maneira externa quanto de maneira interna. E neste artigo abordaremos técnicas de anonimato com o Nmap para demonstrar como alguém mal intencionado pode consultar um alvo passando despercebido.

Com o Nmap é possível encontrar brechas em servidores externamente que são apontadas pela própria ferramenta e fazer muito mais além disso. Em uma rede interna, por exemplo, é possível descobrir endereços físicos (MAC) de dispositivos eletrônicos conectados naquela rede, contribuindo, assim, para um ataque de redirecionamento (Spoofing) em redes internas ou podendo ocasionar na exploração de dispositivos com o Metasploit.

Alguns comandos com Nmap em rede externa:

Detectando falhas em servidores utilizando o método de saída do tipo verbose -v
nmap -sS -v -Pn -A --open --script=vuln + IP do Alvo
(Descobre a vulnerabilidade do servidor com aquele endereço de IP especificamente)
Analisando vulnerabilidades em mais endereços de IP de uma rede
nmap -sS -v -Pn -A --open --script=vuln + IP alvo/24
Descobrindo portas abertas, versões de serviços e sistema operacional que está rodando no alvo.
nmap -v –sV -Pn -O —open + IP do alvo
(O argumento “-O” pode ser substituído pelo argumento “-A”)
Realizando pesquisas sobre alvos
nmap –script=asn-query,whois-ip,ip-geolocation-maxmind + IP do alvo
Burlando firewall
*Existem 3 maneiras diferentes de burlar um Firewall em uma rede externa:
nmap -f -sV -A + IP do alvo (Neste comando ocorre a fragmentação de pacotes que serão enviados para se conectar ao alvo)
nmap -sS -sV -A + IP do alvo (Faz varreduras do tipo SYN na rede alvo)
nmap -Pn -sV -A + IP do alvo (Não enviar pacotes ICMP para o alvo, ou seja, não pingar na rede)
Mandando um recado para o admin que está do outro lado da rede
nmap –sS www.alvo.com —verbose –data-string “Você está sendo ownado, admin!”
Buscando falhas de DDoS
nmap -sU -A -PN -n -pU:19,53,123,161 –script=ntp-monlist,dns-recursion,snmp-sysdescr + IP do alvo
Fazendo brute-force no banco de dados do alvo
nmap --script=mysql-brute + IP do alvo
Alguns comandos com Nmap em rede interna:

Analisando IP e endereços de MAC de dispositivos em uma rede
nmap 192.168.0.1/24
(IP do Gateway da rede / 24)
Como fazer menos ruídos o possível ao se fazer analise em uma rede interna para não ser banido

O fato de não se fazer muito barulho na rede deve-se ao fato de não realizar a busca de endereços do MAC e para que isso não ocorra, utilizamos o comando “–send-ip”. Exemplo:

nmap –T0 –send-ip 192.168.0.1/24 (O parâmetro “-T0” é utilizado para se fazer um Scan mais demorado na rede a ponto de não levantar tanta suspeita do alvo).

*Se o alvo estiver fora da rede, a opção “–send-ip” pode ser ignorada com segurança.

Para mais comandos avançados conheça nossa ferramenta: https://hackersec.com/hnmap/
