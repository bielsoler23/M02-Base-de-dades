**Exercici 0 – Importació de la BD** 

Importa els fitxers .json per la BD de rrhh proporcionada per el professor [(https://github.com/robertventura/databases/blob/master/mongodb/rrhh/)](https://github.com/robertventura/databases/blob/master/mongodb/rrhh/) 

Passos: 

- Crea la BD rrhh** 
- Importa el fitxer departaments.json à col·lecció departaments** 
- Importa el fitxer empleats.json à col·lecció empleats** 

**Exercicis $group** 

1. Mostra la quantitat d’empleats per cada departament. Mostra id de departament i la quantitat.
```sql
```
2. Si no ho has tingut en compte en l’exercici anterior. Només tingues en compte aquells empleats que estiguin en un departament.
```sql
```
3. Ordena el resultat anterior per els departament de més a menys nombre d’empleats.
```sql
```
4. De cada departament mostra el salari més alt. Mostra id de departament i el salari més alt.
```sql
```
5. Quina és la massa salarial de cada departament? Mostra id de departament i la massa salarial.
```sql
```
6. Només mostra aquells departaments que tinguin una massa salarial igual o superior a 19000
```sql
```

**Exercicis** 

7. Redefineix el camp “historial\_feines” perquè tingui el número de feines i no el detall de les feines que ha tingut cada empleat. Si l’empleat no ha tingut cap treure el camp “historial\_feines”. 
7. Com que tot empleat té una feina incorpora la feina actual com una feina més. 
7. Mostra aquells empleats que han tingut 2 feines o més. 

10. Per cada empleat mostra les dades del seu departament. Redefineix el mateix camp departament del document empleats. 
10. Si has utilitzat $join a l’exercici anterior veuràs que el camp departament és un array. Per tant fés el que necessitis perquè aquest camp sigui un objecte a on hi hagi la informació del departament i no un array.
