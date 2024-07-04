# Supertest

## ¿Qué es Supertest y cómo se usa?

Supertest es una librería de Node.js que permite realizar peticiones HTTP a una aplicación Express y testear sus respuestas. Es una herramienta muy útil para realizar pruebas de integración en aplicaciones Express.

Para instalar Supertest, ejecuta el siguiente comando:

```bash
npm install supertest --save-dev
```

Para usar Supertest, primero debes importar la aplicación Express que quieres testear y la librería Supertest. Luego, puedes realizar peticiones HTTP a tu aplicación Express y testear sus respuestas. Por ejemplo, puedes realizar una petición GET a una ruta de tu aplicación Express y comprobar que la respuesta es la esperada.

A continuación, se muestra un ejemplo de cómo usar Supertest para testear una aplicación Express:

```javascript
const express = require('express');
const supertest = require('supertest');

const app = express();

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

const request = supertest(app);

request.get('/')
  .expect(200)
  .expect('Hello, world!')
```

En este ejemplo, se crea una aplicación Express que responde con "Hello, world!" cuando se realiza una petición GET a la ruta "/". Luego, se crea un objeto `request` de Supertest que realiza una petición GET a la ruta "/" de la aplicación Express y se espera que la respuesta sea un código de estado 200 y el texto "Hello, world!".


