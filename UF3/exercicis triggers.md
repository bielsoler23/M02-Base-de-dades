# EXERCICIS TRIGGERS (Part 1)

Donada la base de dades de RRHH proporcionada pel professor realitza els següents exercicis

## Exercici 1
Omplir la següent taula indicant en cada cas si es pot accedir als registres NEW i OLD des del trigger corresponent i, en cas afirmatiu, quin tipus d'operació és pot realitzar (L(llegir) o M(modificar)).

|      | INSERT before | INSERT after | DELETE before | DELETE after | UPDATE before | UPDATE after |
|------|---------------|--------------|---------------|--------------|---------------|--------------|
| NEW  |               |              |               |              |               |              |
| OLD  |               |              |               |              |               |              |

## Exercici 2
A quina taula o taules de la base de dades INFORMATION_SCHEMA de MySQL es poden consultar els triggers que hi ha a la base dades?

## Exercici 3: Auditoria de la taula "empleats"
Crea el que creguis necessari per auditar la taula d’empleats. Aquesta auditoria pretén dur un control automàtic dels canvis (INSERT, UPDATE, DELETE) que es realitzen en aquesta taula.

Si no la tens crea una taula anomenada auditoria_taula amb els següents camps:

| Camp    | Tipus         | Descripció |
|---------|---------------|------------|
| usuari  | VARCHAR(100)  | Usuari del sistema que ha realitzat l’acció |
| data    | DATETIME      | Data i hora que s’ha realitzat l’acció |
| taula   | VARCHAR(64)   | Taula sobre la que es realitza l’acció |
| accio   | VARCHAR(20)   | "ELIMINAR", "AFEGIR", "MODIFICAR" |
| valors  | VARCHAR(250)  | Valor que identifica el registre que ha patit l’acció. Si l’acció és "MODIFICAR" cal guardar els valors antics. Si l’acció és "ELIMINAR" o "AFEGIR" només cal guardar el valor de la PK |

## Exercici 4: Validació de dades d’entrada
Mitjançant triggers volem dur el control de dades d’entrada d’una taula. Concretament volem dur el control del camp salari de la taula empleats. 
Aquest salari ha de ser un valor dins del rang marcat pels camps salari_min i salari_max de la taula feines. 

En definitiva, volem controlar que el salari dels empleats estigui dins dels rangs de salaris marcats per el tipus de feina que fa l’empleat.
## Exercici 5: Manteniment del camp num_empleats
Afegeix un el camp num_empleats a la taula departaments. Aquest camp simbolitza/modela el número d’empleats que té aquell departament. 

Implementa mitjançant triggers el manteniment d’aquest camp de manera automàtica.

Per exemple si s’afegeix un nou empleat del departament amb codi 10 cal augmentar en 1 aquest camp del departament_id = 10

## Exercici 6: Manteniment de l’historial de feines
Implementa el que creguis necessari per mantenir la taula historial_feines de forma automàtica. És dir, quan es s’afegeix o es modifica la feina d’un empleat, cal registrar aquest canvi a la taula historial_feines. 

Cal tenir en compte que si l’empleat canvia de departament no cal registrar-ho a la taula historial_feines. 

La data_inici i data_fi han d’anar en consonància a les dates del canvi de feina.

# EXERCICIS TRIGGERS (Part 2)

Crea la base de dades botiga a partir del seu model relacional. Un cop hagis creat la BD de botiga implementa amb triggers les peticions que es demanen a continuació.

## CLIENT
(nif, nom, cognoms, data_naix, adreça, telefon)

| Domini | Restriccions |
| ------ | ------------ |
| nif: 8 números i 1 lletra | NN: nom |
| nom: 30 lletres | |
| data_naix: data | |
| adreça: 20 lletres | |
| telefon: 12 caracters | |
| edat: nombre de 1-150 | |

## COMERCIAL
(nif, nom, dataNaix, telefon, email)

| Domini | Restriccions |
| ------ | ------------ |
| nif: 8 números i 1 lletra | NN: nom |
| nom: 30 lletres | |
| dataNaix: data | Observacions: |
| telefon: 12 caracters | |
| email: 40 caracters | Les comissions és un valor que conté l'import de comissió que ha cobrat el comercial per les seves factures cobrades. |
| comissions: 10 números (2 decimals) | |

## FACTURA
(numFactura, dataFactura, baseImponible, tipusIva, totalIva, totalFactura, formaPagament, observacions, comissió, dniClient, dniComercial, totalPagat, dataCobrament)

