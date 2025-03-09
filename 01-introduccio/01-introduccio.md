# 🚀 Introducció a MongoDB i Atlas

## 🎯 Què aprendrem?
En aquesta secció entendrem per què necessitem MongoDB i com Atlas complementa les bases de dades tradicionals que ja coneixem. Veurem com MongoDB ens ofereix una manera més flexible de guardar dades i com Atlas ens facilita treballar al núvol.

## 📚 Teoria
MongoDB és una base de dades NoSQL orientada a documents. Mentre que:
- 📋 SQL guarda dades en taules rígides (com un Excel)
- 📦 MongoDB guarda documents flexibles (com fitxers JSON)
- ☁️ Atlas ens dona MongoDB al núvol (sense instal·lar res)

### 🌟 Exemples del món real
- 👥 Xarxa social: Cada usuari pot tenir diferents tipus de dades
  * 📸 Un té fotos i vídeos
  * 📝 Un altre només text
  * 🎵 Un altre té música i events

- 🛍️ Botiga online: Productes molt diferents
  * 👕 Roba amb talles i colors
  * 💻 Electrònica amb especificacions
  * 📚 Llibres amb autor i ISBN

- 🍳 App de receptes:
  * 🥗 Ingredients variables
  * 📝 Passos diferents
  * 📸 Fotos opcionals

### 💡 Casos Reals: MongoDB vs SQL

#### 1. 🏨 Aplicació de Reserves d'Hotel
**Problema:** Cada hotel té diferents tipus d'habitacions amb característiques úniques
- **Amb SQL:**
  ```sql
  CREATE TABLE habitacions (
    id INT PRIMARY KEY,
    tipus VARCHAR(50),
    -- Necessitem moltes columnes, moltes seran NULL
    te_jacuzzi BOOLEAN,
    te_terrassa BOOLEAN,
    tipus_llit VARCHAR(50),
    te_cuina BOOLEAN,
    te_sala BOOLEAN,
    -- I si volem afegir més característiques?
    -- Necessitem ALTER TABLE cada vegada!
  );
  ```
- **Amb MongoDB:**
  ```javascript
  {
    "_id": ObjectId(),
    "tipus": "Suite Premium",
    "caracteristiques": {
      "jacuzzi": true,
      "terrassa": {
        "metres": 20,
        "mobiliari": ["taula", "gandules", "para-sol"]
      },
      "dormitori": {
        "llits": [
          {"tipus": "king-size", "quantitat": 1},
          {"tipus": "individual", "quantitat": 1}
        ]
      }
    }
    // Podem afegir més característiques sense modificar estructura!
  }
  ```
**Per què MongoDB?** Cada habitació pot tenir característiques diferents i podem afegir-ne de noves sense modificar l'estructura.

#### 2. Catàleg de Productes E-commerce
**Problema:** Diferents tipus de productes necessiten diferents atributs
- **Amb SQL:**
  ```sql
  -- Necessitem múltiples taules
  CREATE TABLE productes_roba (
    id INT PRIMARY KEY,
    nom VARCHAR(100),
    talles VARCHAR(10)[]
  );
  
  CREATE TABLE productes_electronica (
    id INT PRIMARY KEY,
    nom VARCHAR(100),
    voltatge INT
  );
  
  -- I una taula per cada tipus nou!
  ```
- **Amb MongoDB:**
  ```javascript
  // Tot en una mateixa col·lecció
  {
    "_id": ObjectId(),
    "tipus": "roba",
    "nom": "Samarreta",
    "talles": ["S", "M", "L"],
    "colors": ["blanc", "negre"]
  }
  
  {
    "_id": ObjectId(),
    "tipus": "electronica",
    "nom": "Portàtil",
    "specs": {
      "ram": "16GB",
      "cpu": "i7",
      "storage": "512GB"
    }
  }
  ```
**Per què MongoDB?** Un sol lloc per tots els productes, cada un amb els seus atributs específics.

