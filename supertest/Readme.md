# Supertest

## ¿Qué es Supertest y cómo se usa?

Supertest es una librería de Node.js que permite realizar peticiones HTTP a una aplicación Express y testear sus respuestas. Es una herramienta muy útil para realizar pruebas de integración en aplicaciones Express.

Para instalar Supertest, ejecuta el siguiente comando:

```bash
npm install supertest jest --save-dev
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

describe('GET /', () => {
    it('responds with Hello, world!', (done) => {
        request.get('/')
        .expect(200)
        .expect('Hello, world!', done);
    });
});
```

## Integración con Jest

Supertest puede hacer uso de los métodos previamente vistos de Jest para realizar las pruebas. Por ejemplo, puedes usar `expect` con los matchers de Jest para comprobar que la respuesta de la aplicación Express es la esperada.

```javascript
const express = require('express');
const supertest = require('supertest');

app.use(express.json());

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

app.post('/data', (req, res) => {
  res.status(201).send(req.body);
});

const request = supertest(app);

describe('Express App', () => {
  describe('GET /', () => {
    it('responds with Hello, world!', async () => {
      const response = await request.get('/');
      expect(response.status).toBe(200);
      expect(response.text).toBe('Hello, world!');
    });
  });

  describe('POST /data', () => {
    it('responds with sent data', async () => {
      const data = { name: 'John', age: 30 };
      const response = await request.post('/data').send(data);
      expect(response.status).toBe(201);
      expect(response.body).toEqual(data);
    });
  });
});
```



