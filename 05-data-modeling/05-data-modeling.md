# 🏗️ Modelatge de Dades

## 🎯 Què aprendrem?
En aquesta secció aprendrem a dissenyar l'estructura de les nostres dades de manera eficient, tenint en compte les limitacions del pla gratuït d'Atlas M0.

## 📚 Teoria
El modelatge en MongoDB és diferent de SQL:
- 📦 Documents flexibles vs Taules rígides
- 🔗 Referències vs Joins
- 📎 Dades incrustades vs Normalització
- 📏 Límit de 16MB per document en M0

### 🌟 Exemples del món real (adaptats a M0)
- 👤 Perfil d'usuari:
  * 📝 Dades bàsiques
  * 📫 Contacte principal
  * 🏷️ Preferències simples

- 📱 Blog personal:
  * 📄 Posts (limitats)
  * 💬 Últims comentaris
  * 🏷️ Categories bàsiques

### 💡 Casos Reals: Modelatge Eficient

#### 1. 👥 Model d'Usuaris i Posts
```javascript
// Model d'usuari (lleuger)
{
  "_id": ObjectId("..."),
  "nom": "Maria Garcia",
  "email": "maria@example.com",
  "ultimPost": {  // Només el més recent
    "titol": "MongoDB Atlas M0",
    "data": ISODate("2024-03-10")
  }
}

// Model de post (separat)
{
  "_id": ObjectId("..."),
  "usuari_id": ObjectId("..."),
  "titol": "MongoDB Atlas M0",
  "contingut": "Text del post...",
  "data": ISODate("2024-03-10")
}
```

#### 2. 📚 Model de Biblioteca Simple
```javascript
// Model de llibre amb préstecs recents
{
  "_id": ObjectId("..."),
  "titol": "MongoDB Bàsic",
  "autor": "Joan Pere",
  "copiesDisponibles": 3,
  "ultimsPrestecs": [  // Limitat a últims 5
    {
      "usuari": "maria@example.com",
      "dataRetorn": ISODate("2024-03-15")
    }
  ]
}
```

## ⚡ Exercici Pràctic
Dissenyem models eficients!

1. 🎓 Model d'Escola:
```javascript
// Col·lecció d'alumnes (eficient)
{
  "_id": ObjectId("..."),
  "nom": "Pere Vila",
  "curs": "DAW2",
  "assignaturesActuals": [  // Només les d'aquest curs
    {
      "codi": "M06",
      "nom": "JavaScript",
      "professor": "Joan Soler"
    }
  ]
}

// Col·lecció de notes (separada)
{
  "alumne_id": ObjectId("..."),
  "assignatura": "M06",
  "trimestre": 1,
  "nota": 8
}
```

## 🎮 Repte
Dissenya un model per una xarxa social simple:

1. 👤 Perfils:
   - Dades bàsiques d'usuari
   - Últims 3 posts
   - Amics recents (màxim 10)

2. 📝 Posts:
   - Contingut del post
   - Últims 5 comentaris
   - Likes (contador simple)

3. 🤝 Connexions:
   - Relacions d'amistat
   - Grups (màxim 5 per usuari)
   - Interessos compartits

## 📚 Per aprendre més
- Data Modeling: https://docs.mongodb.com/manual/core/data-modeling-introduction/
- Schema Design: https://www.mongodb.com/blog/post/building-with-patterns-the-document-versioning-pattern
- M0 Best Practices: https://docs.atlas.mongodb.com/best-practices/

## 💡 Punts Clau a Recordar
- 📏 Respecta el límit de 16MB per document
- 🔍 Dissenya pensant en les consultes freqüents
- 📦 Utilitza referències per dades grans
- 🎯 Mantén els arrays controlats
- ⚡ Prioritza l'eficiència en lectures

## ⏭️ Següent tema
Al següent tema veurem com optimitzar el rendiment amb índexs bàsics dins les limitacions d'Atlas M0. 