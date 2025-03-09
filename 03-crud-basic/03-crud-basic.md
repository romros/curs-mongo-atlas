# 📝 CRUD Bàsic amb MongoDB

## 🎯 Què aprendrem?
En aquesta secció aprendrem les operacions bàsiques per crear, llegir, actualitzar i eliminar documents (CRUD) utilitzant MongoDB Atlas.

## 📚 Teoria
Les operacions CRUD són la base de qualsevol base de dades:
- 📥 Create (insertOne/insertMany)
- 🔍 Read (find/findOne)
- 🔄 Update (updateOne/updateMany)
- 🗑️ Delete (deleteOne/deleteMany)

### 🌟 Exemples del món real
- 📱 App de notes:
  * ✏️ Crear nota (document simple)
  * 📖 Llegir notes (amb límit)
  * 📝 Actualitzar contingut (un document)
  * ❌ Eliminar notes (una a una)

- 🛒 Gestió d'inventari:
  * 📦 Afegir nous productes
  * 🔍 Consultar stock
  * 🔄 Actualitzar preus
  * 🗑️ Eliminar productes descatalogats

### 💡 Casos Reals: CRUD en Acció

#### 1. 📱 Gestió d'Usuaris
**Problema:** Sistema de registre i perfils d'usuari
```javascript
// CREATE: Registrar nou usuari (document petit)
db.usuaris.insertOne({
  "nom": "Maria Garcia",
  "email": "maria@example.com",
  "ultimAcces": new Date()  // Dades mínimes necessàries
})

// READ: Buscar usuaris (amb límit)
db.usuaris.find({}).limit(20)

// UPDATE: Actualitzar un a un
db.usuaris.updateOne(
  { "email": "maria@example.com" },
  { $set: { "ultimAcces": new Date() } }  // Simple
)

// DELETE: Eliminar usuari
db.usuaris.deleteOne({ "email": "maria@example.com" })
```

#### 2. 🛍️ Gestió de Comandes
```javascript
// CREATE: Nova comanda
db.comandes.insertOne({
  "usuari_id": ObjectId("..."),
  "data": new Date(),
  "productes": [
    { "id": 1, "nom": "MongoDB Shirt", "preu": 15.99, "quantitat": 2 },
    { "id": 2, "nom": "Database Stickers", "preu": 3.99, "quantitat": 5 }
  ],
  "estat": "pendent"
})

// READ: Buscar comandes pendents
db.comandes.find({ "estat": "pendent" })

// UPDATE: Marcar com enviada
db.comandes.updateOne(
  { "_id": ObjectId("...") },
  { $set: { "estat": "enviada" } }
)
```

## ⚡ Exercici Pràctic
Anem a practicar les operacions CRUD!

1. 📥 Create:
```javascript
// Afegir diversos alumnes
db.alumnes.insertMany([
  {
    "nom": "Pere Costa",
    "edat": 19,
    "moduls": ["M06", "M07"]
  },
  {
    "nom": "Anna Puig",
    "edat": 20,
    "moduls": ["M06", "M08"]
  }
])
```

2. 🔍 Read:
```javascript
// Buscar alumnes per mòdul
db.alumnes.find({ "moduls": "M06" })

// Buscar per edat
db.alumnes.find({ "edat": { $gte: 20 } })
```

3. 🔄 Update:
```javascript
// Afegir un mòdul a un alumne
db.alumnes.updateOne(
  { "nom": "Pere Costa" },
  { $push: { "moduls": "M09" } }
)
```

4. 🗑️ Delete:
```javascript
// Eliminar un alumne
db.alumnes.deleteOne({ "nom": "Anna Puig" })
```

## 🎮 Repte
Crea un sistema complet de gestió d'una biblioteca:

1. 📚 Llibres:
   - Afegir 5 llibres diferents
   - Cada llibre amb títol, autor, ISBN
   - Afegir stock disponible

2. 👥 Préstecs:
   - Crear préstecs per diferents usuaris
   - Registrar data d'inici i retorn
   - Actualitzar l'estat dels préstecs

3. 📊 Consultes:
   - Trobar llibres disponibles
   - Llistar préstecs actius
   - Veure historial per usuari

## 📚 Per aprendre més
- CRUD Operations: https://docs.mongodb.com/manual/crud/
- Query Operators: https://docs.mongodb.com/manual/reference/operator/
- MongoDB CRUD Examples: https://mongodb.github.io/node-mongodb-native/markdown-docs/insert.html

## 💡 Punts Clau a Recordar
- 📥 insertOne/insertMany per crear documents
- 🔍 find/findOne per buscar documents
- 🔄 updateOne/updateMany per modificar
- 🗑️ deleteOne/deleteMany per eliminar
- 🎯 Sempre verificar els resultats de les operacions

## ⏭️ Següent tema
Al següent tema veurem consultes avançades i agregacions per extreure informació més complexa de les nostres dades. 