# 3 - Fluxos decoradors

Anomenem classes "**decoradores** " a aquelles que hereten d'una classe
determinada i serveixen per a dotar d'una funcionalitat extra que no tenia la
classe original.

En els fluxos, en els d'entrada i en els d'eixida, veurem uns quants
"decoradors" que ens permetran una funcionalitat extra: llegir o escriure una
línia sencera (en compte de byte a byte, o caràcter a caràcter), o guardar amb
determinat format de dades, ... En el cas de caràcters també ens permetran
triar la codificació (ISO-8859-1, UTF-8, UTF-16, ...).

Anirem veient-los poc a poc, classificats per la classe arrel, és a dir, per
una banda els decoradors del InputStream i OutputStream (orientats a byte), i
per una altra banda els de Reader i Writer (orientats a caràcter)

## 3.1 - Decoradors de InputStream i OtputStream

Com hem comentat ens serviran per a donar una funcionalitat extra. Són els que
estan de verd en la següent imatge:

![T2_2_1.png](T2_2_1.png)

Fixem-nos primers en els decoradors de **InputStream** :

Classe | Explicació  
---|---  
**FilterInputStream** | No és instanciable, únicament està per a que les altres depenguen d'ella (no la veurem)   
**LineNumberInputStream** | Afegeix el número de línia de cada línia del InputStream (no la veurem)  
**DataInputStream** | Permet llegir dades de qualsevol tipus de dades: enter, real, booleà, ...   
**BufferedInputStream** | Munta un buffer d'entrada (no la veurem)  
**PushBackInputStream** | Permet retrocedir un byte en la lectura, i per tant permet anar cap arrere (no la veurem)   
**ObjectInputStream** | Permet llegir tot un objecte  
  
I de forma quasi paral·lela tenim els decoradors de **OutputStream** :

Classe | Explicació  
---|---  
**FilterOutputStream** | No és instanciable, únicament està per a que les altres depenguen d'ella (no la veurem)   
**Data**Out** putStream** | Permet guardar al flux de dades d'eixida dades de qualsevol tipus: enter, real, booleà, ...  
**Buffered**Out** putStream** | Munta un buffer d'eixida (no la veurem)  
**PrintStream** | Permet escriure dades de diferents tipus, i té també els mètodes _printf_ i _println_  
**Object**Out** putStream** | Permet escriure (serialitzar) tot un objecte  
  
Comentem-los un poquet més.

