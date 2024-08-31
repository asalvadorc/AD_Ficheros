# 2.1.1 - Mètodes del InputStream

<u>**Nota**</u>

<div style="background-color: #d6eaf8; color: black; padding: 5px;">
Per a fer els primers exemples, i únicament per comoditat, utilitzarem fitxers
de text, encara que estiguem en fluxos orientats a byte. Açò no és l'adequat,
ja que per a fitxers de text hauríem d'utilitzar fluxos orientats a caràcter.
Però com dic és per comoditat, perquè serà molt fàcil crear fitxers des de
qualsevol editor de textos, i que després utilitzarem des de Java o Kotlin.
L'inconvenient serà que no tots els caràcters eixiran de forma correcta,
justament per utilitzar els fluxos de dades orientats a byte.
</div>
<p></p>
El primer mètode que hem de veure del **InputStream** és aquell que ens permet
una lectura senzilla:

  * int **read()** : llig el següent byte del flux d'entrada i el retorna com un **enter**. Si no hi ha cap byte disponible perquè s’ha arribat al final de la seqüència de bytes, es retornarà -1. Si no es pot llegir el següent byte per alguna causa (per exemple si després d'arribar al final intentem llegir un altre byte, o perquè es produeix un error en llegir l'entrada) es llançarà una excepció del tipus **_IOException_**. Es tracta d’un mètode abstracte, que les classes especifiques sobreescriuran adaptant-lo a una font de dades concreta (un fitxer, un array de bytes, ...). I observeu com es tracta d'una lectura seqüencial. Comencem pel primer byte del fitxer, i a cada **read** llig el següent byte fins arribar al final. Els tractaments que veurem en aquest tema seran sempre seqüencials.

Abans de veure altres mètodes, mirem un exemple. Per a aquest exemple fa falta
un fitxer anomenat **f1.txt** , que pot ser un fitxer de text creat amb
qualsevol editor senzillet, com per exemple **gedit** o el **Bloc de notes**.
Ha d'estar en el directori del projecte (el projecte **Tema2**), i així no
caldrà posar la ruta. Per exemple podríem posar el següent contingut:
~~~
    Hola, què tal?
~~~
El que farà el programa és traure per pantalla caràcter a caràcter (en línies
diferents). L'heu de copiar en un fitxer anomenat **Exemple_2_01.kt** dins
d'un paquet anomenat **exemples** en el projecte del Tema 2:

    
    
    package exemples
    
    import java.io.FileInputStream
    
    fun main(args: Array<String>){
    	val f_in = FileInputStream("f1.txt")
    	var c = f_in.read()
    	while (c!=-1){
    		println(c.toChar())
    		c = f_in.read()
    	}
    	f_in.close()
    }

El resultat en Ubuntu serà aquest:
~~~
  H  
  o  
  l  
  a  
  ,

  q  
  u  
  Ã  
  ¨

  t  
  a  
  l  
  ?  
~~~ 

Potser en Windows si que apareguen bé tots els caràcters, ja que utilitza per
defecte una altra codificació. Però no li donarem ara importància al fet que
no apareguen bé els caràcters especials. Observeu com estem utilitzant un
**InputStream** , concretament un **FileInputStream** , per a llegir un fitxer
de text. Açò no és el més apropiat, com ja havíem comentat abans, sinó que
hauríem d'utilitzar algun flux orientat a caràcters, i no orientat a bytes. El
programa funcionarà si utilitzem codificació ASCII (o ISO-8859) ja que cada
caràcter es guarda en un byte. Si ens despistem i el fitxer el gaurdem en
UTF-8, no eixiran bé els caràcters com ç, ñ o vocals accentuades (que es
guarden en 2 bytes). I si el guardem en UTF-16, encara eixirà pitjor.

Hem utilitzat el constructor que accepta un String com a paràmetre. Queda més
curt, però seria totalment equivalent substituir la construcció anterior per
aquestes dues línies

    
    
    	val f = File("f1.txt")
    	val f_in = FileInputStream(f)

El **read** obté un enter, que després l'intentem convertir en caràcter.
Finalitzem quan l'enter és -1.

Aquest segon exemple té l'entrada no des d'un fitxer, sinó des d'un
**ByteArrayInputStream**. A banda de que l'hem d'inicialitzar diferent, podem
observar com el tractament posterior és idèntic. Copieu-lo en un fitxer
anomenat **Exemple_2_02.kt** :

    
    
    package exemples
    
    import java.io.ByteArrayInputStream
    
    fun main(args: Array<String>) {
    	val ent_1 = "Aquest és un byte array"
    	val f_in = ByteArrayInputStream(ent_1.toByteArray())
    	var c = f_in.read()
    	while (c != -1) {
    		println(c.toChar())
    		c = f_in.read()
    	}
    	f_in.close()
    }

