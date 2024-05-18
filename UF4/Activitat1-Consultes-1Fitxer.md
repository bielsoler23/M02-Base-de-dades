# CONSULTES AMB FUNCIONS
El professor us ha proporcionat una sèrie de BD dins de MongoDB

Indica quines són les consultes amb mongoDB que responen a lespreguntes següents:

**Base de dades edx – col·lecció students**

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
