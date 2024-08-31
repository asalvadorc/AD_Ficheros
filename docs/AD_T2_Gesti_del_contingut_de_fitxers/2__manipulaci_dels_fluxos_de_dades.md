# 2 - Manipulació dels fluxos de dades

En Java, i per tant també en Kotlin, no tindrem una única classe per a
manipular els fluxos de dades i així arribar al contingut dels fitxers. És una
cosa que de vegades se li critica a Java, que hi ha una jerarquia molt extensa
de fluxos, i són moltes classes a recordar i utilitzar. Per contra fa que siga
molt versàtil. En l'últim punt del tema veurem la simplificació que ens
proposa Kotlin.

Aquestes classes es trobaran en dues jerarquies, la dels **fluxos orientats a
bytes** i la dels **fluxos orientats a caràcters**.

  * Si les nostres dades són numèriques o de qualsevol altre tipus que puguem imaginar (imatges per exemple), ens convindran les primeres.
  * Si la informació és de caràcters, haurem d'utilitzar la segona jerarquia.

La raó de que existesca aquesta segona jerarquia orientada a caràcters és la
multitud de sistemes de codificació existents. Com havíem comentat en la
pregunta anterior, Java utilitza internament codificació UNICODE de 16 bits
(UTF-16), on cada caràcter ocupa 16 bits i així poder suportar tots els
llenguatges com el grec, àrab, ciríl·lic, xinès, .... Però UTF-8 està molt
estés, i en aquesta codificació de vegades un caràcter ocupa 8 bits, i de
vegades 16. I no podem oblidar altres sistemes de codificació, com ASCII,
ISO-8859, ... La jerarquia de classes orientades a caràcter suportarà totes
les codificacions.

Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 2.5](http://creativecommons.org/licenses/by-nc-sa/2.5/)

