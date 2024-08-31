# 2.2.1 - Mètodes del Reader

Els mètodes del **Reader** són absolutament similars als del **InputStream** .
La diferència és que ara llegirà sempre un caràcter. I no ens haurem de
preocupar pel format en què està guardat, i de i ocupa un o dos bytes. Sempre
el llegirà bé, siga quina siga la codificació utilitzada, com ja havíem
comentat abans:

  * int **read()** : llig el següent caràcter del flux d'entrada i el retorna com un enter. Si no hi ha cap caràcter disponible perquè s’ha assolit el final de la seqüència, es retornarà -1. Si no es pot llegir el següent caràcter per alguna causa (per exemple si després d'arribar al final intentem llegir un altre caràcter, o perquè es produeix un error en llegir l'entrada) es llançarà una excepció del tipus ** _IOException_**. Es tracta d’un mètode abstracte, que les classes especifiques sobreescriuran adaptant-lo a una font de dades concreta (un fitxer, un array de caràcters, ...).

Abans de veure altres mètodes, mirem un exemple que és idèntic al primer
exemple del InputStream, però canviant FileInputStream per FileReader. Llegirà
el mateix fitxer anomenat **f1.txt** , utilitzat en aquell moment, però ara
segurament llegirà tots els caràcters bé. El que farà és traure per pantalla
caràcter a caràcter (en línies diferents). Copieu el següent codi en un fitxer
anomenat **Exemple_2_21.kt** :

    
    
    package exemples
    
    import java.io.FileReader
    
    fun main(args: Array<String>){
    	val f_in = FileReader("f1.txt")
    	var c = f_in.read()
    	while (c!=-1){
    		println(c.toChar())
    		c = f_in.read()
    	}
    	f_in.close()
    }

Ara segurament sí que haurà llegit bé tots els caràcters, incloent ñ, ç,
vocals accentuades, etc. Si encara tenim el mateix contingut en **f1.txt** ,
el resultat serà ara:
~~~
H  
o  
l  
a  
,  
  
q  
u  
è  
  
t  
a  
l  
?  
~~~  

El més normal és que en crear el fitxer **f1.txt** amb algun editor, el
guardem amb la codificació per defecte, que en cas de Windows és ASCII (o
ISO-8859) i en el cas de Linux és UTF-8. I després des de Java, el
**FileReader** utilitzarà la codificació per defecte del Sistema Operatiu. És
a dir que en Linux el fitxer ha d'estar guardat en UTF-8 per a que el puga
llegir bé, i en Windows en ASCII.

Mirem també l'exemple equivalent al segon. Allà utilitzàvem un
**ByteArrayInputStream** com a entrada. Ara podríem utilitzar un
**CharArrayReader** , però ho farem amb un **StringReader** , i quedarà més
curt. A banda de que l'hem d'inicialitzar diferent, podem observar com el
tractament posterior és idèntic. Copieu el següent codi en un fitxer anomenat
**Exemple_2_22.kt** :

    
    
    package exemples
    
    import java.io.CharArrayReader
    
    fun main(args: Array<String>) {
    	val ent_1 = "Aquest és un byte array"
    	val f_in = CharArrayReader(ent_1.toCharArray())
    	var c = f_in.read()
    	while (c != -1) {
    		println(c.toChar())
    		c = f_in.read()
    	}
    	f_in.close()
    }

Altres mètodes del **Reader** són:

  * int **read(char[ ]_buffer_)**: llig un número determinat de caràcters de l'entrada, guardant-los en el paràmetre (que actuarà com un buffer). El número de caràcters llegits serà com a màxim la grandària del buffer, encara que podria ser menor (si no hi ha prou caràcters, per exemple). El mètode tornarà el número de caràcters que realment s'han llegit com un enter. Si no hi haguera cap caràcter disponible, es retornaria -1.
  * int **available()** : indica quants caràcters hi ha disponibles per a la lectura. Sobretot serviria com a condició de final de bucle: si hi ha 0 caràcters disponibles, és que ja hem acabat. Tot i això, hi ha altres maneres de fer la condició de final de bucle.
  * long **skip(long _despl_)**: salta, despreciant-los, tants caràcters com indica el paràmetre. Podria ser que no puguera saltar el número de caràcters especificat per diferents raons. Torna el número de caràcters realment saltats.
  * int **close()** : tanca el flux de dades.

Mirem un altre exemple, utilitzant ara el buffer com a paràmetre del **read**.
És idèntic al de l'apartat del InputStream. La diferència és que ara s'haurien
de llegir bé tots els caràcters. Copieu el següent codi en un fitxer anomenat
**Exemple_2_23.kt** :

    
    
    package exemples
    
    import java.io.FileReader
    
    fun main(args: Array<String>) {
    	val f_in = FileReader("f2.txt")
    	var buffer = CharArray(30)
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
grandària. Com que ara es guarda en un buffer de caràcters, haurem de recórrer
aquest buffer (fins el número de caràcters llegits, que és **n**) . Hem
suposat que en el fitxer **f2.txt** tenim un text prou llarg com per a veure
el funcionament.

Aquesta seria l'eixida:
~~~
Hola. Aquest és un text més ll  
arg, per veure com gestiona el  
s bytes amb un buffer de 30 ca  
ràcters.  
Com que ho llegim des  
d'un InputStream, els caràcte  
rs especials potser no isquen  
bé.
~~~
Efectivament, s'han llegit tots els caràcters perfectament.


Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 2.5](http://creativecommons.org/licenses/by-nc-sa/2.5/)