Una altra vegada els caràcters especial eixiran malament, ja que en compte de
un **InputStream** (en aquest cas **ByteArrayInputStream**) el més adequat
seria un flux orientat a caràcters, però com a exemple sí que ens val.

Mirem un tercer exemple, per veure el **SequenceInputStream** , on es poden
enganxar de forma sequencial diferents InputStream. Després d'aquest exemple
ja ens centrarem en els fitxers, que és el que ens interessa. Copieu-lo en un
fitxer anomenat **Exemple_2_03.kt** :

    
    
    package exemples
    
    import java.io.ByteArrayInputStream
    import java.io.FileInputStream
    import java.io.SequenceInputStream
    
    fun main(args: Array<String>) {
    	val f1 = FileInputStream("f1.txt")
    	val ent_1 = "Aquest és un byte array"
    	val f2 = ByteArrayInputStream(ent_1.toByteArray())
    	val f_in = SequenceInputStream(f1,f2)
    	var c = f_in.read()
    	while (c != -1) {
    		println(c.toChar())
    		c = f_in.read()
    	}
    	f_in.close()
    }

Altres mètodes del **InputStream** són:

  * int **read(_buffer_ : ByteArray)**: llig un número determinat de bytes de l'entrada, guardant-los en el paràmetre (que actuarà com un buffer). El número de bytes llegits serà com a màxim la grandària del buffer, encara que podria ser menor (si no hi ha prou bytes, per exemple). El mètode tornarà el número de bytes que realment s'han llegit com un enter. Si no hi haguera cap byte disponible, es retornarà -1.
  * int **available()** : indica quants bytes hi ha disponibles per a la lectura. Sobretot serviria com a condició de final de bucle (si hi ha 0 bytes disponibles, és que ja hem acabat), encara que hi ha altres maneres de fer la condició de final de bucle.
  * long **skip(_despl_ : Long)**: salta, despreciant-los, tant bytes com indica el paràmetre. Podria ser que no puguera saltar el número de bytes especificat per diferents raons. Torna el número de bytes realment saltats.
  * int **close()** : tanca el flux de dades.

Mirem un altre exemple, utilitzant ara el buffer com a paràmetre del **read**.
Fa falta que existesca un fitxer anomenat **f2.txt** en l'arrel del projecte,
com es comenta després. Copieu-lo en un fitxer anomenat **Exemple_2_04.kt** :

    
    
    package exemples
    
    import java.io.FileInputStream
    
    fun main(args: Array<String>) {
    	val f_in = FileInputStream("f2.txt")
    	var buffer = ByteArray(30)
    	var n = f_in.read(buffer)
    	while (n != -1) {
    		for (i in 0..n - 1)
    			print(buffer[i].toChar())
    		println("")
    		n = f_in.read(buffer)
    	}
    	f_in.close();
    }

Es llegiran els caràcters de 30 en 30, ja que el buffer és d'aquesta
grandària. Com que es guarda en un buffer de bytes (bytes, no caràcters),
haurem de recórrer aquest buffer (fins el número de caràcters llegits, que és
**n**) convertint cada byte en caràcter. Hem suposat que en el fitxer
**f2.txt** tenim un text prou llarg com per a veure el funcionament. Si per
exemple el contingut de **f2.txt** és aquest:
~~~
Hola. Aquest és un text més llarg, per veure com gestiona els bytes amb un
buffer de 30 caràcters.  
Com que ho llegim des d'un InputStream, els caràcters especials potser no
isquen bé.
~~~

Aquesta seria l'eixida:
~~~
Hola. Aquest ￃﾩs un text mￃﾩs  
llarg, per veure com gestiona  
els bytes amb un buffer de 30  
carￃﾠcters.  
Com que ho llegim  
des d'un InputStream, els carￃ  
ﾠcters especials potser no isq  
uen bￃﾩ.
~~~
Recordeu que estem llegint un fitxer de text des d'un InputStream, cosa gens
convenient ja que els caràcters com ç, ñ, o vocals accentuades difícilment
podrem fer que apareguen bé. Ho arreglarem amb els fluxos orientats a
caràcter.

Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 2.5](http://creativecommons.org/licenses/by-nc-sa/2.5/)

