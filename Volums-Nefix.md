# Gestió de volums lògics

### Què són els LVM?

LVM són les sigles de 'Logical Volume Manager', que vol dir 'Gestor de Volums Lògics'. Els Volums Lògics són una espèice de 'discs durs virtuals'. Un dels seus prinicpals avantages és què els pots redimensonar 'en calent'.

### Què volen dir les sigles PV, VG, LV? Posa exemples de les comandes

* PV:  
  + PV són les sigles de 'Physical Volume', que vol dir 'Volum físic'. És una forma d'identificar els discs durs els quals podem utilitzar per crear-hi VG's.
  + Comandes principals:
      * `pvcreate /dev/<dispositiu>` --> Afegeix un dispositiu com a 'PV'
      * `pvs` --> Llista tots els dispositius 'PV'

* VG:
  + VG són les sigles de 'Volume Group', que vol dir 'Grup de Volums'. És una espècie de 'disc dur virtual' que pot estar a més d'un PV alhora. Dins d'aquest VG hi podem crear LV's.
  + Comandes principals:
      * `vgcreate <nom> /dev/<PV>` --> Crea un VG amb el 100% d'espai d'un PV
      * `vgs` --> Llista tots els VG's
      * `vgextend <VG> /dev/<dispositiu>` --> Afegeix un disc a dins del VG
      * `vgrename /dev/<VG> <nom nou>` --> Canvia el nom d'un VG. Continua tenint el nom anterior a tots els LV fins que aquests no es desmuntin.

* LV:
  + LV són les sigles de 'Logical Volume', que vol dir 'Volum Lògic'. És una espècie de 'partició' dins d'un VG.
  + Comandes principals:
      * `lvcreate -L <tamany> -n <nom> <VG>` --> Crea un LV amb un tamany específic dins d'un VG específic
      * `lvcreate -l 100%FREE -n <nom> <VG>` --> Crea un LV amb el 100% del tamany lliure del VG
      * `lvs` --> Llista tots els LV's
      * `lvextend -L +<tamany> /dev/<VG>/<LV>` --> Afegeix X tamany a un LV específic. Perquè els canvis siguin 'visibles', hem de redimensonar, també, el sistema de fitxers (mirar 'Comandes FS') **un cop haguem redimensionat** el LV.
      * `lvreduce -L -<tamany> /dev/<VG>/<LV>` --> Redueix X tamany a un LV específic. Perquè els canvis siguin 'visibles', hem de redimensonar, també, el sistema de fitxers (mirar 'Comandes FS') **ABANS** de redimensionar el LV.
      * `lvrename /dev/<VG>/<LV> <nom nou>` --> Canvia el nom d'un LV. Continua tenint el nom anteriorfins no es desmunti.

* Comandes FS:
  + EXT3/EXT4:
      * `resize2fs /dev/<dispositiu>` --> Ajusta la mida del FS al total de la partició. Si s'ha fet petit, s'ha de remuntar el dispositiu
      * `resize2fs /dev/<dispositiu> <tamany>` --> Ajusta la mida del FS al tamany especificat. Si s'ha fet petit, s'ha de remuntar el dispositiu
  + XFS:
      * `xfs_growfs /dev/<dispositiu>` --> Fa gran la mida del FS al total de la partició.

### Entorn de Pràctiques

Per aquesta pràctica, utilitzaré una 'live' del Fedora 24 amb l'escriptori GNOME com a 'guest' i un Fedora 24 com a 'host', utilitzant el 'virt-manager' com a virtualitzador. La màquina virtual tindrà 3 discs de 200MB cada un de tipus 'Virt-IO'.

![Entorn Pràctiques](entorn.png)


### Pràctica 1: Creació d'un volum lògic a partir d'un dels tres discs durs.

NOTA: Ha de tenir el 100% de la capacitat d'aquest, dir-se 'dades' i estar dins d'un grup anomenat 'practica1'  

Un cop hem arrencat la màquina virtual, ens dirigim a la configuració i canviem la disposició del teclat a la de català. Un cop fet això, ja podem utilitzar les comandes per crear, modificar o destruïr PV's, VG's i LV's. Per començar executarem:

`# pvcreate /dev/vda` --> Creem un PV al dispositiu /dev/vda (el primer disc virtual)  
`# pvs` --> Per asseguran-nos de que el PV s'ha creat correctament  
`# vgcreate practica1 /dev/vda` --> Creem un VG al PV /dev/vda amb el nom 'practica1'  
`# vgs` --> Per asseguran-nos de que el VG s'ha creat correctament  
`# lvcreate -l 100%FREE -n dades practica1` --> Creem un LV al VG /dev/pracitca1 amb el nom 'dades'  
`# lvs` --> Per asseguran-nos de que el LV s'ha crear correctament  

![Pràctica 1](practica1.png)

### Pràctica 2: Creació d'un sistema de fitxers xfs al volum lògic que acabem de crear.

NOTA: Hem de muntar-lo a '/mnt' i crear-hi una imatge en blanc de 180MB.

Un cop ja hem creat el LV, hem de crear-hi un sistema de fitxers per poder utilitzar-lo. Per ferho executarem:

`# mkfs.xfs /dev/pracitca1/dades` --> Crea un sistema de fitxers XFS al LV dades.  
`# mount /dev/pracitca1/dades /mnt` --> Muntem el LV a /mnt  
`# dd if=/dev/zero of=/mnt/imatge1.img bs=1M count=180` --> Crea una imatge plena de zeros de 180MB amb el nom de 'imatge1.img'  

![Pràctica 2](practica2.png)

### Pràctica 3: Creació d'un RAID 1 amb els dos discs restants.

Per crear un RAID 1, utilitzarem els dos discs restants (vdb i vdc). El crearem amb les següents comandes:

`# mdadm --create --verbose /dev/md0 --level=1 --raid-devices=2 /dev/vdb /dev/vdc` --> Creem un RAID 1 amb els dispositius /dev/vda i /dev/vdb. Serà el dispositiu /dev/md0  
`# cat /proc/mdstat` --> Comprovem que la RAID s'hagi creat correctament.  

![Pràctica 3](practica3.png)

### Pràctica 4: Ampliació del volum lògic 'dades' amb el RAID

Per ampliar el LV dades, haurem d'augmentar primer el VG i després aquest. Ho farem amb les següents comandes:
`# vgextend pracitca1 /dev/md0` --> Afegim el dispositiu RAID al VG 'pracitca1'.  
`# vgs` --> Per asseguran-nos de que el VG s'ha extès correctament  
`# lvextend -l +100%FREE /dev/pracitca1/dades` --> Afegim tot l'espai disponible del VG pracitca1 al LV dades  
`# lvs` --> Per asseguran-nos de que el LV s'ha extès correctament  

![Pràctica 4](practica4.png)

### Pràctica 5: Ampliació del sistema de fitxers xfs al tamany actual del volum lògic dades

NOTA: L'hem d'ampliar sense desmuntar-lo i crear-hi una imange en blanc nova de 180MB.  
`# xfs_growfs /dev/pracitca1/dades` --> Ampliem el FS al màxim. No cal desmuntar-lo  
`# dd if=/dev/zero of=/mnt/imatge2.img bs=1M count=180` --> Crea una imatge plena de zeros de 180MB amb el nom de 'imatge2.img'  

![Pràctica 5](practica5.png)
