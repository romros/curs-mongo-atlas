# 🔍 Consultes Avançades i Agregacions

## 🎯 Què aprendrem?
En aquesta secció aprendrem a realitzar consultes i agregacions bàsiques però potents utilitzant el pla gratuït de MongoDB Atlas (M0).

## 🌱 Dades Inicials
Per practicar les consultes avançades, necessitem un conjunt de dades més complet:

```javascript
// Afegim més productes amb més detalls
db.productes.insertMany([
  {
    "nom": "MongoDB Shirt",
    "preu": 15.99,
    "stock": 100,
    "categoria": "roba",
    "colors": ["negre", "blau"],
    "valoracions": [4, 5, 5, 4],
    "dataCreacio": new Date("2024-01-15")
  },
  {
    "nom": "Database Stickers Pack",
    "preu": 3.99,
    "stock": 200,
    "categoria": "accessoris",
    "tipus": ["MongoDB", "SQL", "Redis"],
    "valoracions": [5, 4, 4, 5, 3],
    "dataCreacio": new Date("2024-02-01")
  },
  {
    "nom": "NoSQL Book",
    "preu": 29.99,
    "stock": 50,
    "categoria": "llibres",
    "autor": "Maria Garcia",
    "pagines": 250,
    "valoracions": [5, 5, 4, 5],
    "dataCreacio": new Date("2024-01-10")
  },
  {
    "nom": "Developer Hoodie",
    "preu": 39.99,
    "stock": 75,
    "categoria": "roba",
    "colors": ["gris", "negre", "blau"],
    "valoracions": [4, 4, 3, 5],
    "dataCreacio": new Date("2024-02-15")
  }
]);

// Afegim vendes per agregacions
db.vendes.insertMany([
  {
    "data": new Date("2024-03-01"),
    "producte_id": "SHIRT001",  // ID de la samarreta MongoDB
    "quantitat": 2,
    "preu_unitari": 15.99,
    "client": {
      "nom": "Joan Pere",
      "ciutat": "Barcelona"
    }
  },
  {
    "data": new Date("2024-03-01"),
    "producte_id": "STICKER001",  // ID dels adhesius
    "quantitat": 5,
    "preu_unitari": 3.99,
    "client": {
      "nom": "Anna Vila",
      "ciutat": "Girona"
    }
  },
  {
    "data": new Date("2024-03-02"),
    "producte_id": ObjectId("507f1f77bcf86cd799439013"),  // ID del Book
    "quantitat": 1,
    "preu_unitari": 29.99,
    "client": {
      "nom": "Pere Mas",
      "ciutat": "Barcelona"
    }
  }
]);
```

Aquestes dades ens permetran practicar:
- 🔍 Cerques complexes
- 📊 Agregacions
- 🔢 Operacions amb arrays
- 📅 Consultes per dates

## 📚 Teoria
Les consultes avançades ens permeten...

Amb Atlas M0 podem fer:
- 🎯 Filtres combinats
- 🔄 Agregacions simples
- 📊 Estadístiques bàsiques
- 🔍 Cerques en documents niuats

### 🌟 Exemples del món real (adaptats a M0)
- 📊 Mini dashboard de vendes:
  * 💰 Vendes del dia
  * 📈 Top 3 productes
  * 🌍 Vendes per ciutat

- 📱 Blog personal:
  * 🔝 Posts recents
  * 👥 Comentaris
  * #️⃣ Categories

### 💡 Casos Reals: Consultes per M0

#### 1. 📊 Anàlisi Simple de Vendes
```javascript
// Vendes per dia (dataset petit)
db.vendes.aggregate([
  {
    $group: {
      _id: {
        dia: { $dayOfMonth: "$data" },
        mes: { $month: "$data" }
      },
      total: { $sum: "$import" }
    }
  },
  { $limit: 100 }  // Limitem resultats per M0
])

// Top 3 productes
db.vendes.aggregate([
  { $unwind: "$productes" },
  {
    $group: {
      _id: "$productes.nom",
      total: { $sum: 1 }
    }
  },
  { $sort: { total: -1 } },
  { $limit: 3 }
])
```

#### 2. 🎯 Cerques Eficients
```javascript
// Cerca bàsica amb múltiples condicions
db.productes.find({
  preu: { $lte: 50 },
  stock: { $gt: 0 },
  categoria: "electronics"
})

// Cerca en documents niuats (dataset petit)
db.usuaris.find({
  "ciutat": "Barcelona",
  "edat": { $gte: 18 }
}).limit(20)
```

#### 3. **Auditoria Avançada** 📋
```javascript
// En versions de pagament podries veure:
{
  "usuari": "maria",
  "acció": "update",
  "col·lecció": "vendes",
  "data": ISODate("2024-03-15T10:30:00Z"),
  "canvis": { 
    "abans": {
      "preu": 19.99,
      "stock": 10
    },
    "despres": {
      "preu": 24.99,
      "stock": 5
    }
  }
}
```

## ⚡ Exercici Pràctic
Treballem amb un petit catàleg de productes!

1. 🔍 Consultes Bàsiques:
```javascript
// Trobar productes per rang de preu
db.productes.find({
  preu: { $gte: 10, $lte: 50 }
}).limit(10)

// Cerca per patró en el nom
db.productes.find({
  nom: /^Mon/  // Productes que comencen per "Mon"
})
```

2. 📊 Agregacions Simples:
```javascript
// Comptar productes per categoria
db.productes.aggregate([
  {
    $group: {
      _id: "$categoria",
      total: { $sum: 1 }
    }
  }
])
```

## 🎮 Repte
Analitza un petit catàleg de llibres:

1. 📚 Consultes:
   - Troba llibres per autor
   - Llibres publicats aquest any
   - Llibres per rang de preu

2. 🔍 Cerques Combinades:
   - Llibres d'un autor en stock
   - Llibres per gènere i preu
   - Llibres amb més de 3 còpies

3. 📊 Agregacions Bàsiques:
   - Llibres per editorial
   - Mitjana de preus per gènere
   - Total de llibres en stock

## 📚 Per aprendre més
- Atlas M0 Limits: https://docs.atlas.mongodb.com/reference/free-shared-limitations/
- Basic Queries: https://docs.mongodb.com/manual/tutorial/query-documents/
- Simple Aggregations: https://docs.mongodb.com/manual/aggregation/

## 💡 Punts Clau a Recordar
- 🆓 Atlas M0 és perfecte per aprendre
- 📊 Mantén les consultes simples i eficients
- 🔍 Treballa amb datasets petits (<100MB)
- 📈 Limita els resultats de les consultes
- 💾 Evita operacions massa complexes

## ⏭️ Següent tema
Al següent tema veurem com modelar les dades de manera eficient tenint en compte les limitacions d'Atlas M0. 