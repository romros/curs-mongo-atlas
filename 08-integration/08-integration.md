# 🔄 Integració amb Aplicacions

## 🎯 Què aprendrem?
En aquesta secció aprendrem a connectar i utilitzar MongoDB Atlas directament des del navegador utilitzant JavaScript vanilla, sense necessitat de llibreries externes.

## 🌱 Dades per Practicar
Utilitzarem dues fonts de dades:

1. **Col·leccions d'exemple d'Atlas**:
- `sample_training.zips`: Per cerques de localitats
- `sample_training.grades`: Per gestió de notes

2. **Nova col·lecció per la nostra app**:
```javascript
// Crear col·lecció de tasques
use app_test
db.tasques.insertMany([
  {
    "titol": "Aprendre MongoDB",
    "descripcio": "Completar el curs bàsic",
    "estat": "pendent",
    "prioritat": 1,
    "dataCreacio": new Date()
  },
  {
    "titol": "Practicar JavaScript",
    "descripcio": "Fer exercicis DOM",
    "estat": "en_progres",
    "prioritat": 2,
    "dataCreacio": new Date()
  },
  {
    "titol": "Projecte Final",
    "descripcio": "Crear app amb MongoDB i JS",
    "estat": "pendent",
    "prioritat": 3,
    "dataCreacio": new Date()
  }
]);
```

> 💡 **Nota**: Aquestes dades són ideals per practicar CRUD des del frontend i són prou simples per M0.

## 📚 Teoria
La integració amb Atlas M0 des del navegador:
- 🔌 API REST amb fetch
- 🔒 CORS i seguretat
- ⚡ Gestió asíncrona
- 📊 Manipulació del DOM

### 🌟 Exemples del món real (adaptats a M0)
- 🌐 Web personal:
  * 📝 Blog simple amb HTML+JS
  * 👤 Perfil dinàmic
  * 📊 Estadístiques en temps real

- 📱 App d'estudiants:
  * 📚 Notes en temps real
  * 📅 Calendari interactiu
  * ✅ Llista de tasques

### 💡 Casos Reals: Integració Bàsica

#### 1. 🔌 Connexió Bàsica
```javascript
// config.js
const ATLAS_API = "https://data.mongodb-api.com/app/data-api/endpoint/data/v1";
const API_KEY = "TuAPIKey";  // Guardar de forma segura!

// Funció base per connexió
async function connectAtlas(collection, action, data = null) {
  const headers = {
    'Content-Type': 'application/json',
    'Access-Control-Request-Headers': '*',
    'api-key': API_KEY
  };

  const config = {
    method: 'POST',
    headers: headers,
    body: JSON.stringify({
      collection: collection,
      database: "escola",
      dataSource: "Cluster0",
      ...data
    })
  };

  try {
    const response = await fetch(`${ATLAS_API}/action/${action}`, config);
    return await response.json();
  } catch (error) {
    console.error("Error:", error);
    throw error;
  }
}
```

#### 2. 📝 Operacions CRUD
```javascript
// crud.js
async function getAlumnes() {
  const result = await connectAtlas("alumnes", "find");
  return result.documents;
}

async function addAlumne(alumne) {
  return await connectAtlas("alumnes", "insertOne", {
    document: alumne
  });
}

async function updateAlumne(id, data) {
  return await connectAtlas("alumnes", "updateOne", {
    filter: { _id: { $oid: id } },
    update: { $set: data }
  });
}

// Exemple d'ús amb DOM
document.getElementById('btnCarrega').addEventListener('click', async () => {
  const alumnes = await getAlumnes();
  const llista = document.getElementById('llistaAlumnes');
  
  llista.innerHTML = alumnes.map(alumne => `
    <li class="alumne-item">
      ${alumne.nom} - ${alumne.curs}
      <button onclick="editAlumne('${alumne._id}')">✏️</button>
    </li>
  `).join('');
});
```

## ⚡ Exercici Pràctic
Creem una interfície web simple!

1. 🛠️ HTML Base:
```html
<!DOCTYPE html>
<html>
<head>
  <title>Gestió Alumnes</title>
</head>
<body>
  <div id="app">
    <h1>Gestió d'Alumnes</h1>
    
    <form id="formAlumne">
      <input type="text" id="nom" placeholder="Nom">
      <input type="text" id="curs" placeholder="Curs">
      <button type="submit">Afegir</button>
    </form>

    <ul id="llistaAlumnes"></ul>
  </div>

  <script src="config.js"></script>
  <script src="crud.js"></script>
  <script src="app.js"></script>
</body>
</html>
```

2. 🔐 Gestió d'Events:
```javascript
// app.js
document.getElementById('formAlumne').addEventListener('submit', async (e) => {
  e.preventDefault();
  
  const alumne = {
    nom: document.getElementById('nom').value,
    curs: document.getElementById('curs').value
  };

  await addAlumne(alumne);
  await carregaAlumnes();  // Refresca la llista
});
```

## 🎮 Repte
Crea una aplicació web completa:

1. 📚 Interfície:
   - Formulari d'alta
   - Llista dinàmica
   - Cercador en temps real

2. 🔍 Funcionalitats:
   - Filtres per curs
   - Ordenació per nom/data
   - Edició inline

3. 👥 Millores:
   - Animacions suaus
   - Feedback visual
   - Gestió d'errors

## 📚 Per aprendre més
- Data API: https://docs.mongodb.com/realm/web/
- CORS: https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS
- Fetch API: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API

## 💡 Punts Clau a Recordar
- 🔐 Protegir sempre les credencials
- 🌐 Gestionar CORS adequadament
- ⚡ Usar async/await per claredat
- 🚫 Validar dades d'entrada
- 📊 Proporcionar feedback a l'usuari

## ⏭️ Fi del Curs
Felicitats! Has après a:
- Integrar MongoDB Atlas amb JavaScript pur
- Crear interfícies web dinàmiques
- Implementar CRUD complet al frontend
- Gestionar dades en temps real 