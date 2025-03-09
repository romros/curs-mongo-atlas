# 📊 Índexs i Optimització

## 🎯 Què aprendrem?
En aquesta secció aprendrem a optimitzar el rendiment de les nostres consultes utilitzant els índexs bàsics disponibles en el pla gratuït d'Atlas M0.

## 📚 Teoria
Els índexs en M0 són limitats però útils:
- 🔑 _id index (automàtic)
- 📑 Single field index
- 🚫 No índexs compostos en M0
- ⚡ Límit de consultes/segon

### 🌟 Exemples del món real (adaptats a M0)
- 🏪 Botiga petita:
  * 📦 Cerca per codi producte
  * 💰 Filtratge per preu
  * 📅 Consultes per data

- 📚 Biblioteca:
  * 📖 Cerca per ISBN
  * 👤 Cerca per usuari
  * 📅 Préstecs actius

### 💡 Casos Reals: Optimització Simple

#### 1. 🔍 Índexs Bàsics
```javascript
// Crear índex simple
db.productes.createIndex({ "codi": 1 })

// Consulta optimitzada
db.productes.find({ "codi": "PROD001" })

// Veure índexs existents
db.productes.getIndexes()

// Analitzar consulta
db.productes.find({ "codi": "PROD001" }).explain("executionStats")
```

#### 2. 📈 Monitoratge Bàsic
```javascript
// Consultar estadístiques de col·lecció
db.productes.stats()

// Mida de la col·lecció
db.productes.dataSize()

// Nombre de documents
db.productes.count()
```

## ⚡ Exercici Pràctic
Optimitzem les consultes més comunes!

1. 📑 Crear Índexs:
```javascript
// Índex per cerca d'usuaris
db.usuaris.createIndex({ "email": 1 })

// Índex per productes
db.productes.createIndex({ "categoria": 1 })

// Comprovar ús d'índexs
db.usuaris.find({ "email": "test@example.com" }).explain()
```

2. 📊 Anàlisi de Rendiment:
```javascript
// Consulta sense índex
db.productes.find({ "nom": "Llibreta" })

// Mateixa consulta amb índex
db.productes.createIndex({ "nom": 1 })
db.productes.find({ "nom": "Llibreta" })
```

## 🎮 Repte
Optimitza una botiga online simple:

1. 🏷️ Productes:
   - Índex per codi únic
   - Índex per categoria
   - Analitzar consultes freqüents

2. 👥 Usuaris:
   - Índex per email
   - Índex per ciutat
   - Comprovar rendiment

3. 🛒 Comandes:
   - Índex per data
   - Índex per estat
   - Monitoritzar temps de resposta

## 📚 Per aprendre més
- Index Basics: https://docs.mongodb.com/manual/indexes/
- Query Optimization: https://docs.mongodb.com/manual/tutorial/optimize-query-performance-with-indexes-and-projections/
- Atlas M0 Limits: https://docs.atlas.mongodb.com/reference/free-shared-limitations/

## 💡 Punts Clau a Recordar
- 🔑 Usa índexs per camps de cerca freqüent
- 📊 Monitoritza el rendiment de les consultes
- ⚠️ Respecta els límits de M0
- 🎯 Optimitza les consultes més usades
- 💾 Mantén les col·leccions petites

## ⏭️ Següent tema
Al següent tema veurem com implementar seguretat bàsica i control d'accés en Atlas M0. 