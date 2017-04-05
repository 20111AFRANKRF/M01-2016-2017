# SISTEMES RAID

1. Resum de sistemes RAID fent servir una taula com la vista a classe.

| RAID | MIN. DISCS | MAX. DISCS ERROR | CAPACITAT | READ | WRITE |
| :--- | :--------: | :--------------: | :--------: | :--: | :---: |
|   0  |     2      |         0        |     100%   |  E   |   E   |
|   1  |     2      |         1        |      50%   |  VG  |   G   |
|   5  |     3      |         1        |   67-94%   |  VG  |   G   |
|   6  |     4      |         2        |   50-88%   |  G   |   G   |
|  10  |     4      |      1/MIRROR    |      50%   |  VG  |   G   |

>Llegenda:
 
   * **E** --> Excellent
   * **VG** --> Very Good
   * **G** --> Good

2. Descripció de la metodologia utilitzada a classe per a fer proves amb màquines virtuals.

   + Primer de tot creem una maquina virtual amb un S.O
   + A continuació afegim dos discs durs (tipus *VirtIO* o *IDE* )
   + Desde linia de comandes creem un *'RAID'* 
   + Una vegada creada fem un sistema de fitxer y la muntem a una carpeta
   + Una vegada fet tot això comprobem que el RAID s'ha creat correctament amb **lsblk**
   + Per veure si funciona bé la extracció de discs en calent eliminem un dels disc durs 
   + Mirem l'arxiu amb la informacio dels *RAIDS* per veure que detecta que hi ha un error en un dels discs
   + Insertem altre disc dur i l'afegim al RAID desde linia de comandes
   + Tornem a mirar l'arxiu amb l'informació dels RAID y timdria que estar perfectament.
     
3. Comandes i descripció de les mateixes per tal de crear un sistema RAID1
   
   > ***mdadm --create md0 --level=1 --raid-devices=2 </dev/vda> </dev/vdb>***
   + ***--create:*** Crea el RAID amb el nom que li possis (normalment md0, md1, etc.)
   + ***--level:*** Tipus de RAID que vols crear
   + ***--raid-devices:*** Numero de disc durs que li poses al RAID
   > ***mkfs.ext4 /dev/md0***
   + Crea un sistemes de fitxers ext4 per el RAID md0
   > ***mount /dev/md0 /mnt*** 
   + monta el RAID md0 al directori 'mnt'

4. Comandes i descripció de les mateixes per tal de crear un sistema RAID5

   > ***mdadm --create md1 --level=5 --raid-devices=3 </dev/vda> </dev/vdb> </dev/vdc>***
   + ***--create:*** Crea el RAID amb el nom que li possis (normalment md0, md1, etc.)
   + ***--level:*** Tipus de RAID que vols crear
   + ***--raid-devices:*** Numero de disc durs que li poses al RAID
   > ***mkfs.ext4 /dev/md1***
   + Crea un sistemes de fitxers ext4 per el RAID md1
   > ***mount /dev/md1 /mnt*** 
   + monta el RAID md1 al directori 'mnt'
   
5. Comandes i descripció de les mateixes per tal de crear un sistema RAID6

   > ***mdadm --create md2 --level=6 --raid-devices=4 </dev/vda> </dev/vdb> </dev/vdc> </dev/vdd>***
   + ***--create:*** Crea el RAID amb el nom que li possis (normalment md0, md1, etc.)
   + ***--level:*** Tipus de RAID que vols crear
   + ***--raid-devices:*** Numero de disc durs que li poses al RAID
   > ***mkfs.ext4 /dev/md2***
   + Crea un sistemes de fitxers ext4 per el RAID md2
   > ***mount /dev/md2 /mnt*** 
   + monta el RAID md2 al directori 'mnt'

6. Comandes i descripció de les mateixes per tal de crear un sistema RAID10

   + Per crear un RAID 10 necessitem tenir creat abans dos RAID 1
   > ***mdadm --create md3 --level=10 --raid-devices=2 </dev/md5> </dev/md6>***
   + ***--create:*** Crea el RAID amb el nom que li possis (normalment md0, md1, etc.)
   + ***--level:*** Tipus de RAID que vols crear
   + ***--raid-devices:*** Numero de disc durs que li poses al RAID
   > ***mkfs.ext4 /dev/md3***
   + Crea un sistemes de fitxers ext4 per el RAID md3
   > ***mount /dev/md3 /mnt*** 
   + monta el RAID md3 al directori 'mnt'
