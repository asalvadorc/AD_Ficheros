# 2.2.2 - Mètodes del Writer

Comencem també pel més senzill i primordial, el mètode que escriu un caràcter.

  * void **write(_car_ : Int) **: escriu el caràcter passat com a paràmetre en el flux d'eixida. En cas que siga un FileWriter, escriurà el caràcter amb la codificació per defecte del S.O. : en Windows ISO-8839 i en Linux UTF-8. Si no es poguera fer l'escriptura per qualsevol motiu (per exemple, disc ple), es llançarà una excepció de tipus **IOException**.

Igual que en l'apartat anterior, anem a veure un exemple senzill
d'utilització, en el qual guardarem en un fitxer el contingut d'una cadena,
ara ja sense por als caràcters estranys.

En aquest primer exemple del **Writer** treballarem sobre un fitxer
inexistent. Es podrà comprovar que el resultat serà la creació del fitxer amb
el contingut. Copieu el següent codi en un fitxer anomenat **Exemple_2_31.kt**
:

<u>**Nota**</u>

<div style="background-color: #d6eaf8; color: black; padding: 5px;">
Hem de fer constar que si no es tanca el fitxer (millor dit el flux d'eixida)
podria ser que no es guardara res en el fitxer. Per tant és una operació ben
important que no hem d'oblidar.
</div>
<p></p>
    
    
    package exemples
    
    import java.io.FileWriter
    
    fun main(args: Array<String>) {
    	val text = "Contingut per al fitxer. Ara ja sense por a caràcters especials: ç, à, ú, ..."
    	val f_out = FileWriter ("f5.txt")
    	for (c in text) {
    		f_out.write(c.toInt())
    	}
    	f_out.close()
    }

  
  

En el constructor del **Writer** no hem indicat el segon paràmetre, aquell que
indicava si era per a afegir o no, i per tant si no existia el fitxer el
crearà, però si ja existia el fitxer, destruirà el seu contingut i el
substituirà pel nou contingut. Per això si tornem a executar el programa,
tindrem el mateix resultat en **f5.txt**
~~~
Contingut per al fitxer. Ara ja sense por a caràcters especials: ç, à, ú, ...
~~~
Anem a provar a substituir el constructor, posant ara

    
    
    val f_out = FileWriter ("f5.txt", true)

Si l'executem, veurem que afegirà al final, sense destruir el que ja hi havia.
~~~
Contingut per al fitxer. Ara ja sense por a caràcters especials: ç, à, ú, ...Contingut per al fitxer. Ara ja sense por a caràcters especials: ç, à, ú, ...
~~~
Altres mètodes del **Writer** són:

  * void **write(_buffer_ : CharArray)** : escriu el contingut de l'array de caràcters al fitxer. Cal que buffer no siga nul, o provocarem un error.
  * void **write(_buffer: CharArray_ , _pos_ : Int, _llarg_ : Int)** : escriu al fitxer el contingut de l'array que està a partir de la posició **pos** i tants caràcters com assenyale **llarg**.
  * void **flush()** : Guardar les dades en un fitxer és una operació relativament lenta, ja que és accedir a un dispositiu lent (millor dit, no tan ràpid com la memòria). És habitual que s'utilitze una memòria intermèdia per a que les coses no vagen tan lentes (com si fóra una caché). Però potser que les dades no estiguen guardades encara en el fitxer, sinó que encara estiguen en aquesta caché. El mètode **flush** obliga a escriure els caràcters que queden encara a la caché físicament al fitxer d'eixida.
  * void **close()** : tanca el flux d'eixida, alliberant els recursos. Si quedava alguna cosa en la caché, es guardarà al fitxer i es tancarà el flux.

Aquestos mètodes són totalment similars als del OutputStream. A banda
d'aquestos, el **Writer** té un altre, que pot ser especialment útil per a
caràcters:

  * void **write(_text_ : String)** : escriu tot el contingut del String en el fitxer.


Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 2.5](http://creativecommons.org/licenses/by-nc-sa/2.5/)

