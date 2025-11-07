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

### **2.1 Instal·lació i Configuració Base d'OpenLDAP**

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

### **2.2 Gestió i Administració (LAM)**

Primer de tot farem la instal·lació del LDAP Account Manager:

![Captura21](/Tasca04/img/captura21.png)

Un cop ho tinguem instal·lat, anirem al nostre navegador i posarem http://192.168.56.101/lam (la IP poses la que tinguis tu, aquest és el meu cas), li donarem a dalt a la dreta on posa **LAM configuration** i després a **Edit server profiles** i la contrasenya és lam i un cop fet tot això ja estarem dins.

![Captura22](/Tasca04/img/captura22.png)

Ara el que farem és establir la configuració per defecte per què els usuaris nous s’ubiquin a l’OU users i els grups nous a l’OU groups.

Per fer-ho anairam a l’apartat de tipos de cuentas i l’editarem de la següent manera:

![Captura23](/Tasca04/img/captura23.png)

Una vegada ja ho tinguem tot canviat i bé, crearem dos grups de seguretat al directori: **tech i manager**.

Per fer-ho anirem a l’apartat de **Cuentas** i després a **Grupos**.

![Captura24](/Tasca04/img/captura24.png)

Seguidament li donarem a Nuevo Grupo

![Captura25](/Tasca04/img/captura25.png)

I el creem amb el seu corresponent nom:

![Captura26](/Tasca04/img/captura26.png)

Ara crearem un usuari per cada un d’aquests grups: **tech01 i manager01**.

Per fer-ho anirem a **Cuentas** i després a **Usuarios**.

![Captura27](/Tasca04/img/captura27.png)

I els crearem seguint els criteris que ens demanen.

![Captura28](/Tasca04/img/captura28.png)

---

### **3. Integració de Client (Client Ubuntu Desktop)**

Per fer aquesta part necessitarem instalar un client en una màquina amb Zorin OS amb dos adaptadors de xarxa, el primer en Xarxa NAT i el segon en només amfitrió.

![Captura29](/Tasca04/img/captura29.png)
![Captura30](/Tasca04/img/captura30.png)

Un cop dins la màquina, el primer que farem serà editar l’arxiu d'hosts, jo ho faré a partir de ssh.

![Captura31](/Tasca04/img/captura31.png)

L’editem d’aquesta manera i tot seguit farem una instantánea de la máquina.

![Captura32](/Tasca04/img/captura32.png)

Comprovarem que els noms estiguin bé:

![Captura33](/Tasca04/img/captura33.png)

Ara el que farem serà comprovar la connectivitat amb el servidor fent una consulta ldapsearch des del client.

Per tant, instal·larem LDAP en el client:

![Captura34](/Tasca04/img/captura34.png)

I seguidament posarem aquesta comanda: **ldapsearch -x -H ldap://server.innovatech03.test:389 -b "dc=innovatech03,dc=test"**

![Captura35](/Tasca04/img/captura35.png)

Un cop comprovada la connectivitat, instal·larem els mòduls necessaris per permetre l'autenticació amb LDAP.

Utilitzarem la comanda: **apt install libnss-ldap libpam-ldap ldap-utils nscd -y**, un cop executada, sens obrirà un menu, posarem el següent:

![Captura36](/Tasca04/img/captura36.png)

Li donam a aceptar,

![Captura37](/Tasca04/img/captura37.png)

Aquesta la posem així i li tornem a donar a aceptar,

![Captura38](/Tasca04/img/captura38.png)

Aquí posarem el 3,

![Captura39](/Tasca04/img/captura39.png)

Aquí posem Sí,

![Captura40](/Tasca04/img/captura40.png)

Aquí posem No,

![Captura41](/Tasca04/img/captura41.png)

Això ho editem d’aquesta forma,

![Captura42](/Tasca04/img/captura42.png)

I aquí posarem una contrasenya.

Fet això, ara modificarem els arxius de configuració del client, per tant, entrarem al arxiu **nsswitch.conf** i l’editarem de la següent forma per indicar que s’usarà ldap per usuaris i grups.

![Captura43](/Tasca04/img/captura43.png)

Seguidament anirem a l’arxiu **/etc/pam.d/common-password** i eliminem el **use_authtok**:

![Captura44](/Tasca04/img/captura44.png)
