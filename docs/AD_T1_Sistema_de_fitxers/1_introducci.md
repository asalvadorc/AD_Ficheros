# 1.- Introducció

Un **fitxer** o **arxiu** és un conjunt de bits guardats en un dispositiu (com
podria ser per exemple un disc dur). Els fitxers ens garantitzen la
**persistència** , ja que encara que apaguem l'ordinador podrem recuperar la
informació, cosa que no passaria amb la informació guardada en memòria RAM. El
tema de la persistència és justament el que buscarem durant tot el curs.**  
**

Un fitxer tindrà un nom que l'identifica. Aquest nom pot tenir opcionalment
una extensió, generalment de 3 caràcters que tradicionalment ha servit per
identificar el tipus de fitxer. El nom i l'extensió van separats per un punt.

En els sistemes informàtics actuals, en els quals un únic ordinador pot
arribar a tenir guardats milions de fitxers, resulta imprescindible un sistema
que permeta una gestió eficaç de localització, de manera que els usuaris
puguem moure’ns còmodament entre tants arxius. La major part de **sistemes de
fitxers** han incorporat **contenidors jerarquitzats** que actuen a mode de
**directoris** facilitant la classificació, la identificació i localització
dels arxius. Els directoris s’han acabat popularitzant sota la versió gràfica
de **carpetes**. Dins d'un mateix directori, el nom del fitxer (o
subdirectori) ha de ser únic.

Hem de tenir en compte, que a més dels fitxers guardats en el dispositiu de
l'ordinador (el disc dur, o un altre dispositiu), la necessitat desmesurada
d’espai d’emmagatzematge ha dut els Sistemes Operatius a treballar amb una
gran quantitat de dispositius i a permetre l’accés remot a uns altres sistemes
de fitxers, distribuïts per la xarxa.

  * Per a poder gestionar tanta varietat de sistemes de fitxers, alguns sistemes operatius com **Linux o Unix** utilitzen l’estratègia d’unificar tots els sistemes en **un únic sistema de fitxers** , per tal d’aconseguir una forma d’accés unificada i amb una única jerarquia que facilite la referència a qualsevol dels seus components, amb independència del dispositiu en el qual es troben realment ubicats. En Linux, siga quin siga el dispositiu o el sistema remot real on es guardarà l’arxiu,**la ruta tindrà sempre la mateixa forma**. Observeu que per a recórrer la ruta jeràrquica on es troba el fitxer s'utilitza**la barra de dividir** :
~~~
/dir_1/dir_2/dir_3/.../dir_n/fitxer.txt
~~~

  * Per contra, l’estratègia d’altres Sistemes Operatius com **Windows** passa per mantenir ben diferenciats cadascun dels sistemes i dispositius on es tinga accés. Per distingir el sistema al qual es vol fer referència, Windows utilitza una denominació específica del dispositiu o servidor, que incorpora a la ruta del fitxer o directori a referenciar. Encara que Microsoft ha apostat clarament per la convenció **UNC** (_Uniform Naming Convention_), l’evolució d’aquest sistema operatiu, que té com a origen l’MS-DOS, ha fet que coexistesca amb una altra convenció també molt estesa, la que utilitza una lletra de l’alfabet seguida de dos punts per a identificar el dispositiu on es troba el fitxer. A continuació il·lustrem amb un exemple les dues convencions. Observeu com en els dos casos s'utilitza la **contra-barra** :
~~~
F:\dir_1\dir_2\dir_3\\...\dir_n\fitxer.txt

\\\Servidor_1\dir_1\dir_2\dir_3\\...\dir_n\fitxer.txt
~~~

Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 2.5](http://creativecommons.org/licenses/by-nc-sa/2.5/)

