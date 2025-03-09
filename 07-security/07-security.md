# 🔐 Seguretat i Control d'Accés

## 🎯 Què aprendrem?
En aquesta secció aprendrem a configurar la seguretat bàsica i el control d'accés en MongoDB Atlas utilitzant les opcions disponibles al pla gratuït M0.

## 📚 Teoria
La seguretat en Atlas M0 es basa en:
- 🔑 Autenticació d'usuaris
- 🌐 Control d'accés per IP
- 👥 Rols predefinits
- 🔒 Connexions segures (TLS)

### 🌟 Exemples del món real (adaptats a M0)
- 🎓 Entorn educatiu:
  * 👨‍🏫 Accés del professor
  * 👥 Accés dels alumnes
  * 📱 Accés des de l'aula

- 💻 Desenvolupament:
  * 🔑 Credencials de desenvolupament
  * 🌐 Accés local
  * 🔒 Connexions segures

### 💡 Casos Reals: Seguretat Bàsica

#### 1. 👥 Gestió d'Usuaris
```javascript
// Crear usuari amb rol bàsic
use admin
db.createUser({
  user: "alumne",
  pwd: "password123",  // Usar contrasenya segura!
  roles: [
    { role: "readWrite", db: "escola" }
  ]
})

// Verificar usuari
db.auth("alumne", "password123")
```

#### 2. 🌐 Control d'Accés IP
```javascript
// Des de la UI d'Atlas:
// Network Access > Add IP Address

// Configuracions comunes:
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
Configurem la seguretat bàsica!

1. 🔑 Usuaris i Rols:
```javascript
// Crear usuari de només lectura
db.createUser({
  user: "lector",
  pwd: "lectura123",
  roles: [
    { role: "read", db: "biblioteca" }
  ]
})

// Crear usuari amb permisos d'escriptura
db.createUser({
  user: "editor",
  pwd: "edicio123",
  roles: [
    { role: "readWrite", db: "biblioteca" }
  ]
})
```

2. 🔒 Connection String Segur:
```javascript
// Format bàsic
mongodb+srv://usuari:password@cluster0.xxxxx.mongodb.net/basedades

// Amb opcions de seguretat
mongodb+srv://usuari:password@cluster0.xxxxx.mongodb.net/basedades?retryWrites=true&w=majority&ssl=true
```

## 🎮 Repte
Implementa seguretat per una app d'estudiants:

1. 👥 Usuaris:
   - Crear rol professor (lectura/escriptura)
   - Crear rol alumne (només lectura)
   - Provar els accessos

2. 🌐 Xarxa:
   - Configurar IP de l'institut
   - Afegir IPs dels professors
   - Verificar connexions

3. 🔒 Connexions:
   - Generar connection strings
   - Provar connexions segures
   - Verificar restriccions

## 📚 Per aprendre més
- Atlas Security: https://docs.atlas.mongodb.com/security/
- User Management: https://docs.mongodb.com/manual/tutorial/create-users/
- Network Security: https://docs.atlas.mongodb.com/security/ip-access-list/

## 💡 Punts Clau a Recordar
- 🔑 Mai compartir credencials
- 🌐 Limitar accés per IP
- 👥 Usar rols adequats
- 🔒 Sempre usar TLS/SSL
- ⚠️ Revisar accessos regularment

## ⏭️ Següent tema
Al següent tema veurem com integrar MongoDB Atlas amb les nostres aplicacions. 