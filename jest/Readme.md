# Jest

## ¿Qué es Jest y cómo se usa?

Jest es un framework de testing de JavaScript desarrollado por Facebook, que se utiliza principalmente para probar aplicaciones React, aunque también puede usarse con cualquier aplicación JavaScript.

### Características Principales de Jest

- **Ejecutor de Pruebas (Test Runner) Integrado**: Jest incluye su propio ejecutor de pruebas que proporciona aislamiento de pruebas, lo que asegura que cada prueba se ejecute en un entorno controlado.
- **Soporte para Pruebas Asíncronas**: Maneja funciones asíncronas de manera eficiente, facilitando la prueba de código que realiza operaciones asíncronas, como llamadas a APIs.
- **Mocking Integrado**: Permite crear mocks y spies de manera sencilla, lo que facilita la simulación de funciones y objetos en las pruebas.

### Instalación

Para instalar Jest en el proyecto:

```bash
npm install --save-dev jest
```

### Configuración

Jest no necesita de una configuración inicial, pero se puede realizar una a través de un archivo `jest.config.js` en la raíz del proyecto. En este archivo, se pueden especificar opciones de configuración como rutas de archivos, transformadores, y más.

A continuacion se muestra un ejemplo de archivo de configuración básico:

```javascript
{
  "testEnvironment": "node",
  "verbose": false,
  "cache": false,
  "transform": {
  },
  "testMatch": ["<rootDir>/tests/**/*.test.js"],
  "testPathIgnorePatterns": [
    "/node_modules/",
    "./index.js"
  ]
}
```

**Test Environment**: Especifica el entorno en el que se ejecutarán las pruebas. En este caso, se utiliza el entorno de Node.js.

**Verbose**: Indica si Jest debe mostrar información detallada durante la ejecución de las pruebas.

**Cache**: Habilita o deshabilita la caché de resultados de pruebas.

**Transform**: Permite especificar transformadores para archivos específicos, como Babel para archivos de JavaScript.

**Test Match**: Define los patrones de archivos que Jest debe considerar como pruebas.

**Test Path Ignore Patterns**: Especifica los patrones de archivos que Jest debe ignorar al buscar pruebas.

### Script para la Ejecución de Pruebas

Para ejecutar las pruebas con Jest, se puede agregar un script en el archivo `package.json`:

```json
"scripts": {
  "test": "jest"
}
```

Jest pordefecto solo soporta archivosque sigan el estandar CommonJS, si se desea usar ES6 se puede usar traspiladores como Babel y configurar Jest para que use Babel. O bien se puede usar `NODE_OPTIONS="$NODE_OPTIONS --experimental-vm-modules"` para que Jest soporte archivos ES6.

Por lo tanto, para ejecutar las pruebas con soporte para ES6, se puede modificar el script de la siguiente manera:

```json
"scripts": {
  "test": "NODE_OPTIONS=\"$NODE_OPTIONS --experimental-vm-modules\" jest"
}
```

### Creación de Pruebas

Para crear pruebas con Jest, se deben seguir ciertas convenciones. Por ejemplo, los archivos de pruebas deben tener la extensión `.test.js` o `.spec.js`, y las funciones de prueba deben comenzar con `test` o `it`.

A continuación se muestra un ejemplo de una prueba simple en Jest:

