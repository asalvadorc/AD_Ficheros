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



Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 2.5](http://creativecommons.org/licenses/by-nc-sa/2.5/)

