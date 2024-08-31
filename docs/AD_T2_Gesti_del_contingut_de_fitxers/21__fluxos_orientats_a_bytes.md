# 2.1 - Fluxos orientats a bytes - Classes

L'arrel, la base de tota la jerarquia són **InputStream** i **OutputStream** ,
respectivament per a fluxos d'entrada i d'eixida. Comentarem els fluxos
d'entrada, i els d'eixida són totalment paral·lels.

La super-classe **InputStream** servirà per a fer l'entrada des de qualsevol
dispositiu: fitxer, array de bytes, una tuberia (per a dur dades des d'una
altra aplicació)... Totes les classes d'entrada heretaran d'ella, i serviran
per especificar exactament d'on (per exemple un fitxer: **FileInputStream**) o
per a donar alguna altra funcionalitat, com anirem veient a poc a poc.
D'aquesta manera, els mètodes que es defineixen s'hauran d'implementar per les
classes que hereten de la super-classe i assegura una uniformitat, siga quina
siga la font.

Fem una ullada ràpida a la jerarquia de **classes** en la següent imatge:

![Jerarquia InputStream](T2_2_1.png)

De moment mirem únicament les que estan en color **taronja** , que
especificaran quina serà la font de dades:

Classe | Explicació  
---|---  
**FileInputStream** | Per a llegir informació d'un fitxer  
**PipedInputStream** | Per a llegir des d'una tuberia (és a dir informació que ve d'un altre programa)   
**ByteArrayInputStream** | L'entrada serà un array de bytes   
**SequenceInputStream** | Servirà per enllaçar dues entrades en una de sola, seqüencialment   
  
Evidentment ens centrarem en la primera, que és la que més ens interessa per a
la permanència de les dades, però posarem algun exemple de les altres
(concretament **ByteArrayInputStream**).

Els fluxos d'eixida són molt molt pareguts, tots ells heretaran de
**OutputStream** :

Classe | Explicació  
---|---  
**FileOutputStream** | Per a guardar informació en un fitxer  
**PipedOutputStream** | Per a traure cap a una tuberia (és a dir informació que anirà a un altre programa)   
**ByteArrayOutputStream** | L'eixida serà un array de bytes   
  
```Constructors de FileInputStream```

Com hem comentat, qui més ens interessa de tots els InputStream és el
**FileInpuStream** , per a poder accedir a la informació d'un fitxer. Dos són
els constructors de FileInputStream:

  * **FileInputStream (_f_ : File)**: en el paràmetre se li passa un File (dels vistos en el tema anterior), que ha de ser una referència al fitxer.
  * **FileInputStream (_nom_f_ : String)**: en el paràmetre se li passa un String amb el nom (i la possible ruta) del fitxer. Ens permetrà fer referència al fitxer de forma més ràpida, sense haver de passar per un File.

```Constructors del FileOutputStream```

Canviaran lleugerament respecte als d'entrada, ja que a més de fer referència
al fitxer, opcionalment podrem d'especificar la manera d'escriure en el fitxer
en cas que aquest ja existesca: bé afegint al final, o bé destruint la
informació anterior. Aquestos són els constructors:

  * **FileOutputStream (_f_ : File)**: en el paràmetre se li passa un File. Si no existia, el crearà; si ja existia esborrarà el contingut. En ambdós casos l'obrirà en mode escriptura.
  * **FileOutputStream (_nom_f_ : String)**: igual que en l'anterior, però en el paràmetre se li passa un String amb el nom (i la possible ruta) del fitxer.
  * **FileOutputStream (_f_ : File, **_**afegir**_**: Boolean)** : és com el primer, però si en el segon paràmetre se li passa **true** , en cas que ja existira el fitxer, la informació s'afegirà al final, en compte de substituir el que ja hi havia. Si en aquest paràmetre se li passa **false** s'esborrarà el contingut anterior (com en el primer cas).
  * **FileOutputStream (_nom_f_ : String**,**__**afegir**__****: Boolean)** : igual que en l'anterior, però en el primer paràmetre se li passa un String amb el nom (i la possible ruta) del fitxer.


Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 2.5](http://creativecommons.org/licenses/by-nc-sa/2.5/)

