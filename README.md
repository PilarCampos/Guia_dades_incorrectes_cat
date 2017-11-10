# La Guia Quartz per a les dades incorrectes

**Una guia de referència exhaustiva amb problemes reals amb les dades i suggeriments per resoldre'ls.**

El món és ple de dades. I aquestes dades són plenes d'inconvenients. Aquesta guia descriu problemes i suggereix solucions per facilitar el treball amb dades.

La majoria d'aquests problemes tenen solució. Dels que no, podem distingir entre aquells que invaliden les dades i aquells que, amb precaució, permeten continuar treballant-hi. Per tal d'evitar ambigüitats, el text s'organitza segons qui està preparat per solucionar el problema: tu, la font d'informació, un expert, etc. A vegades, a la descripció de cada problema, també s’hi inclouen suggeriments sobre què es pot fer si no es troba ajuda.

No es pot revisar cada dataset buscant tots aquests problemes. I si es fes, possiblement s'acabaria sense publicar res. Tot i així, familiaritzant-se amb aquestes incidències es tenen més opcions d'identificar els problemes abans de comentre un error. 

Per dubtes relacionats amb la guia, contacteu amb l'autor [Chris](mailto:c@qz.com) o llegiu [l'original](https://github.com/Quartz/bad-data-guide)
Per dubtes o comentaris relacionats amb la traducció, contacteu amb [Pilar](mailto:campospil@gmail.com). S'ha treballat amb la versió del github de 09/11/2017.
Correcció de la traducció per [Proofeditingasesores](http://www.proofeditingasesores.com/)

Aquest article té llicència [Creative Commons Attribution-NonCommercial 4.0 International License](http://creativecommons.org/licenses/by-nc/4.0/).

# Sumari


## Aspectes que hauria de resoldre la font d'informació

* [Falten dades](#falten-dades)
* [Les dades en blanc es reemplacen per ](#les-dades-en-blanc-es-reemplacen-per-zeros)
* [Manquen dades que hi haurien de ser](#manquen-dades-que-hi-haurien-de-ser)
* [Files o valors duplicats](#files-o-valors-duplicats)
* [La ortografia és inconsistent](#la-ortografia-és-inconsistent)
* [L'ordre de les paraules és inconsistent](#lordre-de-les-paraules-és-inconsistent)
* [Formats de dates inconsistents](#formats-de-dates-inconsistents)
* [Els formats dels decimals són inconsistents](#els-formats-dels-decimals-són-inconsistents)
* [No s'especifiquen les unitats](#no-sespecifiquen-les-unitats)
* [Els símbols monetaris són insuficients](#els-símbols-monetaris-són-insuficients)
* [Les categories han estat mal seleccionades](#les-categories-han-estat-mal-seleccionades)
* [Els noms dels camps són ambigus](#els-noms-dels-camps-són-ambigus)
* [L'origen de les dades no està documentat](#lorigen-de-les-dades-no-està-documentat)
* [Valors sospitosos](#valors-sospitosos)
* [Les dades són massa bastes](#les-dades-són-massa-bastes)
* [Els totals difereixen dels globals publicats](#els-totals-difereixen-dels-globals-publicats)
* [El full de càlcul té 65.536 files](#el-full-de-càlcul-té-65536-files)
* [El full de càlcul té 255 columnes](#el-full-de-càlcul-té-255-columnes)
* [El full de càlcul té les dates 1900, 1904, 1969 o 1970](#el-full-de-càlcul-té-les-dates-1900-1904-1969-o-1970)
* [El text s'ha convertit en nombres](#el-text-sha-convertit-en-nombres)
* [Nombres que s'han desat com a text](#nombres-que-shan-desat-com-a-text)

## Aspectes que tu pots resoldre

* [El text està codificat](#el-text-està-codificat)
* [Els espais al final de la línia estan mal codificats](#els-espais-al-final-de-la-línia-estan-mal-codificats)
* [Les dades estan en PDF](#les-dades-estan-en-pdf)
* [Les dades són massa granualrs](#les-dades-són-massa-granulars)
* [Les dades han sigut introduïdes per humans](#les-dades-han-sigut-introduïdes-per-humans)
* [Les dades estan barrejades amb formats i anotacions](#les-dades-estan-barrejades-amb-formats-i-anotacions)
* [Les agregacions es calculen amb valors que falten](#les-agregacions-es-calculen-amb-valors-que-falten)
* [La mostra no és aleatòria](#la-mostra-no-és-aleatòria)
* [El marge d'error és massa ampli](#el-marge-derror-és-massa-ampli)
* [Es desconeix el marge d'error](#es-desconeix-el-marge-derror)
* [La mostra està esbiaixada](#la-mostra-està-esbiaixada)
* [Les dades s'han editat manualment](#les-dades-shan-editat-manualment)
* [La inflació distorsiona les dades](#la-inflació-distorsiona-les-dades)
* [Variacions naturals/de temporada distorsionen dades](#variacions-naturalsde-temporada-distorsionen-les-dades)
* [El marc temporal ha estat manipulat](#el-marc-temporal-ha-estat-manipulat)
* [El marc de referència ha estat manipulat](#el-marc-de-referència-ha-estat-manipulat)

## Problemes que requereixen de l'ajuda d'un expert per resoldre'ls

* [L'autor no és de confiança](#lautor-no-és-de-confiança)
* [El procés de captura és opac](#el-procés-de-captura-és-opac)
* [Les dades són d'una precisió irreal](#les-dades-són-duna-precisió-irreal)
* [Hi ha valors atípics inexplicables](#hi-ha-valors-atípics-inexplicables)
* [Un índex emmascara variacions subjacents](#un-índex-emmascara-variacions-subjacents)
* [Hi ha p-hacking als resultats](#hi-ha-p-hacking-als-resultats)
* [La llei de Benford falla](#la-llei-de-benford-falla)
* [És massa bonic per ser veritat](#és-massa-bonic-per-ser-veritat)

## Problemes que un programador pot ajudar a resoldre

* [Les dades s'han agrupat en categories o geografies errònies](#les-dades-shan-agrupat-en-categories-o-geografies-errònies)
* [Les dades es troben en documents escanejats](#les-dades-es-troben-en-documents-escanejats)


# Llista detallada de tots els problemes 

## Aspectes que hauria de resoldre la font d'informació

### Falten dades

Alerta amb els valors en blanc o nuls als datasets, llevat que estiguis segur del seu significat. Per exemple, si les dades són anuals, és possible que aquell any no es recollissin els valors? Si es tracta d’una enquesta, potser l'entrevistat va refusar contestar-la?

Quan estiguis treballant amb dades on manquen valors, cal preguntar-se: «Sé què significa l'absència de valors?» Si la resposta és no, cal preguntar a la font.

### Les dades en blanc es reemplacen per zeros

Encara pitjor que la falta de dades és quan s'utilitzen valors arbitraris en el seu lloc. Això pot ser el resultat de l’acció d'un individu que no ha pensat en les conseqüències o el resultat d'un procés automatitzat que no ha sabut gestionar els valors nuls. En qualsevol cas, si veus zeros en una sèrie de nombres, cal que et preguntis si aquests valors són realment nombres o si, pel contrari, signifiquen «res» (-1 també s'utilitza en aquest sentit). Si no s’està segur, consulta la font

Caldria tenir la mateixa precaució amb altres valors no numèrics on el 0 pot estar representat de diverses maneres. Per exemple, un fals valor per expressar la data s'acostuma a trobar com a «1970-01-01-01T00:00:00Z» o «1969-12-31T24:59:59ZZ», que és on comença el [registre temporal Unix o Unix epoch for timestamps](https://en.wikipedia.org/wiki/Unix_time#Encoding_time_as_a_number). ’altra banda, un fals 0 per a la localització es pot representar com a 0ª 00'00''N+ 0º 00' 00''E o simplement com a 0ºN 0ºE, que és el punt de l'Oceà Atlàntic just al sud de Ghana conegut com [Null Island](https://en.wikipedia.org/wiki/Null_Island).

Veure també:

* [Valors sospitosos](#valors-sospitosos)
* [El full de càlcul té les dates 1900, 1904, 1969 o 1970](#el-full-de-càlcul-té-les-dates-1900-1904-1969-o-1970)

### Manquen dades que hi haurien de ser

De vegades falten dades i no ho pots saber només amb el dataset. Però, tot i així, ho podràs esbrinar coneixent la temàtica de les dades. Per exemple, si tens un dataset que comprèn els Estats Units d'Amèrica, pots comprovar que els 50 estats hi siguin representats (sense oblidar els [territoris](https://en.wikipedia.org/wiki/Territories_of_the_United_States) — 50 no és un nombre correcte si s'hi inclou Puerto Rico). Si estàs treballant amb un dataset de jugadors de baseball, assegura't que tens el nombre d'equips que esperes i verifica que alguns jugadors que coneguis hi siguin representats. Confia en la teva intuïció si hi ha alguna cosa que sembla que falta i, si cal, torna a verificar-ho amb la font. L'univers de dades amb què treballes pot ser més petit del que creus.

### Files o valors duplicats

Si una mateixa fila apareix al teu dataset més d'una vegada, hauries de saber el perquè. De vegades, no cal que sigui una fila sencera. Per exemple, el finançament d'algunes campanyes inclou «correccions» que utilitzen els mateixos identificadors únics que la transacció original. Si no ho tens en compte, qualsevol càlcul que facis amb aquestes dades serà incorrecte. Si algun element sembla que hauria de ser únic, verifica que ho sigui i si descobreixes que no ho és, pregunta a la teva font per què.


### La ortografia és inconsistent

Els errors tipogràfics són un dels indicadors més clars per saber si les dades s'han recollit a mà. No et fixis només en els noms propis, que és un dels camps més difícils de veure. En lloc d’això, cerca inconsistències en els camps amb noms d'estats o ciutats («Los Angelos» és un error comú). Si trobes aquesta mena d’errades, pots estar bastant segur que les dades han sigut recollides o editades a mà i aquesta és una raó suficient per ser escèptics. Les dades recollides manualment tendeixen a contenir errors. Això no significa que no les puguis utilitzar però sí que hauries de corregir-los o tenir-los en compte com a errors en el teu article.

L'eina [OpenRefine's](http://openrefine.org/)  per [agrupar textos](https://github.com/OpenRefine/OpenRefine/wiki/Clustering) pot ajudar en el procés de correcció, suggerint coincidències entre valors inconsistents en una columna (per exemple relacionant `Los Angelos` amb `Los Angeles`).  Assegura't de documentar [documentar els canvis que facis](https://github.com/OpenRefine/OpenRefine/wiki/Exporters) de manera que puguis garantir [l'origen de les dades](#lorigen-de-les-dades-no-està-documentat)

Veure també:

* [Les dades han sigut introduïdes per humans](#les-dades-han-sigut-introduïdes-per-humans)


### L'ordre de les paraules és inconsistent

Les teves dades inclouen noms de l'Orient Mitjà o asiàtics? Estàs segur que els cognoms sempre estan al mateix lloc? És possible que algú del teu dataset utilitzi un [monònim](https://en.wikipedia.org/wiki/Indonesian_names#Indonesian_naming_system)? són el tipus d’errors que cometen habitualment els qui treballen amb dades. Si tens una llista de noms ètnicament diversos – de fet, qualsevol llista de noms – hauries de fer, com a mínim, una revisió abans d'assumir que les columnes «first_name» i «last_name» et donaran resultats adients per a la seva publicació.

Veure també:

* [Les dades han sigut introduïdes per humans](#les-dades-han-sigut-introduïdes-per-humans)


### Formats de dates inconsistents 

Quina data és setembre? :

* `10/9/15`
* `9/10/15`

Si la primera va ser escrita per un europeu i la segona per un nord-americà, [ambdues ho són](https://en.wikipedia.org/wiki/Date_format_by_country). Si no coneixes la història de les dades, no en podràs estar segur. Investiga d'on venen les dades i assegura't que van ser introduïdes per persones del mateix continent. 

Veure també:

* [Les dades han sigut introduïdes per humans](#les-dades-han-sigut-introduïdes-per-humans)
* [L'origen de les dades no està documentat](#lorigen-de-les-dades-no-està-documentat)


### Els formats dels decimals són inconsistents

Quin número és més gran? 

 * `1,000`
 * `1.000`
 
 Si la primera va ser escrita per un americà, la primera (un miler) que la segona (u); si va ser escrita per un europeu, el segon (un miler) és més gran que el primer (u). Tot i així, en general es parla de la [coma decimal](https://en.wikipedia.org/wiki/Decimal_mark) més que del punt.
 

### No s'especifiquen les unitats

Ni`pes` ni `cost` aporten cap informació sobre les unitats de mesura. No vulguis assumir massa ràpid que les dades produïdes als Estats Units s’expressaran en lliures o dòlars. Les dades científiques habitualment s’expressen mitjançant el sistema mètric decimal i, de la mateixa manera, alguns preus estrangers es poden expressar en la moneda local. Si les dades no expliciten les unitats, torna a la font i demana aquesta informació. Fins i tot si ho diu, hi ha unitats que han canviat el seu significat amb el temps.Un dòlar de 2010 no és un dolar avui, o una [tona curta](https://en.wikipedia.org/wiki/Short_ton) no és una [tona imperial](https://en.wikipedia.org/wiki/Long_ton) ni una [tona](https://en.wikipedia.org/wiki/Tonne).

Veure també:

* [Els noms dels camps són ambigus](#els-noms-dels-camps-són-ambigus)
* [La inflació distorsiona les dades](#la-inflació-distorsiona-les-dades)
* [Els símbols monetaris són insuficients](#els-símbols-monetaris-són-insuficients)

 
 ### Els símbols monetaris són insuficients

 Què és això: `$10`? Són deu dòlars, però de qui? Diversos països utilitzen [el mateix nom per a la seva moneda](https://en.wikipedia.org/wiki/Dollar_sign#Currencies_that_use_the_dollar_or_peso_sign). En alguns casos el simbol monetari pot tenir un prefix (per exemple, `A$10` per a deu dòlars australians), però datasets pensats per a distribucions locals habitualment el treuen.
 

### Les categories han estat mal seleccionades

Vigila amb els valors on només hi ha les respostes `verdader` or `fals`, però que en realitat no ho són. Això passa sovint amb les respostes d'enquestes on `rebutja contestar` o `sense resposta` són valors també vàlids – i significatius. Un altre cas comú és l'ús de la categoria `altres`. Si les categories en un dataset són un conjunt de països, què significa «altres»? Que la persona que va recollir les dades no sabia la resposta correcta? Que es troben en aigües internacionals? Que són expatriats? Refugiats?

Les males categories poden excloure dades artificialment. Això sol passar amb les estadístiques de crims. L'FBI ha definit la violació de diverses maneres al llarg del temps. De fet, han fet tan mala categorització intentant definir què és una violació que molts criminòlegs argumenten que les estadístiques no haurien de ser ni tan sols utilitzades. Una mala definició pot significar que un crim es compti en una categoria diferent de la que esperes o que simplement no sigui comptat.

Estigues especialment atent quan treballis amb temes on les definicions tendeixen a ser arbitràries, com és el cas de `raça` o `ètnia`.


### Els noms dels camps són ambigus

Què significa `residència`? El lloc on es viu o on es paguen els impostos? Una ciutat o una comarca? El noms dels camps mai són tan específics com haurien de ser, però és necessari tenir especial cura d’aquells que poden tenir dos o més significats. Fins i tot, si infereixes el significat de les dades, aquesta ambigüitat pot haver sigut causada per la persona que ha recol·lectat les dades en entrar malament el valor.


### L'origen de les dades no està documentat

Les dades són creades per una varietat d'individus i organitzacions: empreses, governs, ONGs i gent boja amb teories de la conspiració. Les dades es recullen de moltes maneres diferents, incloent enquestes, sensors i satèl·lits. A més a més, es poden escriure a ordinador o a mà (typed, tapped or scribbled). Conèixer l’origen de les dades et pot donar molta informació sobre les seves limitacions.

Les enquestes, per exemple, difícilment seran exhaustives. Els sensors difereixen en la seva precisió. D’altra banda, els governs no solen avenir-se a donar informació imparcial. Les dades en zones de guerra tenen un gran biaix geogràfic degut als perills de creuar fronts de batalla. Per si això fos poc, aquestes fonts normalment estan encadenades, és a dir, els analistes polítics distribueixen dades que han obtingut del govern. Les dades escrites per un doctor poden haver estat teclejades per un infermer. Cada baula de la cadena és una oportunitat per a l'error. En resum, sempre has de conèixer l'origen de les teves dades.

Veure també

* [No s'especifiquen les unitats](#no-sespecifiquen-les-unitats)


### Valors sospitosos

Si detectes algun d'aquests valors a les teves dades, tracta'ls amb molta cautela:

Nombres:

* [`65,535`](https://en.wikipedia.org/wiki/65535_%28number%29)
* [`255`](https://en.wikipedia.org/wiki/255_%28number%29)
* [`2,147,483,647`](https://en.wikipedia.org/wiki/2147483647_%28number%29)
* [`4,294,967,295`](https://en.wikipedia.org/wiki/4294967295)
* [`555-3485`](https://en.wikipedia.org/wiki/555_%28telephone_number%29)
* `99999` (o qualsevol altra seqüència llarga de 9s)
* `00000` (o qualsevol altra seqüència llarga de 0s)

Dates:

* [`1970-01-01T00:00:00Z`](https://en.wikipedia.org/wiki/Unix_time#Encoding_time_as_a_number)
* [`1969-12-31T23:59:59Z`](https://en.wikipedia.org/wiki/Unix_time#Encoding_time_as_a_number)
* [`January 1st, 1900`](#spreadsheet-has-dates-in-1900-1904-1969-or-1970)
* [`January 1st, 1904`](#spreadsheet-has-dates-in-1900-1904-1969-or-1970)

Geolocalització:

* [`0°00'00.0"N+0°00'00.0"E`](https://en.wikipedia.org/wiki/Null_Island) o simplement [`0°N 0°E`](https://en.wikipedia.org/wiki/Null_Island)
* US codi postal `12345` (Schenectady, New York)
* US codi postal `90210` (Beverly Hills, CA)

Cadascun d'aquests nombres dóna indicis de possibles errors, ja siguin entrats per humans o per ordinadors. Si els veus, assegura't que signifiquen allò que creus que signifiquen.

Veure també:

* [El full de càlcul té 65.536 files](#el-full-de-calcul-té-65.536-files)
* [El full de càlcul té 255 columnes](#el-full-de-calcul-té-255-columnes)
* [El full de càlcul té les dates 1900, 1904, 1969 o 1970](#el-full-de-càlcul-té-les-dates-1900-1904-1969-o-1970)


### Les dades són massa bastes

Tens estats i necessites municipis. Tens empresaris i necessites empleats. T'han donat anys, però vols mesos... en molts casos, ens trobem amb dades massa agrupades per als nostres propòsits.

Les dades difícilment es poden desagregar una vegada s'han barrejat. Si tens dades massa bastes, necessites demanar a la font quelcom més específic, però potser no ho tenen o no poden (o volen) donar-t'ho. Hi ha datasets federals que es poden accedir a nivell local per protegir la privacitat d'individus que podrien ser identificats per la seva unicitat (per exemple, l'únic Somalí que viu a l'oest de Texas). En aquests casos, l’única opció és preguntar.

El que no has de fer mai és dividir una dada anual entre 12 i anomenar-la «mitjana mensual». Sense conèixer la distribució dels valors, aquest nombre no tindrà validesa (potser tots els casos succeeixen en un mes o en una estació, o potser les dades segueixen una progressió exponencial i no una lineal). No ho facis, està malament.

Veure també:

* [Les dades són massa granuals](#les-dades-són-massa-granuals)
* [Les dades s'han agrupat en categories o geografies errònies](#les-dades-shan-agrupat-en-categories-o-geografies-errònies)


### Els totals difereixen dels globals publicats

Imagina que després d'una llarga lluita amb la FOIA (Freedom of Information Act) reps una llista «completa» dels casos de brutalitat policial. Quan l'obres descobreixes que té 2467 files i et disposes a publicar-ho... però no tan ràpid. Abans de publicar res del dataset, te n’adones que la darrera vegada que el cap de policia va declarar sobre el seu departament va ser fa sis setmanes i informava de «menys de 2000 casos». Per tant, el número no encaixa.

Aquestes discrepàncies entre les estadístiques publicades i les dades sense tractar són molt bons indicis de possibles errors. Habitualment les explicacions són simples. Per exemple, que les dades que t'han donat no són del mateix període... o de vegades han mentit. En qualsevol cas, assegura't que els números publicats coincideixen amb les dades totals que t'han donat.


### El full de càlcul té 65.536 files

El màxim de files que admetien les versions antigues de l'Excel eren 65.536. Si reps un dataset amb aquest nombre de columnes, pots estar gairebé segur que no t'han donat les dades completes; demana la resta. Les noves versions d'Excel admeten 1.048.576 files, així que és menys probable que et trobis amb dades que arribin a aquests límits.


### El full de càlcul té 255 columnes

L'aplicació d'Apple «Numbers» només admet 255 columnes i retalla les files que en tenen més sense avisar l'usuari. Si reps un dataset amb exactament 255 columnes, pregunta si alguna vegada el van obrir amb el «Numbers» i demana l'original.


### El full de càlcul té les dates 1900, 1904, 1969 o 1970

Per raons desconegudes, la data d'Excel per defecte a partir de la qual compta la resta és l'`1 de gener de 1900`, *excepte* si utilitzes l'Excel en un ordinador Mac, que és `l'1 de gener de 1904`. Hi ha multitud de maneres com les dades es poden entrar o calcular incorrectament en un Excel i acabar en una d'aquetes dates. Si te les hi trobes, es possible que es tracti d’una incidència.

Altres bases de dades i aplicacions generen la data `1970-01-01T00:00:00Z` o `1969-12-31T23:59:59Z`, que és l' [Unix epoch for timestamps](https://en.wikipedia.org/wiki/Unix_time#Encoding_time_as_a_number); en altres paraules, és el que succeeix quan un sistema intenta entrar un valor `0` o buit a un camp de data.


### El text s'ha convertit en nombres

No tots els numerals són nombres. Per exemple, els codis postals identifiquen geogràficament tots els llocs d'un país. Aquests codis tenen diferents longituds i són numèrics; per exemple, el 037 és el FIPS (Estàndard Federal de Processament de la Informació) referent al municipi de Los Angeles. No és el número `37`. Encara que el numeral `37` és un valor FIPS vàlid i correspon a Carolina del Nord. L'Excel i altres fulls de càlcul habitualment assumeixen que els numerals són números i esborren els zeros inicials, causant molts problemes a l'hora de migrar el format o fusionar-lo amb un altre dataset. Cal conèixer què ha succeït amb les dades en el seu recorregut i processament previs.


### Nombres que s'han desat com a text

Quan es treballa amb fulls de càlcul, els nombres es poden guardar en un format text de manera involuntària. Això passa habitualment quan un full de càlcul s'ha optimitzat per presentar dades en comptes de per fer-lo reutilitzable. Per exemple, en comptes d'escriure un milió de dòlars amb el nombre `1000000`, la cel·la pot contenir comes `1,000,000`, espais `1 000 000`, o text `USD 1,000,000`. L'Excel pot fer canvis en el casos simples mitjançant funcions, però en molts casos caldrà netejar les cel·les perquè es reconeguin els nombres. Una bona pràctica és guardar els números sense format i després incloure informació de suport en el nom de la columna o en les metadades.

## Aspectes que tu pots resoldre


### El text està codificat

Les lletres es representen com si fossin nombres. Els problemes amb la codificació apareixen quan un text es representa amb un grup específic de nombres desconegut (anomenat «encoding» o codificació). Això origina un fenomen anomenat [mojibake](https://en.wikipedia.org/wiki/Mojibake), que provoca que el text de les teves dades aparegui com si fos brossa o d’aquesta manera: ���.

En la gran majoria de casos, el teu editor de textos o full de càlcul detectarà quina és la codificació correcta, tot i que si no funciona, podries cometre l'error de publicar el nom d'algú amb algun caràcter estrany al mig. La teva font ha de ser capaç d'indicar-te la codificació de les seves dades i, en cas contrari, hi ha maneres bastant fiables d'esbrinar-la (consulta un programador).


### Els espais al final de la línia estan mal codificats

Els arxius amb text i dades, com és el cas dels .csv, utilitzen caràcters invisibles per representar una nova línia. Windows, Mac i Linux han tingut un desacord històric sobre quins haurien de ser aquests caràcters. Intentar obrir un fitxer en un programa guardat en un altre sistema operatiu provoca que l’Excel o altres aplicacions puguin fallar a l'hora d’identificar aquests salts de línia.

Normalment, es resol fàcilment obrint el fitxer en un editor de text genèric i guardant-lo a continuació. Si l'arxiu és excepcionalment gran hauries de considerar utilitzar una eina amb línia de comandaments o buscar l’ajuda d'un programador. Pots llegir més sobre aquesta qüestió aquí: [aquí](https://nicercode.github.io/blog/2013-04-30-excel-and-line-endings/).


### Les dades estan en PDF

Una gran quantitat de dades – especialment governamentals – només està disponible en format PDF. Si les vols recuperar, hi ha diverses opcions per extreure-les (quan provenen de [documents escanejats](#les-dades-es-troben-en-documents-escanejats), el problema és un altre). Una bona eina és [Tabula](http://tabula.technology/). De qualsevol manera, amb l'Adobe Creative Cloud es té accés a l'Acrobat Pro, que incorpora una eina per exportar taules de PDF a Excel.

Veure també

* [Les dades es troben en documents escanejats](#les-dades-es-troben-en-documents-escanejats)


### Les dades són massa granulars

És el cas oposat a tenir les [dades massa bastes](#les-dades-són-massa-bastes). És a dir, tens municipis i vols estats, o tens mesos però vols anys. Per sort, això és molt més fàcil de resoldre.

Les dades poden agregar-se utilitzant taules dinàmiques d'Excel o Google Docs, utilitzant una base de dades SQL o amb un codi personalitzat. Les taules dinàmiques són una gran eina, però tenen els seus límits. Per a volums excepcionalment grans o per agregar dades en grups inusuals, hauries de preguntar a un programador, ells poden trobar una solució que sigui senzilla i fàcil de verificar i reutilitzar.

Veure també 
* [Les dades són massa bastes](#les-dades-són-massa-bastes)
* [Les dades s'han agrupat en categories o geografies errònies](#les-dades-shan-agrupat-en-categories-o-geografies-errònies)


### Les dades han sigut introduïdes per humans

Les dades introduïdes per humans són un problema habitual i els seus símptomes són, com a mínim, 10 dels problemes que ja hem descrit. No hi ha un millor manera d’arruïnar dades que deixar que una única persona les capturi sense passar per cap validació. Per exemple, una vegada vaig adquirir una base de dades completa de llicències per a gossos del Comtat de Cook, Illinois. En comptes de demanar als propietaris que escollissin una raça de la llista per registrar els seus gossos, els creadors de la base els van donar un espai de text per escriure-la. El resultat va ser que aquesta base de dades tenia escrita la paraula Chihuahua com a mínim de 250 maneres diferents. Fins i tot amb les millors eines, aquesta mena de dades no es poden arreglar i, per tant, no aportaran valor. Això no és tan important en el cas de dades de gossos, però no voldràs que passi amb soldats ferits o cotitzacions. Cal anar amb precaució amb les dades introduïdes per humans.

### Les dades estan barrejades amb formats i anotacions

Representacions complexes de dades com HTML o XML permeten una clara separació entre les dades i el format, però no és el cas de les representacions de dades tabulars comuns, com és el cas dels fulls de càlcul. Tot i així, alguns intenten fer-ho. Problemes comuns amb les dades dels fulls de càlcul és que les primeres files són descripcions o notes sobre les dades, més que no pas el títol de la columna o les pròpies dades. Així mateix, una clau o diccionari de dades també es pot trobar a mitja pàgina; els encapçalaments es poden anar repetint; o la fulla de càlcul pot tenir múltiples taules (amb diferents encapçalaments per columna) una darrera l’altra en comptes d'estar separades en diferents fulls.

En tots aquests casos, la solució passa per identificar el problema. Òbviament, qualsevol anàlisi que parteixi de fulls de càlcul amb aquests problemes fallarà, i de vegades per raons que no són tan evidents. Quan llegeixis noves dades per primera vegada, sempre és bona idea assegurar-te que no hi ha files extra d'encapçalaments o altres caràcters de format inserits entre les dades.


### Les agregacions es calculen amb valors que falten
Imagina un dataset amb 100 files i una columna anomenada `cost`. En 50 de les columnes, el valor «cost» està en blanc. Quina és la mitjana d'aquesta columna? És la `suma_del_cost/50` o `suma_del_cost/100`? No hi ha una resposta definitiva. En general, si calcules els agregats en columnes amb dades que falten, pots fer-ho deixant fora les columnes sense dades, però en aquests casos cal anar alerta amb fer comparacions entre columnes! En alguns casos, aquests valors que falten poden estar correctament interpretats com 0. Si no estàs segur, pregunta a un expert o no ho facis.
Aquest és un error que pots cometre en la teva anàlisi, però també es un error que altres poden cometre i passar-te’n els resultats, així que estigues alerta quan les teves dades ja venen calculades.

See also:

* [Manquen dades que hi haurien de ser](#manquen-dades-que-hi-haurien-de-ser)
* [Les dades en blanc es reemplacen per zeros](#les-dades-en-blanc-es-reemplacen-per-zeros)


### La mostra no és aleatòria

Un error de mostreig no aleatori succeeix quan una enquesta o dataset no representa tot el conjunt de la població, ja sigui de manera intencionada o accidental. Això pot passar per moltes raons, que van des de l'hora del dia a la llengua nativa de l'enquestat, i solen ser font d'errors a les investigacions sociològiques. També pot passar per raons menys òbvies, com quan un investigador creu que té una base de dades completa i escull treballar només amb una part. Si el dataset original estigués incomplet per alguna raó, les conclusions que se n’extraguessin serien incorrectes. L'únic que es pot fer per evitar aquests errors és evitar les mostres no aleatòries. 

Veure també

* [La mostra està esbiaixada](#la-mostra-està-esbiaixada)


### El marge d'error és massa ampli

El problema que causa més errors d'informació és l’ús irreflexiu de nombres amb marges d'error massa amplis (MOE, per les sigles en anglès de margins-of-error). El MOE s'associa normalment amb dades que provenen d'enquestes. Un lloc habitual on se sol trobar és quan s'utilitzen les dades d'intenció de vot o les dades de l'[American Community Survey](https://www.census.gov/programs-surveys/acs/) de la Oficina del Cens d'Estats Units. El MOE és la mesura dels rangs dels possibles valors certs. Es pot expressar com a número (`400 +/- 80`) o com a percentatge del total (`400 +/- 20%`). Com més petita sigui la població en qüestió, més gran serà el MOE. Per exemple, segons les estimacions de l'ACS de 2014, en un període de 5 anys el nombre d'asiàtics vivint a Nova York és de `1,106,989 +/- 3,526` (0.3%); el nombre de filipins és de `71,969 +/- 3,088` (4.3%) El nombre de samoans de `203 +/- 144` (71%).

Els dos primers nombres es poden publicar amb seguretat. El tercer nombre mai s’hauria d'utilitzar. No hi ha una regla específica que indiqui quan un nombre no és suficientment precís però, per regla general, s'hauria d'anar amb precaució utilitzant qualsevol dada amb un MOE per sobre del 10%.

See also:

* [Es desconeix el marge d'error](#es-desconeix-el-marge-derror)


### Es desconeix el marge d'error

De vegades el problema no és que el marge d'error sigui [massa gran](#el-marge-d-error-és-massa-ampli), sinó que ningú s’hagi molestat a comprovar-ho. Aquest és un problema amb les enquestes no científiques. Sense calcular un MOE, és impossible saber amb exactitud la fiabilitat dels resultats. Com a regla general, sempre que tinguis dades d'enquestes hauries de preguntar quin és el seu MOE. Si la font no t'ho pot dir, probablement les dades no siguin vàlides per utilitzar-les una anàlisi seriosa.

Veure també

* [El marge d'error és massa ampli](#el-marge-derror-és-massa-ampli)


### La mostra està esbiaixada

Com quan la mostra [no es aleatòria](#la-mostra-no-és-aleatòria), una mostra esbiaixada és el resultat de la falta de cura en la realització del mostreig, tot i que també es pot donar el cas que sigui enganyosa intencionadament. Una mostra pot estar esbiaixada perquè es va realitzar via Internet i hi ha una part desfavorida de la població que no hi té accés de manera tan freqüent. Les enquestes han de poder de cobrir segments proporcionats de qualsevol població que pugui esbiaixar els resultats. És casi impossible fer-ho a la perfecció, de manera que se sol fer malament.

Veure també:

* [La mostra no és aleatòria](#la-mostra-no-és-aleatoria)


### Les dades s'han editat manualment

L'edició manual té els mateixos problemes que [les dades introduïdes per humans](#les-dades-han-sigut-introduides-per-humans), excepte que succeeix a posteriori. De fet, les dades editades manualment solen ser un intent d'arreglar les dades que originalment es van capturar manualment. Els problemes apareixen quan la persona que els està editant no té un coneixement total de les dades originals. Una vegada vaig veure algú «corregint» un nom a una base de dades (`Smit` per `Smith`). Realment el nom de la persona era Smith? No ho sé, però el que sí sé és que ara aquest valor és un problema. Si no es registra el canvi, és impossible verificar quin dels dos hauria de ser.


Aquests problemes amb l’edició manual és una de les raons per les quals hauries d'assegurar-te que [l'origen de les dades està ben documentat](#l-origen-de-les-dades-no-esta-documentat). En cas contrari, pot ser un bon indici que algú hi ha estat jugant. Habitualment, acadèmics i analistes polítics obtenen les dades del govern, les modifiquen i després les distribueixen entre els periodistes. Sense accedir al registre de canvis és impossible saber si van ser justificats. Sempre que sigui possible, intenta accedir a la *font primària* o, com a mínim, a la versió més antiga possible i fes la teva anàlisi a partir d'aquesta.

Veure també:

* [Les dades han sigut introduïdes per humans](#les-dades-han-sigut-introduïdes-per-humans)
* [L'origen de les dades no està documentat](#lorigen-de-les-dades-no-està-documentat)



## La inflació distorsiona les dades
La inflació monetària significa que amb el temps el valor dels diners canvia. No hi ha manera de saber si els números s'han ajustat a la inflació només mirant-los. Si obtens dades i no estàs segur de si s'han ajustat als efectes de la inflació, verifica-ho amb la font. Si no s'han ajustat, segurament ho voldràs fer tu mateix. Hi ha recursos per fer-ho, com ara aquest ajustador de [la inflació](http://inflation-adjust.herokuapp.com/)

Veure també:

* [Variacions naturals/de temporada distorsionen dades](#variacions-naturalsde-temporada-distorsionen-les-dades)


## Variacions naturals/de temporada distorsionen les dades

Molts tipus de dades fluctuen naturalment per raó d’algunes forces subjacents. L'exemple més conegut són les variacions en les dades d'ocupació i atur, que fluctuen al llarg de l'any. Els economistes han desenvolupat mètodes per compensar aquesta variació. Els detalls dels mètodes no són particularment importants, però és important esbrinar si s'han ajustat o no les dades. Si no s’ha fet i vols comparar les dades d'ocupació mes a mes, segurament caldrà que la font t’envií les dades ajustades (ajustar-les tu mateix és més complex que ajustar la inflació).

Veure també:

* [La inflació distorsiona les dades](#la-inflació-distorsiona-les-dades)


## El marc temporal ha estat manipulat

La font pot distorsionar la visió del món de manera intencionada o accidental si dóna les dades que comencen o acaben en un determinat lapse de temps. Per exemple, la «onada de crim nacional» àmpliament reportada al 2015. No hi va haver cap «onada de crim». El que es va produir van ser una sèrie d’increments puntuals a ciutats determinades en comparació amb els anys anteriors. Si els periodistes haguessin examinat un marc temporal més ampli, haurien descobert que els crims violents van ser més nombrosos deu anys enrere pràcticament a qualsevol lloc d'Estats Units i que vint anys abans eren quasi el doble.

Si les dades que tens cobreixen un marc temporal limitat, evita començar els càlculs amb el primer període de dades. Si comences uns anys (o mesos, o dies) després de la data inicial, pots tenir la seguretat que no estàs fent una comparació que s’invalidaria amb un únic punt de dades addicional.

Veure també:

* [El marc de referència ha estat manipulat](#el-marc-de-referència-ha-estat-manipulat)


## El marc de referència ha estat manipulat

Les estadístiques de crim es manipulen habitualment per raons polítiques, comparant-les amb un any que les xifres van ser altes. Això es pot expressar tant com a canvi (disminució d'un `60%` des del 2004) o com a índex (`40`, on 2004=100). En qualsevol dels dos casos, 2014 pot ser o no un any adequat per a les comparatives, ja que pot haver estat un any amb una taxa inhabitualment alta de crims.
El mateix cas es pot donar quan es comparen localitzacions. Si es vol fer quedar malament un país, simplement s'expressen les dades relativitzant-les amb altres nacions amb millors resultats.
El problema acostuma a arrelar en individus que ja tenen un fort prejudici de confirmació («tal com pensava, el crim ha augmentat!»). Quan sigui possible, compara ràtios a partir de diferents punts de partida per veure com canvien les xifres. I, sobretot, *no utilitzis aquesta tècnica per ressaltar un argument que creguis que és important*. És inexcusable.
Problemes que requereixen de l’ajuda d’un expert per resoldre'ls

Veure també:

* [El marc temporal ha estat manipulat](#el-marc-temporal-ha-estat-manipulat)


## Problemes que requereixen de l'ajuda d'un expert per resoldre'ls

### L'autor no és de confiança

De vegades les úniques dades que tenim provenen d'una font de la qual preferiries no dependre. En alguns casos, això no suposa cap problema. Les úniques persones que saben quantes armes es fabriquen són els qui les fan. Tot i així, si es tenen dades qüestionables, sempre verifica-les amb algun expert. Millor encara si ho verifiques amb dos o tres. No s'han de publicar dades d'una font esbiaixada a menys que es disposi d’evidències substancials que la corroborin.


### El procés de captura és opac

És molt senzill que s'introdueixin falses suposicions, errors o grans falsedats en el procés de recol·lecció de dades. Per aquesta raó, és important que el mètode utilitzat sigui transparent. Serà difícil esbrinar exactament com es van recollir les dades però, tanmateix, existeixen elements que funcionen com a indicadors de problemes. Per exemple, quan les xifres incloses [són d'una precisió irreal](#les-dades-són-d-una-precisio-irreal) o quan les dades [són massa bones per ser veritat](#és-massa-bonic-per-ser-veritat)

De vegades l'origen de les dades pot ser simplement sospitós: realment els acadèmics x i y van entrevistar 50 membres actius de les bandes de la zona sud de Chicago? Si la manera que les dades van ser recol·lectades sembla qüestionable i la font no pot oferir [proves fefaents del seu origen](#l-origen-de-les-dades-no-està-documentat), caldria verificar sempre amb un altre expert per veure si realment és possible que les dades s’hagin recollit de la manera que es descriu.

Veure també:

* [L'origen de les dades no està documentat](#l-origen-de-les-dades-no-està-documentat)
* [Les dades són d'una precisió irreal](#les-dades-són-duna-precisio-irreal)
* [És massa bonic per ser veritat](#és-massa-bonic-per-ser-veritat)


### Hi ha valors atípics inexplicables

Recentment vaig crear un dataset del temps que triguen a arribar diferents missatges a diferents destinacions a través d'internet. Tots els temps se situaven en un rang dels `0,05`als `0,8` segons, excepte tres d'ells. Aquests estaven per sobre dels `5.000` segons. Això és senyal que quelcom no funcionava en la producció de les dades. En aquest cas particular, un error en el codi va provocar errades en el comptatge, mentre que la resta de missatges s'anaven enviant i rebent amb normalitat.

Aquesta mena d’errors atípics poden arruïnar dramàticament les estadístiques – especialment si s'utilitza una mitjana (probablement s'haurien d’utilitzar medianes). Quan es té un nou data set, és una bona idea mirar quins són els valors majors i menors per assegurar-nos que es troben en un rang raonable. Si la dada ho justifica i es vol fer una estadística més rigorosa, es pot utilitzar la [desviació estàndard](https://en.wikipedia.org/wiki/Standard_deviation) o la [desviació mitjana](https://en.wikipedia.org/wiki/Median_absolute_deviation) 

Un benefici addicional que comporta la detecció de valors atípics és que acostumen a ser una bona manera de trobar grans titulars. Si realment hi hagués un país que triga 5.000 vegades més a enviar un missatge per internet, seria una gran història.


### Un índex emmascara variacions subjacents

Els analistes que volen estudiar tendències generen amb freqüència índexs amb diversos valors per monitoritzar el seu progrés. Utilitzar-los no és intrínsecament incorrecte, però cal ser cautelós amb els índexs que associen mesures dispars.

Per exemple, l'[Índex de desigualtat de gènere de les Nacions Unides](http://hdr.undp.org/en/content/gender-inequality-index-gii) (GII) combina diferents mesures relacionades amb el progrés de les dones cap a la igualtat. Una d'elles és l'índex de la «representació de dones al Parlament». Dos països que tenen lleis vinculants pel que fa a la representació paritària de gènere als parlaments són Pakistan i la Xina i, en conseqüència, aquests països tenen un millor resultat a l'índex que altres països que tenen condicions similars en la resta de paràmetres. És just? Realment no importa, perquè la qüestió és que confon a qui desconegui aquest factor. El GII i índexs similars sempre s’haurien d'utilitzar mitjançant una anàlisi acurada per assegurar-nos que les seves variables subjacents no esbiaixen l'índex de maneres inesperades.


### Hi ha p-hacking als resultats 

P-hacking significa l’alteració de les dades de manera intencionada, canviant una anàlisi estadística, o reportant els resultats selectivament amb l'objectiu d’obtenir conclusions significatives. Aquesta pràctica inclou, entre d’altres, deixar de recollir dades una vegada s'ha assolit un resultat significatiu, obviar observacions, o realitzar moltes anàlisis però publicar només aquelles que donen resultats significatius. Hi ha bons [estudis](http://fivethirtyeight.com/features/science-isnt-broken) que tracten aquesta qüestió.

En cas de voler publicar els resultats d'un estudi, cal comprendre què són els «valors p», què signifiquen i després decidir demanera argumentada si els resultats tenen valor. Es publiquen moltes estudis brossa perquè els periodistes no entenen què són els «valors p».

Veure també

* [El marge d'error és massa ampli](#el-marge-derror-és-massa-ampli)


### La llei de Benford falla

La [llei Benford](https://en.wikipedia.org/wiki/Benford's_law) és una teoria segons la qual els dígits menors (1, 2, 3...) apareixen molt més sovint que dígits majors (7, 8, 9). En teoria, la Llei de Bendord es pot utilitzar per detectar anomalies en pràctiques comptables o resultats electorals. A la pràctica, però, no és tan fàcil d’aplicar. Si hi ha sospites que un dataset s'ha creat o modificat amb intencions fraudulentes, la llei de Benford és un molt bon primer test, però sempre caldrà que un expert en verifiqui els resultats abans de concloure que han estat manipulats.


### És massa bonic per ser veritat

No hi ha un dataset global de l’opinió pública. Ningú coneix el nombre exacte d’habitants de Sibèria. Les estadístiques de criminalitat no són comparables entre fronteres. El govern dels Estat Units mai ens dirà la quantitat de material fissible es guarda a la màniga.
Alerta amb les dades que ens pretenen mostrar quelcom que no és pot conèixer. No són dades. Són les estimacions d'algú i probablement siguin errònies. Repeteixo... pot ser una bona història... però requereix una mirada experta.


## Problemes que un programador pot ajudar a resoldre

### Les dades s'han agrupat en categories o geografies errònies

De vegades les dades presenten el nivell de detall correcte (ni massa [genèric](#les-dades-són-massa-bastes) ni massa [específic](#les-dades-són-massa-granulars), però s'han agregat en agrupacions que no són les desitjades. Un exemple clàssic són les dades agrupades per codi postal que preferiries tenir per barris o districtes. En molts casos, és un problema impossible de resoldre si no es disposa d’accés a les dades específiques, però, en canvi, de vegades les dades es poden separar proporcionalment entre els grups.

Aquesta opció cal executar-la amb cura, entenent [el marge d'error](#el-marge-derror-és-massa-ampli) que es pot introduir durant el procés. Si les dades es troben agregades en grups erronis, demana al programador o a la font si és possible reagrupar-les d’una altra manera.

Veure també:

* [Les dades són massa bastes](#les-dades-són-massa-bastes)
* [Les dades són massa granulars](#les-dades-són-massa-granulars)
* [El marge d'error és massa ampli](#el-marge-derror-és-massa-ampli)


### Les dades es troben en documents escanejats

Gràcies a les lleis FOIA és freqüent el cas d'administracions que estan obligades a facilitar dades –malgrat que realment no vulguin fer-ho. En aquests casos, és una estratègia habitual que les publiquin en documents escanejats o fotografies. De fet, les podem trobar en fitxers d'imatge o, més sovint, transformades en un arxiu pdf.

És possible extreure text des d’arxius d’imatge i convertir-lo en dades; es fa mitjançant un procés de reconeixement òptic de caràcters (anomenat OCR). Els sistemes moderns d'OCR tenen una precisió de gairebé el 100%, però dependrà molt de la naturalesa del document. Sempre que s'utilitzi un OCR per extreure dades és recomanable dur a terme un procés de validació per verificar que els resultats coincideixen amb l'original.

Hi ha webs on es pot pujar un document per passar l'OCR, però també es poden trobar eines gratuïtes que un programador pot adaptar per a un tipus específic de document. Consulta quina és la millor estratègia per als teus documents.

Veure també

* [Les dades estan en PDF](#les-dades-estan-en-pdf)

