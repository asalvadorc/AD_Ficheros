# 3.2 - Decoradors de Reader i Writer

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

Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 2.5](http://creativecommons.org/licenses/by-nc-sa/2.5/)

