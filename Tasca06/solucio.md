# **Fonaments del servei DNS** 

## **Fase teòrica**

### **1\. Jerarquia i Estructura del DNS** 

* **Estructura en arbre**:   
* **Root (.)**: punt de partida de totes les consultes DNS.   
* **TLDs (Top-Level Domains)**: .com, .org, .net, etc.   
* **Domini de segon nivell**: digicore.com   
* **Subdominis**: app.digicore.com 

 

### **2\. Procés de Resolució** 

* **Consulta iterativa**:   
* El client pregunta a cada servidor fins trobar la resposta.   
* Exemple: resolució pas a pas fins arribar al servidor autoritatiu.   
* **Consulta recursiva**:   
* El servidor DNS fa tot el procés per al client.   
* Exemple: el servidor recursiu contacta amb root, TLD i autoritatius.   
* **Servidor d’arrel (Root Server)**:   
* Coneix els servidors TLD.   
* **Servidor autoritatiu**:   
* Conté la resposta final per a un domini específic. 

 

### **3\. Tipus de Zones DNS** 

* **Zona directa**:   
* Traducció de noms a IPs.   
* **Zona inversa**:   
* Traducció d’IPs a noms.   
* **Zona primària**:   
* Conté la còpia principal de la base de dades DNS.   
* **Zona secundària**:   
* Còpia de seguretat sincronitzada amb la primària. 

 

### **4\. Tipus de Registres Clau** 

* **A**: assigna una IP a un nom.   
* **CNAME**: àlies d’un altre nom.   
* **MX**: indica el servidor de correu.   
* **NS**: defineix els servidors autoritatius.   
* **SRV**: especifica serveis amb port i protocol. 

 

### **5\. Conceptes Essencials** 

* **Resposta autoritativa**:   
* Prové del servidor que gestiona el domini.   
* Es pot identificar amb eines com dig.   
* **TTL (Time To Live)**:   
* Temps que una resposta DNS es manté en memòria cau.   
* Impacta en la propagació i rendiment.   
* **SOA (Start of Authority)**:   
* Conté informació crítica: correu del responsable, número de sèrie, TTL, etc.   
* **Reenviadors**:   
* **Incondicionals**: reenviament de totes les consultes.   
* **Condicionals**: només per a dominis específics. 

 

### **6\. Resolució Local i mDNS** 

* **Resolució local**:   
* Fitxer hosts, memòria cau del sistema.   
* **mDNS (Multicast DNS)**:   
* Resolució sense servidor, útil en xarxes locals.   
* Exemple: dispositius IoT o impressora en xarxa. 

 

### **7\. Recomanacions Pràctiques** 

* Utilitzar eines com nslookup, dig, host per diagnosticar.   
* Revisar TTLs, reenviadors i registres autoritatius.   
* Monitoritzar la latència en resolució de noms. 

 

### **Activitat Final** 

Preparació d’un vídeo formatiu (10-15 min) que expliqui aquests conceptes amb exemples visuals i clars. 

