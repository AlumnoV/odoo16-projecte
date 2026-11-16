# odoo16-projecte
## 1. El nostre projecte i el problema de duplicitat
En el nostre projecte anem a gestionar el **préstec de material informàtic de l'institut** (portàtils, projectors, càmeres i kits de robòtica). 

El problema principal que volem resoldre és que ara mateix les dades s'apunten en diversos fulls d'Excel i en paper segons el departament, sense estar connectats entre si. Per això utilitzem **Odoo Community 16**, que ens permet tindre tots els contactes, el material d'inventari i els préstecs en una única base de dades i desenvolupar el nostre mòdul en les següents entregues.

## 2. Abans de començar (E1)

### Diferència entre aplicació, servidor i base de dades
* **Aplicació (Odoo 16):** És el programa amb la interfície web i les funcions (Vendes, Contactes, Inventari) que utilitza l'usuari des del navegador. Està fet en Python.
* **Servidor (Ubuntu Server / procés d'Odoo):** És el servei que està en marxa dins de la màquina virtual escoltant peticions al port `8069` i connectant l'aplicació amb les dades.
* **Base de dades (PostgreSQL):** És on es guarden realment totes les taules i dades (contactes, productes, pressupostos) al disc dur a través del port `5432`, perquè no es perden en apagar la màquina.

### Exemple de duplicitat si guardem la mateixa adreça en tres llocs
Imaginem que una alumna o sòcia, **Marta Soler**, té la seua adreça guardada en tres llocs diferents:
1. A l'Excel de **Secretaria** quan es matricula.
2. A la llista del **Departament d'Informàtica** quan demana un portàtil en préstec.
3. Al full d'**Administració** per cobrar-li la fiança del material.

Si Marta es muda de pis i només avisa a Secretaria, els altres dos llocs tindran l'adreça vella. Quan Informàtica li envie un avís per retornar el portàtil o Administració li faça el rebut, les dades no coincidiran i l'avís arribarà a l'adreça incorrecta. Amb Odoo, la fitxa de Marta es crea una sola vegada en *Contactes* i qualsevol pressupost o préstec agafa l'adreça d'ahí.
