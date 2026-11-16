# E1 · Coneix Odoo Community i verifica el seu entorn

## Pas 1. Odoo Community i comparació amb altres ERP

### 1.1. Tres sistemes ERP/CRM i com ajuden al projecte
1. **Odoo Community 16:** ERP de codi obert modular. Ens serveix per portar en un mateix lloc els contactes del centre, l'inventari d'equips i els pressupostos/reserves, a més de permetre'ns crear el nostre propi mòdul en Python.
   * Web consultada: https://www.odoo.com/documentation/16.0/ (Consulta: novembre 2026).
2. **Dolibarr ERP & CRM:** Sistema web lliure enfocat a xicotetes empreses i associacions. Per al nostre projecte serviria per controlar altes de socis/usuaris, quotes i factures senzilles.
   * Web consultada: https://www.dolibarr.org/ (Consulta: novembre 2026).
3. **ERPNext:** ERP de codi obert basat en Python (Frappe). Al nostre projecte ens ajudaria a gestionar el manteniment dels equips prestats i el control d'estoc per ubicacions.
   * Web consultada: https://docs.erpnext.com/ (Consulta: novembre 2026).

### 1.2. Taula comparativa: Odoo Community 16 vs Dolibarr

| Característica | Odoo Community 16 | Dolibarr ERP/CRM |
| :--- | :--- | :--- |
| **Funcions** | Mòduls de Contactes, Vendes, Inventari, Facturació, Projectes i Web. Molt fàcil d'ampliar programant mòduls propis en Python i XML. | Gestió de clients/socis, pressupostos, factures i estoc bàsic. Més senzill però menys flexible per a desenvolupaments a mida. |
| **Llicència (codi, mòduls i servei)** | **Codi base:** LGPLv3 (lliure, permet modificar i afegir mòduls). **Mòduls de la comunitat (OCA):** LGPLv3 / AGPLv3. **Servei:** El programa és gratuït; si contractes un servidor al núvol o suport tècnic es paga a part. | **Codi i mòduls:** GPLv3 (programari lliure). **Servei:** Gratuït si l'instal·les al teu servidor; de pagament mensual si es contracta al núvol (DoliCloud). |
| **Desplegament** | Com a servei en Linux (`systemd`), amb contenidors Docker Compose o en un servidor al núvol (VPS). | En un servidor web clàssic amb Apache/Nginx i PHP (LAMP/WAMP) o amb Docker. |
| **Requisits** | Ubuntu Server 22.04/24.04 LTS, Python 3.10+, base de dades PostgreSQL, mínim 2-4 GB de RAM i 25 GB de disc. | Servidor web amb PHP 8+, base de dades MySQL/MariaDB o PostgreSQL, i almenys 1 GB de RAM. |

### 1.3. Justificació d'Odoo Community 16 i diferències amb Enterprise (U1)
* **Per què fem servir Odoo Community 16:** És l'ERP fixat per al curs i s'adapta al projecte perquè és gratuït, té llicència lliure LGPLv3 i tenim accés a tot el codi font per aprendre a desenvolupar el nostre mòdul en la següent entrega.
* **Diferències amb l'Odoo 19 Enterprise que vam provar en la U1:**
  * En la U1 vam usar **Odoo 19 Enterprise** al núvol educatiu (Scale-Up), que té llicència privativa de pagament, una pantalla principal amb totes les icones en quadrícula i mòduls exclusius com *Studio* o Comptabilitat completa.
  * Al laboratori d'U2 fem servir **Odoo 16 Community** instal·lat per nosaltres en local: el menú d'aplicacions és un desplegable dalt a l'esquerra, no té els mòduls de pagament d'Enterprise i nosaltres mateixos controlem el servidor Ubuntu i la base de dades PostgreSQL.

---

## Pas 2. Exploració guiada: Contacte, Producte i Pressupost

En l'entorn de proves hem creat les dades fictícies següents (captura a `/img/01_flujo_presupuesto.png`):
* **Contacte:** *Marta Soler - Associació El Pont*.
* **Producte:** *Préstec Projector + Pantalla* (Preu: `25,00 €`).
* **Pressupost (`S00001`):** Assignat a Marta Soler amb 1 línia de **2 unitats x 25,00 € = 50,00 €** (més 21% d'IVA = **60,50 €** en total).

**Què canvia quan polsem «Confirmar» al pressupost?**
El document deixa de ser un esborrany de pressupost i passa a ser una **Comanda de Venda** ferma. En eixe moment, Odoo habilita el botó per **Crear Factura** i, si tenim el mòdul d'Inventari activat, genera automàticament l'ordre d'entrega (albarà d'eixida del magatzem) per preparar el material per a Marta Soler.

---

## Pas 3. Fitxa de l'entorn i pregunta de Transferència

### 3.1. Versions de l'entorn de laboratori
* **Sistema operatiu:** **Ubuntu Server 24.04 LTS**. El fem servir perquè la versió Server no gasta memòria RAM en interfície gràfica i, en ser LTS (Long Term Support), té 5 anys de suport i estabilitat.
* **Base de dades:** **PostgreSQL** (versió 16 en instal·lació manual i 15 en Docker). És obligatori perquè Odoo només funciona amb PostgreSQL per guardar totes les taules.
* **Xarxa en VirtualBox:** Configurada en mode **NAT** (perquè en WifiEdu el mode pont no ens dona IP) amb redirecció dels ports `8069` (Odoo servei), `8070` (Odoo Docker), `8025` (MailHog) i `2222` (SSH).

### 3.2. Pregunta de Transferència: Obertura d'una segona seu amb teletreball
* **Què conservaríem:** Conservaríem **Odoo Community 16 amb Docker Compose** i una **única base de dades PostgreSQL comuna** per a totes dues seus, perquè així no es dupliquen els contactes ni l'inventari entre oficines.
* **Què canviaríem:** No podríem tindre l'Odoo dins d'una màquina virtual al nostre portàtil amb NAT. El passaríem a un **servidor al núvol (VPS) o servidor central de l'entitat** amb una IP fixa/domini, posant un proxy invers (com Nginx amb certificat segur HTTPS) o una VPN perquè els treballadors de la segona seu i els de casa puguen entrar des d'Internet de forma segura.
