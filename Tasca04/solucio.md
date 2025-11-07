# Servei LDAP

## 1. Introducció

Innovatech està experimentant un creixement accelerat que ha provocat problemes en la gestió d’usuaris i accessos. Cada servei intern utilitza sistemes d’autenticació separats, cosa que genera ineficiència, riscos de seguretat i dificultats d’escalabilitat.

Per solucionar-ho, s’ha decidit implementar una autenticació centralitzada amb OpenLDAP, una eina de codi obert compatible amb GNU/Linux. La tasca consisteix en:

-Instal·lar i configurar un servidor OpenLDAP.

-Definir la jerarquia d’unitats organitzatives.

-Crear usuaris i grups.

-Integrar un equip client per autenticar-se mitjançant el directori LDAP.

Aquesta solució millorarà la gestió, la seguretat i permetrà escalar la infraestructura de manera eficient.

---

## 2. Guia

Primer de tot configurarem els adaptadors de xarxa desde el VirtualBox, el primer adaptador ha d’estar en Xarxa NAT i el segon ha d’estar en només-amfitrió.

![Captura1](/Tasca04/img/captura1.png)
![Captura2](/Tasca04/img/captura2.png)

I en quant a hardware jo li he posat 4 GB de RAM i 2 processadors.

![Captura3](/Tasca04/img/captura3.png)

Ara farem unes configuracions inicials, un cop hem fet la instal·lació del nostre server, li canviarem el nom i el domin. Per fer-ho entrarem al arxiu /etc/hosts i el canviarem de la següent manera:

![Captura4](/Tasca04/img/captura4.png)

Per comprovar que el tenim ben canviat farem les següents comandes:

![Captura5](/Tasca04/img/captura5.png)

Seguidament, després de canviar nom i domini treballarem a partir de SSH, per tant hem de donar-li ip al segon adaptador de la següent manera:

Primer entrarem a aquest arxiu: /etc/netplan/00-installer-config.yaml (amb sudo nano).

Un cop dins l’arxiu l’editarem de la següent manera perquè ens dongui ip.

![Captura6](/Tasca04/img/captura6.png)

Un cop editat, el guardarem i executarem la comanda **sudo netplan apply**, tot seguit farem **ip a** i mirarem que tinguem IP en el segon adaptador.

![Captura7](/Tasca04/img/captura7.png)

Per continuar amb el SSH, obrirem el nostre terminal de Windows i escriurem la següent comanda: **ssh (el nom d’usuari que tinguis)@(la ip que tinguis), en el meu cas, ssh usuari@192.168.56.101** i fet això ja podriem utilitzar ssh i fer servir el servidor remotament desde el nostre equip. En cas de que no hagueu pogut o no us hagi deixat, reviseu que teniu ssh instal·lat al vostre servidor.

### **3.1 Instal·lació i Configuració Base d'OpenLDAP**

Seguirem amb la instal·lació del servei OpenLDAP, per instal·lar-ho utilitzarem aquesta comanda:

![Captura8](/Tasca04/img/captura8.png)

De contrasenya li podeu posar la que vulgueu, jo he posat usuari i així no se’m oblida.

Un cop fet, comprovarem que el servei està en funcionament.

![Captura9](/Tasca04/img/captura9.png)

I també comprovarem que el directori s’ha creat amb el nom que voliem:

![Captura10](/Tasca04/img/captura10.png)

En cas de que el nom del directori no és el que volem, ens tocarà reconfigurar el servei amb: sudo dpkg-reconfigure slapd i posarem la següent configuració:

![Captura11](/Tasca04/img/captura11.png)

Li diem que no,

![Captura12](/Tasca04/img/captura12.png)

Aqui posem el nom corresponent al directori que volem crear.

![Captura13](/Tasca04/img/captura13.png)

Seguim amb el nom de la organització.

![Captura14](/Tasca04/img/captura14.png)

Li poses la contrasenya del administrador.

![Captura15](/Tasca04/img/captura15.png)

Aqui li donem a Yes.

![Captura16](/Tasca04/img/captura16.png)

I aquí li tornem a donar Yes, i fet això ja estaria.

![Captura17](/Tasca04/img/captura17.png)

---

Ara el que farem és crear dues OUs: **users i groups** mitjançant un fitxer **.ldif**.

Per crear la de les dues OUs, primer de tot crearem l’arxiu OU_users.ldif i l’editarem de la següent manera:

![Captura18](/Tasca04/img/captura18.png)

Un cop fet, utilitzarem la comanda **ldapadd** per crear les entrades al directori LDAP.

![Captura19](/Tasca04/img/captura19.png)

I seguidament farem una consulta amb **ldapsearch** que es mostrin les OUs.

![Captura20](/Tasca04/img/captura20.png)

---

### **3.2 Gestió i Administració (LAM)**
