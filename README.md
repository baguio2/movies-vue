# List Movies
Listado de Películas
  - La películas se muestra en una tabla, componente aislado.
  - Se puede realizar un orden ascendente o descente en cada columna.
  - Se puede buscar por título
  - Se ha incluido un componente de paginación por página(15 películas por página) para mejorar el rendimiento de la muestra de tablas
  - El listado se recoge de la dirección
    - https://raw.githubusercontent.com/getmanfred/codechallenges/main/vue/movies.json

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Run your unit tests
```
yarn test:unit
```

### Lints and fixes files
```
yarn lint
```

## Component Table
Componente para mostrar un listado de elementos. 
Presionando sobre el título de cada columna ordena los elementos de forma ascendente o descendente.

### Inputs
- Rows: Array de elementos para mostrar en el listado.
- Header: Array de cabeceras ordenaras para mostrar en el listado.

### Example
```
  <Table
    :rows="infoPage"
    :headers="headers"
  />
```