**BufferedInputStream** i **BufferedOutputStream** ens ofereixen un buffer
d'entrada i d'eixida respectivament, per a fer la transferència més efectiva.
En la pràctica ens oferirà poques funcionalitats útils (a banda de
l'eficiència en la transferència, clar). Quan anem als decoradors de fluxos
orientats a caràcters, sí que trobarem utilitats als decoradors semblants a
aquestos, com per exemple llegir o escriure una línia sencera de caràcters.
Però aquestos orientats a bytes, no els veurem.

**DataInputStream** i **DataOutputStream** ens oferiran la possibilitat de
llegir o escriure còmodament dades de diferents tipus: enter, real, booleà,
strings, ... Els veurem en detall en el proper **Tema 3**

**ObjectInputStream** i **ObjectOutputStream** (que curiosament són els únics
que no depenen de **FilterInputStream** i **FilterOutputStream**) ens
permetran guardar o recuperar de cop tot un objecte, és a dir totes les seues
propietats (les dades de l'objecte). No ens haurem de preocupar ni de l'ordre
ni del tipus de les propietats de l'objecte: quan escrivim l'objecte, es
guardaran totes les dades de forma compacta; i quan llegim es recuperaran de
forma correcta. És per tant una parella de classes d'extrema utilitat per a
guardar objectes, que en definitiva són l'essència de la programació en Java.
Els veurem en detall en el proper **Tema 3**.

```PrintStream```

L'únic que ens queda és el que veurem ara amb un poquet més de detall, el
**PrintStream**. Ens permetrà bàsicament 3 coses:

  * Escriure dades de més d'un tipus de dades. Per exemple **print(5.25)** escriu un número real, i **print("Hola")** escriu tot un string.
  * Donar un determinat format a l'eixida, amb tota la funcionalitat a què estem acostumats amb **printf**
  * Escriure tota una línia amb **println** , és a dir, acabar una dada amb el retorn de carro, per a baixar de línia.

Mirem un exemple que ens pot donar idea de la seua funcionalitat. Copieu el
següent codi en un fitxer anomenat **Exemple_2_41.kt** :

    
    
    package exemples
    
    import java.io.PrintStream
    import java.io.FileOutputStream
    
    fun main(args: Array<String>) {
    	val f_out = PrintStream(FileOutputStream ("f6.txt"))
    
    	val a = 5.25.toFloat()
    	val b = "Hola."
    	f_out.print(b)
    	f_out.println("Què tal?")
    	f_out.println(a + 3)
    	f_out.printf("El número %d en hexadecimal és %x", 27, 27)
    
    	f_out.close();
    }

Es crearà el fitxer **f6.txt** (si ja existia esborrarà el contingut anterior)
amb el següent contingut:
~~~
Hola.Què tal?
8.25
El número 27 en hexadecimal és 1b
~~~
En realitat el **PrintStream** , a banda del constructor que accepta un
**OutputStream** , també té un altre que accepta un **File** i fins i tot un
altre que accepta un **String** amb el nom del fitxer. Per tant, la següent
sentència també ens funcionaria:

        
    	val f_out = PrintStream("f6.txt")


## 3.2 - Decoradors de Reader i Writer

Mirem ara els decoradors de la jerarquia **Reader** i **Writer** . Tornen a
ser els de color verd. Els de color gris **InputStreamReader** i
**OutputStreamWriter** són conversors que permeten passar un **InputStream** a
un **Reader** i un **OutputStream** a **Writer**. Els veurem en la següent
pregunta.

![T2_2_2.png](T2__2_2.png)

Fixem-nos primers en els decoradors de **Reader** :

Classe | Explicació  
---|---  
**FilterReader** | No és instanciable, únicament està per a que les altres depenguen d'ella (no la veurem)   
**PushBackInputStream** | Permet retrocedir un caràcter en la lectura, i per tant permet anar cap arrere (no la veurem)   
**Buffered**Reader**** | Munta un buffer d'entrada, i permet entre altres coses llegir una línia sencera  
**LineNumber**Reader**** | Afegeix el número de línia de cada línia del fitxer (no la veurem)  
  
I de forma quasi paral·lela tenim els decoradors de **Writer** :

Classe | Explicació  
---|---  
**FilterWriter** | No és instanciable, únicament està per a que les altres depenguen d'ella (no la veurem)   
**Buffered**Writer**** | Munta un buffer d'eixida, i permet entre altres coses escriure una línia sencera  
**Print**Writer**** | Permet escriure dades de diferents tipus, i té també els mètodes _printf_ i _println_  
  
El **PrintWriter** funciona quasi exactament igual que el **PrintStream** , i
per a caràcters és més útil que l'altre (per ser **Writer**), per tant és el
candidat a recordar.

El **BufferedReader** sí que ens oferirà facilitats interessants, com llegir
una línia sencera. En canvi el **BufferedWriter** no ens ofereix tantes
facilitats com el **PrintWriter** , és un poc més incòmode.

```BufferedReader i BufferedWriter. PrintWriter```

BufferedReader i BufferedWriter munten un buffer (d'entrada i d'eixida
respectivament) de caràcters per a fer més eficient la transferència. A banda
d'això tindran uns mètodes que ens seran molt útils.

<u>**BufferedReader**</u>

  * mètode **readLine()** que ens permet llegir una línia sencera del fitxer (fins al final de línia). Açò és de molta utilitat en els fitxers de text.

<u>**BufferedWriter**</u>

  * mètode **newLine()** que permet introduir el caràcter de baixada de línia
  * mètode **write(_cad_ : String, _com_ : Int, _llarg_ : Int)** que permet escriure tot un string, o una part d'ell, especificant on comença el que volem escriure i la llargària

Com veieu el **BufferedReader** sí que ens ofereix la possibilitat de llegir
una línia sencera, però en canvi el **BufferedWriter** es queda un poc curt.
Per això preferirem el **PrintWriter**.

<u>**PrintWriter**</u>

  * mètodes **print(_qualsevol_tipu_ _s_)** , que permeten imprimir una dada de qualsevol tipus: booleà, char, tots els numèrics, string, ... Serà segurament el que més utilitzarem.
  * mètodes **println**(_qualsevol_tipu_ _s_)**** , a banda de tot el de **print** , baixen de línia
  * mètode **printf()** , que permet donar un format

Veiem un senzill exemple per a copiar el contingut d'un fitxer de text i
modificar-lo lleugerament. El més còmode serà anar línia a línia. Per tant
utilitzarem el **BufferedReader** per a llegir línies, i el **PrintWriter**
per a escriure línies. La lleugera modificació consistirà en posar el número
de línia davant. Copieu el següent codi en un fitxer anomenat
**Exemple_2_51.kt** :

    
    
    package exemples
    
    import java.io.BufferedReader
    import java.io.FileReader
    import java.io.PrintWriter
    import java.io.FileWriter
    
    fun main(args: Array<String>) {
        val f_ent = BufferedReader(FileReader ("f7_ent.txt"))
        val f_eix = PrintWriter(FileWriter ("f7_eix.txt"))
        var cad = f_ent.readLine();
        var i = 0
        while (cad != null) {
            i++
            f_eix.println("" + i + ".- " + cad)
            cad = f_ent.readLine()
        }
        f_eix.close()
        f_ent.close()
    }

Si en el fitxer d'entrada (**f7_ent.txt**) tenim guardada la següent
informació (introduïda amb el notepad o gedit):
~~~
Primera
Segona
Tercera
~~~
En el fitxer d'eixida (**f7_eix.txt**) tindrem:
~~~
1.- Primera
2.- Segona
3.- Tercera
~~~

## 3.3 - Conversors: InputStreamReader i OutputStreamWriter

Una vegada vistes les jerarquies de les classes **InputStream-OutputStream**
per una banda, i **Reader-Writer** per una altra, veurem ara unes classes que
serviran per a passar d'una jeraquia a una altra. És a dir, poder passar un
**InputStream** a **Reader** , o el que és el mateix, un flux orientat a bytes
en un flux orientat a caràcters. I el mateix amb el OutputStream i el Writer.

  * **InputStreamReader** : passa un **InputStream** a **Reader**. Accepta com a paràmetre el **InputStream** i dóna com a resultat un **Reader**.
  * **OutputStreamWriter** : passa un **OutputStream** a **Writer**. Accepta com a paràmetre el **OutputStream** i dóna com a resultat un **Writer**.

A més en el constructor dels dos, **InputStreamReader** i
**OutputStreamWriter** , tenim la possibilitat d'especificar el tipus de
codificació, a més del InputStream o OutputStream. Açò ens serà molt útil,
perquè fins el moment no podíem triar el tipus de codificació d'un
**FileReader** o **FileWriter** que era UTF-8 en el cas de Linux, i ASCII
(millor dit la seua extensió ISO-8859-1) en el cas de Windows.

Mirem aquest exemple, en el qual transformem el mateix fitxer d'una
configuració a una altra. Aprofitem algun dels fitxers que ja disposem (per
exemple f5.txt, que tenia caràcters especials com vocals accentuades). En
l'exemple el tindrem en codificació UTF-8, ja que està provat en Linux. El
transformarem a ISO-8859-1. Copieu el següent codi en un fitxer anomenat
**Exemple_2_61.kt** :

    
    
    package exemples
    
    import java.io.InputStreamReader
    import java.io.FileInputStream
    import java.io.OutputStreamWriter
    import java.io.FileOutputStream
    
    fun main(args: Array<String>) {
    	val f_ent = InputStreamReader(FileInputStream("f5.txt"), "UTF-8")
    	val f_eix = OutputStreamWriter(FileOutputStream("f5_ISO.txt"), "ISO-8859-1")
    
    	var car = f_ent.read()
    	while (car != -1) {
    		f_eix.write(car)
    		car = f_ent.read()
    	}
    	f_eix.close()
    	f_ent.close()
    }

Hem posat l'entrada explícitament que siga de UTF-8. En realitat no faria
falta, ja que si treballem en Linux, aquesta serà la codificació per defecte,
i per tant seria la que utilitzaria un FileReader.

    
    
    FileReader f_ent = new FileReader("f5.txt")

Anem a fer una altra versió del mateix programa. A banda de no especificar la
codificació del fitxer d'entrada, utilitzarem els decoradors
**BufferedReader** i **PrintWriter** per a poder anar còmodament línia a
línia. Copieu el següent codi en un fitxer anomenat **Exemple_2_62.kt** :

    
    
    package exemples
    
    import java.io.FileReader
    import java.io.BufferedReader
    import java.io.FileOutputStream
    import java.io.OutputStreamWriter
    import java.io.PrintWriter
    
    fun main(args: Array<String>) {
    	val f_ent = BufferedReader(FileReader ("f5.txt"))
    	val f_eix = PrintWriter(OutputStreamWriter(FileOutputStream ("f5_ISO.txt"), "ISO-8859-1"))
    
    	var cad = f_ent.readLine()
    	while (cad != null) {
    		f_eix.println(cad)
    		cad = f_ent.readLine()
    	}
    	f_eix.close()
    	f_ent.close()
    }


Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 2.5](http://creativecommons.org/licenses/by-nc-sa/2.5/)

