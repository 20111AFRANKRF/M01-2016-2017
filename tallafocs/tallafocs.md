# Tallafocs
**Què es un sistema tallafocs? Quina és la seva finalitat?**  
  Es una parte de un sistema o una red que tiene como finalidad impedir el  acceso de extraños no autorizados y al mismo tiempo permitir el acceso a los autorizados    

**Quines generacions de tallafocs hi ha hagut i què millorava cadascun?**  
  Ha habido tres generaciones:    
  * PRIMERA GENERACION - FILTRADO DE PAQUETES  
  * SEGUNDA GENERACION - CORTAFUEGOS DE ESTADO
  * TERCERA GENERACION - CORTAFUEGOS DE APLICACION  

**Quines capes té el model OSI?**  
  El modelo OSI tiene siete capas:
  * APLICACION
  * PRESENTACION
  * SESION
  * TRANSPORTE
  * RED
  * ENLACE DE DATOS
  * FISICA  

**Quines capes té el model TCP/IP? En aquest cas feu una breu descripció de les funcionalitats de cada capa.**  
  El modelo TCP/IP tiene cinco capas:
  * APLICACION
  * TRANSPORTE
  * RED
  * ENLACE DE DATOS
  * FISICA  

**A quina capa/capes sol treballar tradicionalment un tallafocs?**  
  Suele aplicarse entre las capas desde la de red hasta la de aplicaciones
# Tallafocs Linux  

**Busqueu quins són els tradicionals sistemes de tallafocs incorporats en linux i anomeneu-los**

* IPTABLES: Es un poderoso firewall integrado en el kernel de Linux y que forma parte del proyecto netfilter. Iptables puede ser configurado directamente, como también por medio de un frontend o una GUI. iptables es usado por IPv4, en tanto que ip6tables es usado para IPv6    

* IPCHAIN: Es un cortafuegos libre para Linux. Es el código reescrito del código fuente del cortafuego IPv4 anterior de Linux. En Linux 2.2, ipchains es requerido para administrar los filtros de paquetes IP. ipchains fue escrito porque el cortafuegos IPv4 anterior utilizado en Linux 2.0 no funcionaba con fragmentos IP y no permitía que se especifiquen otros protocolos que no sean TCP, UDP o ICMP.

**Quins dels anteriors tallafocs estan instal.lats al fedora de classe? Com ho comproveu?**
En clase tenemos instalado IPTABLES (se puede comprobar mediante linia de comandos i/o porque a partir de la version 2.4 del S.O. ya viene instalado de forma predeterminada en el kernel)

**Algun dels anteriors tallafocs es troba activat?**  
NO  

**Instal.leu el servidor web httpd o nginx i activeu-ne el servei (dnf installl ...  ; systemctl ....). Indiqueu les comandes i comproveu que des d'una altra màquina podeu accedir via web a la vostra IP (digueu-li a un company). Hauria de sortir la plana per defecte.**  
(FET)  
**Activeu el servei firewalld. Indiqueu com ho feu.**   
systemctl start firewalld.service  
**Comproveu si ara es pot seguir accedint.**  
No puede acceder  

# Win7
**Porta aquest SO algun tallafocs incorporat?**  
Si, el windows firewall  
**Arrenqueu una màquina win7 a isard.escoladeltreball.org**  
(FET)  
**Indiqueu com arribar al tallafocs (passos i pantalles)**  
1. Abrir barra de inicio  
2. Buscar firewall de windows
3. Abrir el programa    

**Es troba activat en aquest windows?**   
 Si, se encuentra activado  
**Busqueu un altre tallafocs per windows. Indiqueu la plana web i les prestacions que ens dona. Intenteu que NOMÉS sigui tallafocs**  
Zonealarm - http://www.zonealarm.com/es/software/free-firewall/
