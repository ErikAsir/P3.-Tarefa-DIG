1. Realiza unha consulta "dig danielcastelao.org" e identific cada parte da resposta (IN, CNAME, A, QUERY SECTION, ANSWER SECTION, AUTHORITY SECTION, etc)

IN → 	O apartado IN fai referencia a clase do rexistro DNS.

QUESTION SECTION:
danielcastelao.org
IN A

ANSWER SECTION
danielocastelao 900 178.211.133.37
IN A

CNAME → Este tipo de rexistro empregase para facer un alias para un dominio.

A → A principal función deste rexistro e resolver un nome de dominio a unha dirección ip.

danielcastelao.org   900  IN  A  178.211.133.37

QUERY SECTION → Mostra os detalles da consulta que se está facendo ao servidor DNS.

Question section:
danielcastelao.org   IN   A

ANSWER SECTION → Mostra a resposta que o servidor DNS ha proporcionado para a consulta realizada.

ANSWER SECTION:
danielcastelao.org  900  IN  A  178.211.133.37

AUTHORITY SECTION →Mostra os servidores de nombres autorizados, que son responsables dun dominio.

Flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

2. Realiza consutas dos seguintes nomes e identifica as diferencias: moodle.danielcastelao.org, www.danielcastelao.org

moodle.danielcastelao.org → ANSWER: 0, AUTHORITY: 1
www.danielcastelao.org    → ANSWER: 1, AUTHORITY: 0

3. Averigua o nome e IP dos servidores de DNS autoritativos de www.danielcastelao.org, por qué soen ser 2 servidores autoritativos?

dig www.danielcastelao.org NS

NS                                    IP
daniel.org                         209.204.128.117
a.auth-ns.sonic.net           157.131.0.39
c.auth-ns.sonic.net           139.178.66.139
b.auth-ns.sonic.net           150.239.18.116

4. Realiza as consultas de nomes inversas: 130.206.164.68 e de outras dúas IPs que se che ocorran.

- Para faxer este tipo de consultas temos que empregar o comando dig -x direccionIP como por exemplo:

dig -x 130.206.164.68 → pluto.tlm.unavarra.es
dig -x 8.8.8.8               → dns.google
dig -x 40.78.5.103       → ns1-201.azure-dns.com

5. A qué servidor DNS estás consultando? Cómo o podes cambiar sen tocar os ficheiros de configuración do sistema?

a) ;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
b) Podo cambiar o servidor DNS especificando uno diferente na consulta sen tocar os archivos de configuracion:

dig @8.8.8.8 danielcastelao.org

6. Obtén o rexistro SOA (Start of Authority) do dominio moodle.danielcastelao.org preguntándolle ó servidor DNS de google e logo preoguntándollo directamente ó servidor primario do dominio danielcastelao.org.

- Para obter o rexistro SOA vou empregar o seguinte comando, primero consultando o servidor de Google:
Dig @8.8.8.8 SOA moodle.danielcastelao.org

7. Consulta a IP de www.elpais.com. Cánto tempo queda almaceado o rexistro de recurso no DNS local?, se preguntas ó DNS local por este recurso, qué observas no TTL do rexistro?

- Pra consultar a IP de www.elpais.com empregare o seguinte comando:

dig www.elpais.com

- Na seccion ANSWER SECTION se pode ver o campo TTL que indica o tempo en segundos que ese rexistro estará no caché. Se volvese a preguntar por este recurso despois dun tempo o TTL deveria disminuir progresivamente

8. Busca o TTL de distintos nomes de dominio de servicios que escollas, a qué se poden deber as diferencias?

dig google.com → TTL: 186
dig instagram.com → TTL: 29
dig x.com → TTL:1800


Pode que as diferenzas debanse a temas do cache, algunos poden ter actualizaciones mais rapida ca outros





10. Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por qué?

No lo entiendo se supone que si hago dig +short  a google o facebook etc me deberian de aparecer varias ips pero solo me muestra una . _.


11. Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET por exemplo) e comproba na resposta se o server acepta o modo recursivo

- Para preguntar a un servidor raiz, empregare o seguinte comando:

dig @j.root-servers.net www.google.es

No caso de que o servidor non aceptara o modo recursivo nos lo mostraría con un flag pero en este caso non o mostra xa que acepta o modo recursivo

12. Se queremos ver tóda-las queries que fai o servidor de DNS, qué opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados

- Ao estar traballando co dig podo emprepregar a opcion +tracer para ver las consultas que se fan en cada nivel

dig +tracer www.timesonline.co.uk

- co comando anterior poderemos ver os pasos que segue o servidor para resolver o dominio

IP: 205.251.193.192

14. Podes obter os rexistros AAAA de www.facebook.com? a qué corresponden?

- Podo obter os rexistros AAAA de www.facebook.com co seguinte comando:

dig AAAA www.facebook.com

2a03:2880:f104:83:face:b00c:0:25de

- A direccion ip anterior que pode verse na answer question e o servidor de facebook que é accesible a traves de ipv6.
