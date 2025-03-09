# 📊 Índexs i Optimització

## 🎯 Què aprendrem?
En aquesta secció aprendrem a optimitzar el rendiment de les nostres consultes utilitzant els índexs bàsics disponibles en el pla gratuït d'Atlas M0.

## 🌱 Dades d'Exemple
Per aquest tema utilitzarem la col·lecció "sample_training" que ve preinstal·lada amb Atlas. Per carregar-la:

1. Al dashboard d'Atlas, clica "Browse Collections"
2. Clica "Add My Own Data"
3. Selecciona "Load Sample Dataset"

Utilitzarem específicament aquestes col·leccions:
- `sample_training.zips`: ~30k documents amb dades postals
- `sample_training.grades`: ~1000 documents amb notes d'estudiants
- `sample_training.trips`: dades de viatges

```javascript
// Exemple de document de zips
{
  "_id": "5c8eccc1caa187d17ca6ed16",
  "city": "ALPINE",
  "zip": "35014",
  "loc": {
    "y": 33.331165,
    "x": 86.208934
  },
  "pop": 3062,
  "state": "AL"
}

// Exemple de document de grades
{
  "_id": "56d5f7eb604eb380b0d8d8ce",
  "student_id": 0,
  "scores": [
    {
      "type": "exam",
      "score": 78.5
    },
    {
      "type": "quiz",
      "score": 74.2
    }
  ],
  "class_id": 339
}
```

## 📚 Teoria
Els índexs en M0 són limitats però útils:
- 🔑 _id index (automàtic)
- 📑 Single field index
- 🚫 No índexs compostos en M0
- ⚡ Límit de consultes/segon
- 🚫 No índexs de text
- 🚫 No índexs geoespacials
- 🚫 No índexs únics (excepte _id)

### 🎓 Tipus d'Índexs en MongoDB

#### 1. 📑 Índexs Simples (Disponibles en M0)
- **Descripció**: Índexs en un sol camp
- **Ús**: Cerques per un camp específic
- **Exemple**: 
```javascript
db.zips.createIndex({ "state": 1 })  // 1 ascendent, -1 descendent
```
- **Quan usar-los**: Cerques freqüents per un camp concret

#### 2. 🔄 Índexs Compostos (No disponibles en M0)
- **Descripció**: Índexs que combinen múltiples camps
- **Ús**: Cerques que filtren per diversos camps
- **Exemple**: 
```javascript
// No disponible en M0
db.zips.createIndex({ "state": 1, "city": 1 })
```
- **Per què són importants**: Optimitzen consultes amb múltiples condicions

#### 3. 📝 Índexs de Text (No disponibles en M0)
- **Descripció**: Optimitzen cerques de text complet
- **Ús**: Cercador intern, cerca per paraules clau
- **Exemple**:
```javascript
// No disponible en M0
db.articles.createIndex({ "content": "text" })
```
- **Quan són necessaris**: Cercadors, motors de cerca

#### 4. 🌍 Índexs Geoespacials (No disponibles en M0)
- **Descripció**: Optimitzen consultes de localització
- **Ús**: Cerques per proximitat, distància
- **Exemple**:
```javascript
// No disponible en M0
db.places.createIndex({ "location": "2dsphere" })
```
- **Aplicacions**: Maps, delivery, geolocalització

#### 5. 🔒 Índexs Únics (Limitats en M0)
- **Descripció**: Garanteixen valors únics
- **Ús**: Evitar duplicats (emails, codis)
- **Exemple**:
```javascript
// Només disponible per _id en M0
db.users.createIndex({ "email": 1 }, { unique: true })
```
- **Importància**: Integritat de dades

#### 6. 🎯 Índexs Parcials (No disponibles en M0)
- **Descripció**: Índexs que només cobreixen documents que compleixen una condició
- **Ús**: Optimitzar subconjunts de dades
- **Exemple**:
```javascript
// No disponible en M0
db.orders.createIndex(
  { "status": 1 },
  { partialFilterExpression: { "active": true } }
)
```
- **Beneficis**: Menor ús de recursos, millor rendiment

### 🌟 Exemples del món real (adaptats a M0)
- 🏪 Botiga petita:
  * 📦 Cerca per categoria
  * 💰 Filtratge per preu
  * 📊 Comptadors simples

- 📚 Biblioteca:
  * 📖 Cerca per ISBN
  * 👤 Cerca per usuari
  * 📅 Préstecs actius

### 💡 Casos Reals: Optimització Simple

#### 1. 🔍 Índexs Bàsics
```javascript
// Crear índex per ciutat
db.zips.createIndex({ "city": 1 })

// Consulta optimitzada
db.zips.find({ "city": "ALPINE" })

// Veure índexs existents
db.zips.getIndexes()

// Analitzar consulta
db.zips.find({ "city": "ALPINE" }).explain("executionStats")
```

#### 2. 📈 Monitoratge Bàsic
```javascript
// Consultar estadístiques de col·lecció
db.zips.stats()

// Mida de la col·lecció
db.zips.dataSize()

// Nombre de documents
db.zips.count()
```

## ⚡ Exercici Pràctic
Optimitzem les consultes més comunes!

1. 📑 Crear Índexs Permesos:
```javascript
// ✅ Índex simple permès
db.zips.createIndex({ "state": 1 })

// ✅ Índex simple per població
db.zips.createIndex({ "pop": 1 })
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

1. 🏷️ Anàlisi:
   - Identificar camps més consultats
   - Verificar tipus de consultes
   - Prioritzar índexs simples

2. 👥 Optimització:
   - Índex per estat
   - Índex per població
   - Analitzar rendiment

3. 📊 Monitoratge:
   - Temps de resposta
   - Ús d'índexs
   - Plans d'execució

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

// En exemples d'índexs
db.usuaris.find({ "_id": "USR001" })  // ID més simple

// En explicacions
// Altres opcions disponibles en plans de pagament:
// - Índexs compostos
// - Índexs de text
// - Índexs geoespacials 