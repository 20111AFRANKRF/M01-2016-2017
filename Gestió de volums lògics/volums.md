# GESTIÓ DE VOLUMS LÒGICS  

## QUè SÓN?  

 * Els volums lògics son unitats de disc virtualitzades quie permeten fer més funcions que les clàssiques particions  

## DESCRIPCIÓ:  

| **PV** | Physical Volume ~ Identificació de discs |         
| **VG** | Volume Group ~ Discs Virtuals |  
| **LV** | Logical Volume ~ Particións |  

													
		                                            
		                                            
## COMANDES:   

**pvcreate** --> S'utilitza pre crear PV  
**vgcreate nombre-vg ruta-pv1 ruta-pv2 etc.** --> S'utilitza per crear VG  
**lvcreate -l +100%FREE> -n nombre-lv** --> S'utilitza per crear un LV amb tot l'espai lliure  
**lvcreate -L tamany -n nombre-lv ruta-vg-donde-lo-quieres-crear** --> S'utilitza per crear un LV amb el tamany que tu vulguis   
**pvs** --> llista els punts de muntatge   
**vgextend** --> Augmenta la mida del VG  
**lvextend** --> Augmenta la mida del LV  

## ENTORN DE PRACTIQUES:  

> Explicar com farem la pràctica detalladament (màquina virtual i afegir tres discs de 200M)  

* Pràctica 1: Creació d'un volum lògic a partir d'un dels tres discs durs (vda per exemple). Aquest volum lògic ha de ser del total de capacitat del disc. El volum de grup s'ha de dir practica1 i el volum lògic dades.  

!(PRACTICA1.png)  

Primer de tot afegim 3 discs ***VirtIO***  
Despres identifiquem un dels discs con **PV**  
Seguidament creem el **VG** practica1     
y per finalitzar creem el **LV**     
al final de tot veiem que tot a quedat bé mitjaçant *pvs* y *lvs*  

* Pràctica 2: Creació d'un sistema de fitxers xfs al volum lògic creat i muntatge a /mnt. També s'ha de crear un fitxer amb dd de 180MB.

* Pràctica 3: Creació d'un RAID 1 als dos discos sobrants (vdb i vdc per exemple).

* Pràctica 4: Ampliació del volum lògic de dades al raid.

* Pràctica 5: Ampliació del sistema de fitxers xfs al tamany actual del volum lògic dades (s'ha de poder fer sense desmuntar-lo de /mnt ja que és xfs). Una vegada creat crearem un nou fitxer de 180M.
