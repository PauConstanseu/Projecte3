# **Fase 1: Anàlisi i justificació**

---

## 1. **Introducció i justificació**

L’incident de seguretat a EverPia ha evidenciat una vulnerabilitat crítica: l’ús de contrasenyes febles o reutilitzades. Aquestes pràctiques exposen l’empresa a:

* **Atacs de diccionari**: proves amb paraules comunes.  
* **Credential stuffing**: ús de credencials filtrades en altres serveis.  
* **Brute force**: proves sistemàtiques fins a trobar la contrasenya.

Un gestor de contrasenyes permet mitigar aquests riscos generant contrasenyes fortes, úniques i emmagatzemant-les de forma segura. També facilita l’accés des de diversos dispositius i pot integrar-se amb sistemes d’autenticació multifactor (MFA).

---

## 2. **Comparativa tècnic**

| Característica | Bitwarden (online) | KeePassX (offline) |
| :---- | :---- | :---- |
| Model de seguretat | Xifratge end-to-end (AES-256), zero-knowledge | Xifratge local (AES-256), arxiu KDBX |
| Emmagatzematge | Núvol (amb opció d’autoallotjament) | Local (fitxer KDBX) |
| Sincronització | Sí, automàtica entre dispositius | No nativa, cal sincronització manual |
| Accés multiplataforma | Web, mòbil, escriptori | Escriptori, portabilitat via USB |
| Model freemium | Gratuït amb opcions premium | Totalment gratuït |
| Open source | Sí | Sí |
| Facilitat d’ús | Alta, intuïtiu | Mitjana, més tècnic |
| Portabilitat | Alta (núvol) | Alta (fitxer portàtil) |

---

## 3. **Avantatges i inconvenients**

#### **Bitwarden (Online)** {#bitwarden-(online)}

**Avantatges:**

* Sincronització automàtica.  
* Interfície intuïtiva.  
* Opció d’autoallotjament per a control intern.

**Inconvenients:**

* Dependència del núvol (si no s’autoallotja).  
* Potencials riscos si el servei és compromès (tot i el xifratge).

#### **KeePassXC (Offline)** {#keepassxc-(offline)}

**Avantatges:**

* Control total de les dades.  
* No depèn de connexió ni de tercers.  
* Ideal per a entorns restringits.

**Inconvenients:**

* No sincronitza automàticament.  
* Més complex per a usuaris no tècnics.  
* Risc de pèrdua si no es fa còpia de seguretat.  
  ---

## 4. **Recomanació final**

Es recomana Bitwarden com a gestor principal per al personal tècnic d’EverPia per la seva seguretat, facilitat d’ús i capacitat de sincronització. L’opció d’autoallotjament permet mantenir el control intern de les dades. KeePassXC pot ser una alternativa complementària en entorns on no es permet l’ús del núvol.
