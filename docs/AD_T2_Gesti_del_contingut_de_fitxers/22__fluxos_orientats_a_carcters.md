# 2.2 - Fluxos orientats a caràcters - Classes

Treballar amb caràcters implica una dificultat apreciable, a causa sobretot de
la diversitat de codificacions existents.

Per poder solucionar-ho, Java disposa de dues jerarquies, una d'entrada i una
d'eixida, diferents de les que ja hem vist per a bytes (que eren InputStream i
OutputStream). Aquestes jerarquies per a caràcters seran molt semblants a les
de bytes, però sempre orientades a caràcters. Kotlin, per heretar de Java,
també les tindrà, encara que com veurem en l'última pregunta, podrem
simplificar les coses.

Igual que en els casos anteriors, tindrem unes classes abstractes, **Reader**
i **Writer** , que no es poden instanciar directament (no podrem crear un
objecte d'aquestes classes). Serviran per a homogeneïtzar tots els fluxos
d'entrada i d'exida orientats a caràcter.

La super-classe **Reader** servirà per a fer l'entrada des de qualsevol
dispositiu: fitxer, array de caràcters, una canonada ("tuberia", per a dur
dades des d'una altra aplicació). Totes les classes d'entrada heretaran
d'ella, i serviran per especificar exactament d'on (per exemple un fitxer:
**FileReader**) o per a donar alguna altra funcionalitat, com anirem veient a
poc a poc. D'aquesta manera, els mètodes que es defineixen s'hauran
d'implementar per les classes que hereten d'ella i assegura una uniformitat,
siga quina siga la font.

Fem una ullada ràpida a la jerarquia de **classes** en la següent imatge:

![Jerarquia Reader-Writer](T2__2_2.png)

De moment mirem únicament les que estan en color **taronja** , que
especificaran quina serà la font de dades:

Classe | Explicació  
---|---  
**FileReader** | Per a llegir caràcters d'un fitxer  
****PipedReader**** | Per a llegir des d'una tuberia (és a dir informació que ve d'un altre programa)   
**CharArray**Reader**** | L'entrada serà un array de caràcters  
**StringReader** | L'entrada serà un string  
  
Evidentment ens centrarem en la primera, que és la que més ens interessa per a
la permanència de les dades.

Els fluxos d'eixida són molt molt pareguts, tots ells heretaran de **Writer**
:

Classe | Explicació  
---|---  
**FileWriter** | Per a guardar caràcters en un fitxer  
**Piped**Writer**** | Per a traure cap a una tuberia (és a dir informació que anirà a un altre programa)   
**CharArray**Writer**** | L'eixida serà un array de caràcters  
**StringWriter** | L'eixida serà un string   
  
Hem de fer constar que les classes d’emmagatzematge intern (utilitzem Java o
Kotlin), com ara **CharArrayReader** , **CharArrayWriter** , **StringReader**
, **StringWriter** , **PipedReader** , **PipedWriter** utilitzen sempre la
codificació pròpia de Java (unicode de 16 bits: **UTF-16**), ja que guarden
les dades a la memòria basant-se en els tipus dades de tractament de caràcters
de Java o Kotlin (C _har_ i _String_).

En canvi les classes **FileReader** o **FileWriter** agafen la codificació
**per defecte del sistema operatiu amfitrió**. L’usuari no pot seleccionar
diferents sistemes de codificació en crear les instàncies. Així, una màquina
virtual Java sobre Windows utilitzarà, per defecte, la codificació ISO-8859-1,
però si corre sobre Linux, la codificació serà UTF-8. De tota manera veurem
que sí que podrem arribar a especificar quin és el joc de caràcters que volem
utilitzar en la pregunta 3.3. Intentarem veure exemples de tot.

```Constructors de FileReader```

De forma totalment paral·lela als fluxos orientats a byte, el **FileReader**
té dos constructors, acceptant com a paràmetre un File o un String (amb el nom
del fitxer). La diferència ara és que la unitat de transferència serà el
caràcter (en compte d'un byte):

  * **FileReader (_f_ : File)**: en el paràmetre se li passa un File (dels vistos en el tema anterior), que ha de ser una referència al fitxer.
  * **FileReader (_nom_f_ : String)**: en el paràmetre se li passa un String amb el nom (i la possible ruta) del fitxer. Ens permetrà fer referència al fitxer de forma més ràpida, sense haver de passar per un File.

```Constructors del FileWriter```

També totalment paral·lel al FileOutputStream. Canviaran lleugerament respecte
als d'entrada, ja que a més de fer referència al fitxer, opcionalment podrem
d'especificar la manera d'escriure en el fitxer en cas que aquest ja
existesca: bé afegint al final, o bé destruint la informació anterior.
Aquestos són els constructors:

  * **FileWriter (_f_ : File)**: en el paràmetre se li passa un File. Si no existia, el crearà; si ja existia esborrarà el contingut. En ambdós casos l'obrirà en mode escriptura.
  * **FileWriter (_nom_f_ : String)**: igual que en l'anterior, però en el paràmetre se li passa un String amb el nom (i la possible ruta) del fitxer.
  * **File**Writer** _(f: File_ , **_**afegir**_**: Boolean)** : és com el primer, però si en el segon paràmetre se li passa **true** en compte de substituir el que ja hi havia, la informació s'afegirà al final. Si en aquest paràmetre se li passa **false** s'esborrarà el contingut anterior (com en el primer cas).
  * **File**Writer** _(nom_f: String_**,**__**afegir**__****: Boolean)** : igual que en l'anterior, però en el primer paràmetre se li passa un String amb el nom (i la possible ruta) del fitxer.

Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 2.5](http://creativecommons.org/licenses/by-nc-sa/2.5/)

