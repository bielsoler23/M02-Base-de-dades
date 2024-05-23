# CONSULTES AMB FUNCIONS
El professor us ha proporcionat una sèrie de BD dins de MongoDB

Indica quines són les consultes amb mongoDB que responen a lespreguntes següents:

## Base de dades edx – col·lecció students

### Exercici 1
```sql
db.students.find({gender: 'H'})
```

### Exercici 2
```sql
db.students.find({gender: 'M'}).count()
db.students.count({gender: 'M'})
```
### Exercici 3
```sql
db.students.find({birth_year: 1993})
```

### Exercici 4
```sql
db.students.find({$and: [ {birth_year: 1993}, {gender: 'H' } ] })
db.students.find({birth_year: 1993, gender: 'H'})
```

### Exercici 5
```sql
db.students.find({birth_year: {$gt:1990}})
```

### Exercici 6
```sql
db.students.find({birth_year: {$lte:1990}})
```

### Exercici 7
```sql
db.students.find({birth_year: { $gte: 1990, $lte: 1999 }})
```

### Exercici 8
```sql
db.students.find({$and: [ {birth_year: {$gte: 1990}}, {birth_year: {$lte: 1999}} ] })
```

### Exercici 9
```sql
db.students.find({$and: [ {gender: 'M'}, {$and: [ {birth_year: {$gte: 1990}}, {birth_year: {$lte: 1999}} ] } ] } )
```

### Exercici 10
```sql
db.students.find({$and: [ {birth_year: { $gte: 1990, $lte: 1999 }}, {gender: 'M' } ] } )
```

### Exercici 11
```sql
db.students.find({birth_year: {$ne: 1985 } } )
```

### Exercici 12
```sql
db.students.find({$or: [ {birth_year:1970}, {birth_year: 1980},{birth_year: 1990} ] } )
```

### Exercici 13
```sql
db.students.find({ "birth_year": { $mod: [2, 0] } })
```

### Exercici 14
```sql
db.students.find({ "phone_aux": { "$exists": true } })
```

### Exercici 15
```sql
db.students.find({ "lastname2": { "$exists": false } })
```

### Exercici 16
```sql
db.students.find({ "phone_aux": { "$exists": true },
 "lastname1": { "$exists": true },                  
 "lastname2": { "$exists": false }
 })
 ```

### Exercici 17
```sql
db.students.find({email:/\.net$/})
```
 
### Exercici 18
```sql
db.students.find({phone:/^622/})
```

### Exercici 19
```sql
db.students.find({dni:/^[A-Z].+[A-Z]$/})
```

### Exercici 20
```sql
db.students.find({name:/^[aeiou]/i})
```

### Exercici 21
```sql
db.students.find({name:/\w\s\w/i})
```
### Exercici 22
```sql
db.students.find({name:/\w\s\w/i})
```

### Exercici 23
```sql
db.students.find({name:/\w\s\w/i})
```


## Base de dades edx – col·lecció bios

### Exercici 24
```sql
db.bios.find({ "contribs": "OOP" }, { "_id": 0, "name": 1 })
```

### Exercici 25
```sql
db.bios.find({ $or: [{ "contribs": "OOP" }, { "contribs": "Java" }] }, { "_id": 0, "name": 1 })
```
### Exercici 26
```sql
db.bios.find({ "contribs": { $all: ["OOP", "Simula"] } }, { "_id": 0, "name": 1 })
```

### Exercici 27
```sql
db.bios.find({ "deathYear": { $exists: false } }, { "_id": 0, "name": 1 })
```

### Exercici 28
```sql
db.bios.find({ "deathYear": { $exists: true } }, { "_id": 0, "name": 1 })
```

### Exercici 29
```sql
db.bios.find({ "awards.year": 2002 }, { "_id": 0, "name": 1 })
```

### Exercici 30
```sql
db.bios.find({ $expr: { $eq: [{ $size: "$awards" }, 3] } }, { "_id": 0, "name": 1 })
```


## Base de dades imdb – col·lecció people

### Exercici 31
```sql
```

### Exercici 32
```sql
```
### Exercici 33
```sql
```

### Exercici 34
```sql
```

### Exercici 35
```sql
```

## Base de dades edx – col·lecció books

### Exercici 36
```sql
db.books.find({ "author": { $all: ["Martin Fowler", "Kent Beck"] } }, { "_id": 0, "title": 1 })
```

### Exercici 37
```sql
db.books.find({ "tags": { $all: ["programming", "agile"] } }, { "_id": 0, "title": 1 })
```
### Exercici 38
```sql
db.books.find({ "tags": { $in: ["html", "html5", "css", "css3"] } }, { "_id": 0, "title": 1 })
```

### Exercici 39
```sql
db.books.find({ "tags": { $nin: ["html", "html5", "css", "css3"] } }, { "_id": 0, "title": 1 })
```