| Domini | Restriccions |
| ------ | ------------ |
| numFactura: 7 números | NN: dataFactura, totalFactura |
| dataFactura: data | FK: nifClient --> CLIENT (nif) |
| baseImponible: 10 números (2 decimals) | FK: nifComercial --> COMERCIAL (nif) |
| tipusIva: 2 números | CK: tipusIva ha de ser 4, 8 o 18. |
| totalIva: 10 números (2 decimals) | Observacions: |
| totalFactura: 10 números (2 decimals) | La forma de pagament habitual és ‘Efectiu’ |
| formaPagament: 30 lletres | La comissió és un tant per 1 indicant quin és el % que s'emporta el comercial si es cobra tota la factura |
| observacions: 100 lletres | |
| comissió: 4 números (2 decimals) | |
| nifClient: 8 números i 1 lletra | |
| nifComercial: 8 números i 1 lletra | |
| totalPagat: 10 números (2 decimals) | |
| dataCobrament: data | |

## LINIAFACTURA
(numFactura, numLinia, quantitat, idArticle, descripcio, preuU, dte, totalLinia)

| Domini | Restriccions |
| ------ | ------------ |
| numFactura: 7 números | NN: descripcio |
| numLinia: 9 números | FK: (numFactura) --> FACTURA (numFactura) |
| quantitat: 6 números (2 decimals) | FK: (idArticle) --> ARTICLE (idArticle) |
| idArticle: 10 lletres | CK: preuU >= 0 |
| descripcio: 30 lletres | CK: dte >= 0 |
| preuU: 8 números (2 decimals) | |
| dte: 4 números (2 decimals) | |
| totalLinia: 10 números (2 decimals) | |

## ARTICLES
(idArticle, descripcio, preuU, quantitat, estoc_min, estoc_demanar, estoc_pendent)

| Domini | Restriccions |
| ------ | ------------ |
| idArticle: 10 lletres | NN: descripcio, preuU |
| descripcio: 30 lletres | CK: preuU > 0 |
| preuU: 8 números (2 decimals) | |
| quantitat: 6 números (2 decimals) | |
| estoc_min: 6 números (2 decimals) | |
| estoc_demanar: 6 números (2 decimals) | |
| estoc_pendent: 6 números (2 decimals) | |

## REBUT
(numRebut, dataRebut, numFactura, import)

| Domini | Restriccions |
| ------ | ------------ |
| numRebut: 7 números | NN: numFactura, import |
| dataRebut: data | FK: numFactura --> FACTURA (numFactura) |
| numFactura: 7 números | |
| import: 10 números (2 decimals) | |

## RESUM_VENDES
(nifComercial, any, mes, totalFactures, totalImport)

| Domini | Restriccions |
| ------ | ------------ |
| nifComercial: 8 números i 1 lletra | FK: nifComercial --> COMERCIAL (nif) |
| any: Any expressat en 4 dígits | |
| mes: 2 dígits | |
| totalFactures: 4 dígits | |
| totalImport: 15 números (2 decimals) | |

### Implementa els següents triggers:
- Cada vegada que es modifica un client i aquest li canviem la data_naix, cal actualitzar el camp edat.
- Cada vegada que s'afegeix, es modifica o s'esborra una línia de factura, que calculi el totalLinia i actualitzi de la taula factura els camps de baseImponible, totalIva, totalFactura.
- Cada vegada que s'afegeix, es modifica o s'esborra una línia de factura, actualitzi l'estoc disponible (quantitat) de la taula articles. L'estoc no pot quedar MAI en negatiu. Si s'intenta vendre més quantitat que la disponible, ha de cancel·lar l'operació.
- Modificar el trigger anterior perquè si després de fer una operació a la taula articles, aquest article queda amb una quantitat inferior a l'estoc mínim, s'ompli la casella d'estoc_demanar amb un valor del doble de l'estoc mínim. Nota: Si ja tenim un valor a estoc_demanar, no cal tornar a preparar una altra comanda.
- Crear un trigger perquè cada vegada que es cobri un rebut, s'actualitzi la informació de l'import pagat a la factura i s'actualitzi també les comissions del comercial.
- Es vol mantenir la taula de RESUM_VENDES de forma automàtica mitjançant triggers. Crea el/s trigger/s necessaris per tal de realitzar aquest manteniment automàtic.

