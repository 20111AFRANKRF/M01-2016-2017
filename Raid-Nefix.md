# RAID

### 1- Resum de els tipus de RAID:  

|      Tipus      | Mín Discs |   Fallats  |   Capacitat   |   Read    |   Write   |  
| -------------- -| --------- | ---------- | ------------- | --------- | --------- |  
|     RAID 0      |     2     |      0     |     100%      | Exel·lent | Exel·lent |  
|     RAID 1      |  2 (MAX)  |      1     |      50%      | Molt Bona |    Bona   |
|     RAID 5      |     3     |      1     |    67%-94%    | Molt Bona |    Bona   |
|     RAID 6      |     4     |      2     |    50%-88%    |    Bona   |    Bona   |
| RAID 10 (1 + 0) |     4     | 1 / mirror |      50%      | Molt Bona |    Bona   |
| RAID 50 (5 + 0) |     6     | 1 / mirror |    67%-94%    | Exel·lent | Molt Bona |
| RAID 60 (6 + 0) |     8     | 2 / mirror |    50%-88%    | Molt Bona |    Bona   |


### 2- Descripció de la metodologia:  
Per a fer aquesta pràctica, he utilitzat un Fedora 24 com a host, utilitzant el "virt-manager" com a gestor de màquines virutals. Com a guest, utilitzarem el Debian 8.7 Cinnamon. A l'hora d'afegir i esborrar discs, s'utilitza l'eina GUI del "virt-manager".

### 3- RAID 1:
`mdadm --create --verbose /dev/md<número del dispositiu> --level=1 --raid-devices=2 /dev/<dispositiu 1> /dev/<dispositiu 2>`

### 4- RAID 5:
`mdadm --create --verbose /dev/md0 --level=5 --raid-devices=3 /dev/<dispositiu 1> /dev/<dispositiu 2> /dev/<dispositiu 3>`

### 5- RAID 6:
`mdadm --create --verbose /dev/md0 --level=6 --raid-devices=4 /dev/<dispositiu 1> /dev/<dispositiu 2> /dev/<dispositiu 3> /dev/<dispositiu 4>`

### 6- RAID 10:  
Per crear un RAID 10, primer hem de crear els dos RAID 1 i després ajuntar-los a un RAID 0:

#### RAID 1 1:
`mdadm --create --verbose /dev/md1 --level=1 --raid-devices=2 /dev/<dispositiu 1> /dev/<dispositiu 2>`

#### RAID 1 2:
`mdadm --create --verbose /dev/md2 --level=1 --raid-devices=2 /dev/<dispositiu 1> /dev/<dispositiu 2>`

#### RAID 0:
`mdadm --create --verbose /dev/md0 --level=0 --raid-devices=2 /dev/md1 /dev/md2`
