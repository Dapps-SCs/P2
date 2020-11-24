# P2: se añade y se testea las funcionalidades de decr() y reset()

## Autores:

Carlos Aznar
Salomón Fereres
Adrián Blázquez

## Tareas:

0. Inicio:

¿Qué arquitectura presenta la aplicación?

Client <-> Business Logic

En este ejemplo, ¿qué archivo hace qué función en la arquitectura?

 dapp (app.js + index.html) <-> Web3 <-> Contador.sol

¿Dónde se despliega cada uno?

Serve + truffle + ganache

1. instalo ganache e inicializo un workspace con el trufle.config.js

2. Instalo truffle y comrpeubo la versión; enotnces compilo el contrato y lo migro
```
npm install truffle 
npx truffle version
```

```
npx truffle compile --all
npx truffle migrate --reset
```

3. Instalo serve

1. [ ] Modificar Contador.sol

2. [ ] Tests

- decr
- reset

3. [ ] Dos botones

Instrucciones

1. Clonar el proyecto
