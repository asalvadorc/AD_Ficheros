# 2.1.2 - Mètodes del OutputStream

Comencem també pel més senzill i primordial, el mètode que escriu un byte
(recordeu que estem en fluxos orientats a bytes).

  * void **write(_byte_ : Int) **: escriu el byte passat com a paràmetre en el flux d'eixida. Encara que el paràmetre és de tipus int, només s'escriurà un byte. Si no es poguera fer l'escriptura per qualsevol motiu (per exemple, disc ple), es llançarà una excepció de tipus **IOException**.

Igual que en l'apartat anterior, anem a veure un exemple senzill
d'utilització, en què guardarem en un fitxer el contingut d'una cadena (encara
que ja sabem que no és el més apropiat utilitzar fluxos orientats a bytes per
a informació de caràcters).

En aquest primer exemple del **OutputStream** treballarem sobre un fitxer
inexistent. Es podrà comprovar que el resultat serà la creació del fitxer amb
el contingut. Hem de fer constar que si no es tanca el fitxer (millor dit el
flux d'eixida) podria ser que no es guardara res en el fitxer. Per tant
**tancar és una operació ben important que no hem d'oblidar**.

Copieu el següent codi en un fitxer anomenat **Exemple_2_11.kt** :

    
    
    package exemples
    
    import java.io.FileOutputStream
    
    fun main(args: Array<String>) {
    	val text = "Contingut per al fitxer."
    	val f_out = FileOutputStream("f3.txt")
    	for (c in text) 
    		f_out.write(c.toInt())
    	f_out.close()
    }

Observeu com hem convertit cada caràcter a **Int** per a que puga funcionar,
ja que el mètode **write()** accepta un enter.

En el constructor del OutputStream no hem indicat el segon paràmetre, aquell
que indicava si era per a afegir o no, i per tant si no existia el fitxer el
crearà, però si ja existia el fitxer, destruirà el seu contingut i el
substituirà pel nou contingut. Per això si tornem a executar el programa,
tindrem el mateix resultat.
~~~
Contingut per al fitxer.
~~~
La codificació del fitxer haurà segut la que tinga per defecte el Sistema
Operatiu, que en el cas d'Ubuntu és UTF-8, i en el cas de Windows és ISO-8859.

Anem a provar a substituir el constructor, posant ara

    
    
    val f_out = FileOutputStream("f3.txt",true)

Si l'executem una altra vegada, veurem que afegirà al final, sense destruir el
que ja hi havia.
~~~
Contingut per al fitxer.Contingut per al fitxer.
~~~
Altres mètodes del OutputStream són:

  * void **write(_buffer_ : ByteArray)** : escriu el contingut de l'array de bytes al fitxer. Cal que buffer no siga nul, o provocarem un error.
  * void **write(_buffer_ : ByteArray, _pos_ : Int, _llarg_ : Int)** : escriu al fitxer el contingut de l'array que està a partir de la posició **pos** i tants bytes com assenyale **llarg**.
  * void **flush()** : Guardar les dades en un fitxer és una operació relativament lenta, ja que és accedir a un dispositiu lent (millor dit, no tan ràpid com la memòria). És habitual que s'utilitze una memòria intermèdia per a que les coses no vagen tan lentes (com si fóra una caché). Però potser que les dades no estiguen guardades encara en el fitxer, sinó que encara estiguen en aquesta caché. El mètode **flush** obliga a escriure els bytes que queden encara a la caché físicament al fitxer d'eixida.
  * void **close()** : tanca el flux d'eixida, alliberant els recursos. Si quedava alguna cosa en la caché, es guardarà al fitxer i es tancarà el flux.

En aquest exemple es copia el contingut del fitxer **f2.txt** en el fitxer
**f4.txt** , però en compte d'anar byte a byte, anirem de 30 en 30, amb un
buffer de 30 posicions. Podríem cometre l'error de la línia 13 del següent
programa, la del comentari, d'escriure sempre els 30 caràcters. Copieu el
següent codi en un fitxer anomenat **Exemple_2_12.kt** :

    
    
    package exemples
    
    import java.io.FileInputStream
    import java.io.FileOutputStream
    
    fun main(args: Array<String>) {
    	val f_in = FileInputStream("f2.txt")
    	val f_out = FileOutputStream("f4.txt")
    
    	var buffer = ByteArray(30)
    	var num = f_in.read(buffer)
    	while (num != -1) {
    		f_out.write(buffer)    // açò és un error
    		num = f_in.read(buffer)
    	}
    	f_in.close();
    	f_out.close();
    }

D'aquesta manera, l'última vegada que és llig és molt possible que no hi hagen
exactament 30 caràcters. Si hi ha menys de 30 caràcters, només es llegiran els
que queden al principi del buffer, i en la resta del buffer hi ha la
informació anterior, la de la penúltima lectura. En definitiva, tenim
"basura", i si no ho controlem el resultat no serà el correcte. Aquest ser`el
contingut de **f4.txt** :
~~~
Hola. Aquest és un text més llarg, per veure com gestiona els bytes amb un
buffer de 30 caràcters.  
Com que ho llegim des d'un InputStream, els caràcters especials potser no
isquen bé.  
pecials potser no isq
~~~
Ha eixit d'aquesta manera perquè l'última vegada només s'han llegit 9 bytes.
Els 21 restants tenen la informació encara de la penúltima lectura.

Per a fer-lo de forma correcta, ens aprofitem de que **read(buffer)** torna el
número de bytes realment llegits, per escriure exactament aquest número. Per
tant substituirem la línia 13, la del comentari, per aquesta altra:

    
    
    f_out.write(buffer,0,num)     // ara sí que funcionarà bé

Ara el contingut de **f4.txt** serà idèntic al de **f2.txt**

<u>**Nota important**</u>

<div style="background-color: #d6eaf8; color: black; padding: 5px;">
Per a assegurar-nos que realment escrivim en el fitxer i no es queda res en la
memòria intermèdia, <b>hem de tancar sempre els fluxos d'eixida</b>. Si ens
oblidem de tancar-los, és molt fàcil que no s'acabe d'escriure físicament en
el fitxer.
</div>
<p></p>


Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 2.5](http://creativecommons.org/licenses/by-nc-sa/2.5/)