```javascript
// sum.js
function sum(a, b) {
  return a + b;
}

module.exports = sum;

// sum.test.js
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

En este ejemplo, se define una función `sum` en el archivo `sum.js`, y se crea una prueba para verificar que la función suma correctamente dos números en el archivo `sum.test.js`.

### Ejecución de Pruebas

Para ejecutar las pruebas con Jest, se puede utilizar el script definido en el archivo `package.json`:

```bash
npm test
```

Jest ejecutará todas las pruebas en el proyecto y mostrará los resultados en la consola.

### Expect

Jest proporciona una función `expect` que se utiliza para realizar aserciones en las pruebas. La función `expect` toma un valor y permite verificar si cumple con ciertas condiciones como:

- `toBe`: Verifica si dos valores son iguales utilizando el operador de igualdad estricta (`===`).
- `toEqual`: Verifica si dos valores son iguales utilizando el operador de igualdad (`==`).
- `toBeTruthy`: Verifica si un valor es verdadero.
- `toBeFalsy`: Verifica si un valor es falso.
- `toBeNull`: Verifica si un valor es nulo.
- `toBeDefined`: Verifica si un valor está definido.
- `toBeUndefined`: Verifica si un valor es indefinido.
- `toContain`: Verifica si un valor está contenido en un arreglo o cadena.
- `toHaveLength`: Verifica la longitud de un arreglo o cadena.
- `toBeGreaterThan`: Verifica si un valor es mayor que otro.
- `toBeLessThan`: Verifica si un valor es menor que otro.


### Test suite

Una suite de pruebas es un conjunto de pruebas que se agrupan lógicamente para probar una funcionalidad específica de la aplicación. Jest permite agrupar pruebas en suites utilizando la función `describe`.

A continuación se muestra un ejemplo de una suite de pruebas en Jest:

```javascript
// math.js
function sum(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

module.exports = { sum, subtract };

// math.test.js
const { sum, subtract } = require('./math');

describe('Math functions', () => {
  test('adds 1 + 2 to equal 3', () => {
    expect(sum(1, 2)).toBe(3);
  });

  test('subtracts 2 - 1 to equal 1', () => {
    expect(subtract(2, 1)).toBe(1);
  });
});
```

En este ejemplo, se define un módulo `math` con las funciones `sum` y `subtract`, y se agrupan las pruebas relacionadas con estas funciones en una suite utilizando la función `describe`.

### Hooks de Jest

Jest proporciona hooks que permiten ejecutar código antes y después de las pruebas, suites y módulos. Algunos de los hooks más comunes son:

- `beforeAll`: Se ejecuta una vez antes de que comiencen todas las pruebas en una suite.
- `afterAll`: Se ejecuta una vez después de que finalicen todas las pruebas en una suite.
- `beforeEach`: Se ejecuta antes de cada prueba en una suite.
- `afterEach`: Se ejecuta después de cada prueba en una suite.

A continuación se muestra un ejemplo de cómo utilizar los hooks en Jest:

```javascript

// math.test.js
const { sum, subtract } = require('./math');

describe('Math functions', () => {

    beforeAll(() => {
        console.log('Before all tests');
    });

    afterAll(() => {
        console.log('After all tests');
    });

    beforeEach(() => {
        console.log('Before each test');
    });

    afterEach(() => {
        console.log('After each test');
    });

  test('adds 1 + 2 to equal 3', () => {
    expect(sum(1, 2)).toBe(3);
  });

  test('subtracts 2 - 1 to equal 1', () => {
    expect(subtract(2, 1)).toBe(1);
  });
});
```

### Test de Apis externas

Supongamos que tenemos una función `fetchData` que realiza una llamada a una API usando axios y devuelve los datos obtenidos y todo eso esta dentro de un bloque `try-catch`.

```javascript
// fetchData.js
const axios = require('axios');

async function fetchData(url) {
  try {
    const response = await axios.get(url);
    return response.data;
  } catch (error) {
    console.error('Error fetching data:', error);
    return null;
  }
}

module.exports = fetchData;
```

Al tratarse de un API externa, existen varios problemas al momento de realizar pruebas unitarias, como la variabilidad de los datos, y la necesidad de simular errores. Para resolver estos problemas, podemos utilizar mocks y spies de Jest.

#### Mocks y Spies

Jest proporciona funciones para crear mocks y spies de manera sencilla. Un mock es una función simulada que reemplaza una función real, mientras que un spy es una función que registra información sobre las llamadas a una función.

Para crear un mock de una librería o módulo, se puede utilizar la función `jest.mock`. Jest reemplazará automáticamente la implementación real con el mock, lo que permite simular el comportamiento de la función o módulo. Otra consideración importante es que Jest permite especificar el valor de retorno de un mock utilizando las funciones `mockResolvedValue` y `mockRejectedValue` para simular respuestas exitosas y errores, respectivamente.

A continuación se muestra un ejemplo de cómo utilizar mocks en Jest para probar la función `fetchData`:

```javascript
// fetchData.test.js
const fetchData = require('./fetchData');
const axios = require('axios');

jest.mock('axios');

describe('fetchData', () => {
  test('Mocked fetchData', async () => {
    const data = { id: 1, name: 'John Doe' };
    axios.get.mockResolvedValue({ data });

    const result = await fetchData('https://pokeapi.co/api/v2/pokemon-form/1/');
    expect(result).toEqual(data);
  });

  test('Handles error with mocked fetchData', async () => {
    const error = new Error('Failed to fetch data');
    axios.get.mockRejectedValue(error);

    const result = await fetchData('https://pokeapi.co/api/v2/pokemon-form/1/');
    expect(result).toBeNull();
  });
});
```

Por otro lado, un spy se puede utilizar para verificar si una función ha sido llamada y con qué argumentos o para hacer mock de una función y modificar su comportamiento.

```javascript
// fetchData.test.js
const fetchData = require('./fetchData');

describe('fetchData', () => {
  test('Mocked fechData', async () => {
    const axiosSpy = jest.spyOn(axios, 'get');
    const data = { id: 1, name: 'John Doe' };
    axiosSpy.mockResolvedValue({ data });

    const result = await fetchData('https://pokeapi.co/api/v2/pokemon-form/1/');
    expect(result).toEqual(data);
    expect(axiosSpy).toHaveBeenCalledWith('https://pokeapi.co/api/v2/pokemon-form/1/');
  });

  test('Handles error with mocked fetchData', async () => {
    const axiosSpy = jest.spyOn(axios, 'get');
    const error = new Error('Failed to fetch data');
    axiosSpy.mockRejectedValue(error);

    const result = await fetchData('https://pokeapi.co/api/v2/pokemon-form/1/');
    expect(result).toBeNull();
    expect(axiosSpy).toHaveBeenCalledWith('https://pokeapi.co/api/v2/pokemon-form/1/');
  });
});
```
Dado que spyOn aparentemente realiza lo mismo que mock, ¿cuál es la diferencia entre ellos? 

Retornemos a los test donde se utilizó mock:
```javascript
// fetchData.test.js
const fetchData = require('./fetchData');
const axios = require('axios');

jest.mock('axios');

describe('fetchData', () => {
  test('Mocked fetchData', async () => {
    const data = { id: 1, name: 'John Doe' };
    axios.get.mockResolvedValue({ data });

    const result = await fetchData('https://pokeapi.co/api/v2/pokemon-form/1/');
    expect(result).toEqual(data);
  });

  test('Handles error with mocked fetchData', async () => {
    const error = new Error('Failed to fetch data');
    axios.get.mockRejectedValue(error);

    const result = await fetchData('https://pokeapi.co/api/v2/pokemon-form/1/');
    expect(result).toBeNull();
  });
});
```

A esa test suite agreguemos un test más:
```javascript
test('Original fetchData', async () => {

    const result = await fetchData('https://pokeapi.co/api/v2/pokemon-form/1/');
    expect(result).toEqual({"form_name":"","form_names":[],"form_order":1,"id":1,"is_battle_only":false,"is_default":true,"is_mega":false,"name":"bulbasaur","names":[],"order":1,"pokemon":{"name":"bulbasaur","url":"https://pokeapi.co/api/v2/pokemon/1/"},"sprites":{"back_default":"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/1.png","back_female":null,"back_shiny":"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/shiny/1.png","back_shiny_female":null,"front_default":"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/1.png","front_female":null,"front_shiny":"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/shiny/1.png","front_shiny_female":null},"types":[{"slot":1,"type":{"name":"grass","url":"https://pokeapi.co/api/v2/type/12/"}},{"slot":2,"type":{"name":"poison","url":"https://pokeapi.co/api/v2/type/4/"}}],"version_group":{"name":"red-blue","url":"https://pokeapi.co/api/v2/version-group/1/"}});
  });
```
¿Qué sucede con el test?

El test falla, ya que axios.get conserva el valor que se le asignó en el test anterior, por lo que no se realiza la llamada a la API y el resultado esperado no es el correcto.

¿Cómo se puede solucionar este problema?
Para recuperar la implementación original de una función o módulo, se puede utilizar spyOn para crear un mock temporal y restaurar la implementación original después de cada prueba utilizando el método `mockRestore`.

```javascript
// fetchData.test.js
const fetchData = require('./fetchData');
const axios = require('axios');

describe('fetchData', () => {
  
  test('Mocked fetchData', async () => {
    const axiosSpy = jest.spyOn(axios, 'get');
    const data = { id: 1, name: 'John Doe' };
    axiosSpy.mockResolvedValue({ data });

    const result = await fetchData('https://pokeapi.co/api/v2/pokemon-form/1/');
    expect(result).toEqual(data);
    expect(axiosSpy).toHaveBeenCalledWith('https://pokeapi.co/api/v2/pokemon-form/1/');

    axiosSpy.mockRestore();
  });

  test('Original fetchData', async () => {

    const result = await fetchData('https://pokeapi.co/api/v2/pokemon-form/1/');
    expect(result).toEqual({"form_name":"","form_names":[],"form_order":1,"id":1,"is_battle_only":false,"is_default":true,"is_mega":false,"name":"bulbasaur","names":[],"order":1,"pokemon":{"name":"bulbasaur","url":"https://pokeapi.co/api/v2/pokemon/1/"},"sprites":{"back_default":"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/1.png","back_female":null,"back_shiny":"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/shiny/1.png","back_shiny_female":null,"front_default":"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/1.png","front_female":null,"front_shiny":"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/shiny/1.png","front_shiny_female":null},"types":[{"slot":1,"type":{"name":"grass","url":"https://pokeapi.co/api/v2/type/12/"}},{"slot":2,"type":{"name":"poison","url":"https://pokeapi.co/api/v2/type/4/"}}],"version_group":{"name":"red-blue","url":"https://pokeapi.co/api/v2/version-group/1/"}});
  });
});
```

Otra forma de solucionar el problema es utilizando `jest.restoreAllMocks()` dentro de un `afterEach` para restaurar todas las implementaciones de mocks creadas con `jest.spyOn` después de cada prueba.

```javascript
// fetchData.test.js
const fetchData = require('./fetchData');
const axios = require('axios');

describe('fetchData', () => {

  afterEach(() => {
    jest.restoreAllMocks();
  });

  test('Mocked fetchData', async () => {
    const axiosSpy = jest.spyOn(axios, 'get');
    const data = { id: 1, name: 'John Doe' };
    axiosSpy.mockResolvedValue({ data });

    const result = await fetchData('https://pokeapi.co/api/v2/pokemon-form/1/');
    expect(result).toEqual(data);
    expect(axiosSpy).toHaveBeenCalledWith('https://pokeapi.co/api/v2/pokemon-form/1/');
  });

  test('Original fetchData', async () => {

    const result = await fetchData('https://pokeapi.co/api/v2/pokemon-form/1/');
    expect(result).toEqual({"form_name":"","form_names":[],"form_order":1,"id":1,"is_battle_only":false,"is_default":true,"is_mega":false,"name":"bulbasaur","names":[],"order":1,"pokemon":{"name":"bulbasaur","url":"https://pokeapi.co/api/v2/pokemon/1/"},"sprites":{"back_default":"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/1.png","back_female":null,"back_shiny":"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/shiny/1.png","back_shiny_female":null,"front_default":"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/1.png","front_female":null,"front_shiny":"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/shiny/1.png","front_shiny_female":null},"types":[{"slot":1,"type":{"name":"grass","url":"https://pokeapi.co/api/v2/type/12/"}},{"slot":2,"type":{"name":"poison","url":"https://pokeapi.co/api/v2/type/4/"}}],"version_group":{"name":"red-blue","url":"https://pokeapi.co/api/v2/version-group/1/"}});
  });
});
```







