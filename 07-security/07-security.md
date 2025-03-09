# 🔐 Seguretat i Control d'Accés

## 🎯 Què aprendrem?
En aquesta secció aprendrem a configurar la seguretat bàsica i el control d'accés en MongoDB Atlas utilitzant les opcions disponibles al pla gratuït M0.

## 🌱 Preparació de l'Entorn
Per practicar la seguretat utilitzarem:

1. **Col·leccions d'exemple**:
- `sample_training.zips`: Per practicar permisos de lectura
- `sample_training.grades`: Per practicar permisos d'escriptura

2. **Base de dades de test**:
```javascript
// Crear una nova base de dades per proves
use seguretat_test

// Crear col·lecció d'usuaris
db.usuaris.insertMany([
  {
    "username": "professor1",
    "email": "prof1@escola.com",
    "rol": "professor"
  },
  {
    "username": "alumne1",
    "email": "alumne1@escola.com",
    "rol": "alumne"
  }
]);

// Crear col·lecció de notes
db.notes.insertMany([
  {
    "alumne_id": "alumne1",
    "assignatura": "MongoDB",
    "nota": 8.5
  },
  {
    "alumne_id": "alumne2",
    "assignatura": "MongoDB",
    "nota": 7.5
  }
]);
```

3. **Rols que crearem**:
- 👨‍🏫 Professor (lectura/escriptura)
- 👨‍🎓 Alumne (només lectura)
- 📊 Analista (només agregacions)

## 📚 Teoria
La seguretat en Atlas M0 es basa en:
- 🔑 Autenticació bàsica d'usuaris
- 🌐 Control d'accés per IP
- 👥 Rols bàsics predefinits
- 🔒 Connexions segures (TLS)

### 🚫 Limitacions de Seguretat en M0
- No es poden crear rols personalitzats
- No hi ha integració amb LDAP/AD
- No hi ha auditoria avançada
- No es poden usar Private Endpoints
- Un sol usuari administrador

#### Què podem fer amb el pla gratuït?
- ✅ Crear usuaris bàsics (amb permisos de lectura/escriptura)
- ✅ Controlar accés per IP (qui es pot connectar)
- ✅ Usar connexions segures (SSL/TLS)
- ✅ Gestionar contrasenyes
- ✅ Usar els rols bàsics (read, readWrite)

#### Què NO podem fer amb M0 (però és bo saber que existeix)

1. **Rols Personalitzats** 🎭
```javascript
// En versions de pagament podríem fer:
db.createRole({
  role: "gestor_vendes",
  privileges: [
    { resource: { db: "botiga", collection: "vendes" }, actions: ["find", "update"] },
    { resource: { db: "botiga", collection: "clients" }, actions: ["find"] }
  ]
})
```
➡️ Útil quan: Necessites permisos molt específics per cada rol d'usuari

2. **Integració amb LDAP/Active Directory** 👥
- Permet usar els mateixos usuaris que a l'empresa
- Centralitza la gestió d'usuaris
- Molt útil en entorns empresarials grans

3. **Auditoria Avançada** 📋
```javascript
// En versions de pagament podries veure:
{
  "usuari": "maria",
  "acció": "update",
  "col·lecció": "vendes",
  "data": ISODate("2024-03-15T10:30:00Z"),
  "canvis": { ... }
}
```
➡️ Important per: Seguretat, compliment normatiu, traçabilitat

4. **Private Endpoints** 🔒
- Connexions directes i segures des de AWS/Azure/Google Cloud
- Sense passar per internet pública
- Essencial per aplicacions empresarials

#### Per què és important conèixer això?
- 🎓 Prepara't pel món professional
- 🔄 Entén les limitacions del pla gratuït
- 📈 Coneix les opcions de creixement
- 🏢 Comprèn necessitats empresarials

> 💡 **Consell**: Comença amb les funcions bàsiques de M0. Quan necessitis més seguretat per un projecte real, ja sabràs quines opcions tens disponibles.

### 🌟 Exemples del món real (adaptats a M0)
- 🎓 Entorn educatiu:
  * 👨‍🏫 Accés del professor
  * 👥 Accés dels alumnes
  * 📱 Accés des de l'aula

- 💻 desenvolupament:
  * 🔑 Credencials de desenvolupament
  * 🌐 Accés local
  * 🔒 Connexions segures

### 💡 Casos Reals: Seguretat Bàsica

#### 1. 👥 Gestió d'Usuaris
```javascript
// Crear usuari amb rol bàsic (permès)
use admin
db.createUser({
  user: "alumne",
  pwd: "password123",
  roles: [
    { role: "read", db: "escola" }  // Rol bàsic permès
  ]
})

#### 2. 🌐 Control d'Accés IP (Permès)
```javascript
// Des de la UI d'Atlas:
// Network Access > Add IP Address

// Configuracions permeses:
{
  "ipAddress": "192.168.1.100",  // IP específica
  "comment": "PC Aula Informàtica"
}

{
  "ipAddress": "192.168.1.0/24",  // Rang d'IPs
  "comment": "Xarxa Institut"
}
```

## ⚡ Exercici Pràctic
Configurem la seguretat bàsica permesa en M0!

1. 🔑 Usuaris i Rols Bàsics:
```javascript
// Crear usuari només lectura (permès)
db.createUser({
  user: "lector",
  pwd: "lectura123",
  roles: [
    { role: "read", db: "biblioteca" }
  ]
})

// Crear usuari lectura/escriptura (permès)
db.createUser({
  user: "editor",
  pwd: "edicio123",
  roles: [
    { role: "readWrite", db: "escola" }
  ]
})
```