#### 3. Xarxa Social d'Estudiants
**Problema:** Cada estudiant comparteix diferents tipus de contingut
- **Amb SQL:**
  ```sql
  -- Necessitem moltes taules relacionades
  CREATE TABLE posts (
    id INT PRIMARY KEY,
    tipus VARCHAR(50),
    -- Moltes columnes seran NULL segons el tipus
    text_content TEXT,
    image_url VARCHAR(255),
    video_url VARCHAR(255),
    poll_options TEXT[]
  );
  ```
- **Amb MongoDB:**
  ```javascript
  // Post de text
  {
    "_id": ObjectId(),
    "tipus": "text",
    "contingut": "Avui examen de MongoDB!",
    "tags": ["estudis", "basedades"]
  }
  
  // Post amb enquesta
  {
    "_id": ObjectId(),
    "tipus": "enquesta",
    "pregunta": "Millor base de dades?",
    "opcions": ["MongoDB", "MySQL", "PostgreSQL"],
    "vots": {
      "MongoDB": 15,
      "MySQL": 10,
      "PostgreSQL": 12
    }
  }
  ```
**Per què MongoDB?** 
- Flexibilitat per diferents tipus de contingut
- Fàcil d'afegir nous tipus de posts
- Consultes més simples (tot en una col·lecció)
- Millor rendiment en lectures (no necessitem JOINs)

### Comparativa Ràpida
SQL                 | MongoDB
-------------------|------------------
Base de dades      | Base de dades
Taula              | Col·lecció
Fila               | Document
Columna            | Camp
JOIN               | $lookup
Clau Primària      | _id

### Comparativa Detallada
```sql
-- SQL
CREATE TABLE usuaris (
    id INT PRIMARY KEY,
    nom VARCHAR(100),
    edat INT
);

INSERT INTO usuaris VALUES (1, 'Joan', 25);
```

```javascript
// MongoDB
{
  "_id": ObjectId(),
  "nom": "Joan",
  "edat": 25,
  "interessos": ["mongodb", "programació"]  // Podem afegir camps nous!
}
```

## ⚡ Exercici Pràctic
Anem a crear la nostra primera base de dades!

1. 🔑 Crear compte:
```javascript
// Ves a mongodb.com/cloud/atlas
// Clica "Try Free"
// Omple:
//   - Email professional
//   - Password segura
//   - Nom del projecte: "CursFP"
```

2. 🛠️ Configurar accés:
```javascript
// Security > Database Access
// Add New Database User
// Username: fpuser
// Password: fppass2024
// Role: Atlas admin
```

3. Crear primera base de dades:
```javascript
// Collections > Create Database
// Database: escola
// Collection: alumnes
// Primer document:
{
  "nom": "Joan Garcia",
  "curs": "DAW2",
  "moduls": ["M06", "M07", "M08"],
  "notes": {
    "M06": 8,
    "M07": 7,
    "M08": 9
  }
}
```

## 🎮 Repte
Expandeix la base de dades d'alumnes:

1. 👤 Afegeix més alumnes amb:
   - Nom complet
   - Email
   - Telèfon
   - Adreça completa

2. 📚 Per cada alumne, afegeix:
   - Mòduls que cursa
   - Notes per UF
   - Assistència

3. Crea documents diferents per:
   - Alumne presencial
   - Alumne online
   - Alumne dual

## 📚 Per aprendre més
- MongoDB University: https://university.mongodb.com/
- Atlas Tutorials: https://docs.atlas.mongodb.com/getting-started/
- MongoDB Manual: https://docs.mongodb.com/manual/
- Community Forums: https://www.mongodb.com/community

## 💡 Punts Clau a Recordar
- 📦 MongoDB és flexible: no necessita estructura fixa
- 🔄 Els documents poden tenir camps diferents
- ☁️ Atlas ens estalvia instal·lacions complexes
- 🔀 Podem barrejar tipus de dades en un document
- 🚀 És més fàcil modificar l'estructura sobre la marxa

## ⏭️ Següent tema
Al següent tema aprendrem a configurar el nostre cluster en detall i començarem a fer consultes més complexes. 