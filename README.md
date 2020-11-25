# P2: se añade y se testea las funcionalidades de decr() y reset()

## Autores:

Carlos Aznar
Salomón Fereres
Adrián Blázquez

Demo de la feature:

[![Demo de la feature](https://img.youtube.com/vi/3X_pqKg6xyM/0.jpg)](https://www.youtube.com/watch?v=3X_pqKg6xyM)

De sarrollo de cada requisito:

0. Análisis y diseño
1. 
- [x] Modificar Contador.sol
2.
- [x] Tests
3.
- [x] Dos botones y dos manejadores
B. Demo de la feature

## Tareas:

0. Análisis y diseño

¿Qué arquitectura presenta la aplicación?

Client <-> Business Logic

En este ejemplo, ¿qué archivo hace qué función en la arquitectura?

 dapp (app.js + index.html) <-> Web3 <-> Contador.sol

¿Dónde se despliega cada uno?

Serve + truffle + ganache

a.. instalo ganache e inicializo un workspace con el trufle.config.js

b Instalo truffle y comrpeubo la versión; enotnces compilo el contrato, lo migro y realizo tests.
```
npm install truffle 
npx truffle version
```

Output
```
aluche@aluche-VirtualBox:~/PycharmProjects/P2$ npx truffle version
Truffle v5.1.54 (core: 5.1.54)
Solidity - 0.7.4 (solc-js)
Node v10.19.0
Web3.js v1.2.9
```

```
npx truffle compile --all
npx truffle migrate --reset
npx truffle test
```
Output:
```
PS C:\Users\ablaz\PycharmProjects\BCDA\P2> npx truffle version                                                          Truffle v5.1.54 (core: 5.1.54)
Solidity - 0.7.4 (solc-js)
Node v12.16.1
Web3.js v1.2.9
PS C:\Users\ablaz\PycharmProjects\BCDA\P2> npx truffle compile --all

Compiling your contracts...
===========================
√ Fetching solc version list from solc-bin. Attempt #1
√ Downloading compiler. Attempt #1.
> Compiling .\contracts\Contador.sol
> Compiling .\contracts\Migrations.sol
> Artifacts written to C:\Users\ablaz\PycharmProjects\BCDA\P2\build\contracts
> Compiled successfully using:
   - solc: 0.7.4+commit.3f05b770.Emscripten.clang

PS C:\Users\ablaz\PycharmProjects\BCDA\P2> npx truffle migrate --reset

Compiling your contracts...
===========================
> Everything is up to date, there is nothing to compile.



Starting migrations...
======================
> Network name:    'development'
> Network id:      5777
> Block gas limit: 6721975 (0x6691b7)


1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > transaction hash:    0xb3533c05d07f3358fd08f1c13c53f6ffda955ba27388790febe55319585c5e88
   > Blocks: 0            Seconds: 0
   > contract address:    0x1d46fE6461Fe706576Be01C077F053F49BF8203F
   > block number:        1
   > block timestamp:     1606247463
   > account:             0x908a530710da2d270418Ba983ae001DC19B70012
   > balance:             99.99626074
   > gas used:            186963 (0x2da53)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.00373926 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00373926 ETH


1605356460_deploy_contador.js
=============================

   Deploying 'Contador'
   --------------------
   > transaction hash:    0x5b99441c05e721df06bb2aae5d9d047fd2f5959963db9bc1b633a29a40b7647f
   > Blocks: 0            Seconds: 0
   > contract address:    0x22DD5D035988ACA88aAa846d1b4b3060AE771C37
   > block number:        3
   > block timestamp:     1606247467
   > account:             0x908a530710da2d270418Ba983ae001DC19B70012
   > balance:             99.9908407
   > gas used:            228667 (0x37d3b)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.00457334 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00457334 ETH


Summary
=======
> Total deployments:   2
> Final cost:          0.0083126 ETH


PS C:\Users\ablaz\PycharmProjects\BCDA\P2> npx truffle test
Using network 'development'.


Compiling your contracts...
===========================
> Compiling .\test\TestContador.sol
> Compilation warnings encountered:

    /C/Users/ablaz/PycharmProjects/BCDA/P2/test/TestContador.sol: Warning: SPDX license identifier not provided in source file. Before publishing, consider adding a comment containing "SPDX-License-Identifier: <SPDX-License>" to each source file. Use "SPDX-License-Identifier: UNLICENSED" for non-open-source code. Please see https://spdx.org for more information.

> Artifacts written to C:\Users\ablaz\AppData\Local\Temp\test--13508-tSPK2J25MTH6
> Compiled successfully using:
   - solc: 0.7.4+commit.3f05b770.Emscripten.clang



  TestContador
    √ testZero (213ms)
    √ testIncr (438ms)

  Contract: Usamos un Contador:
    √ el valor inicial debe ser 0 (170ms)
    √ el valor inicial debe ser 0 (62ms)
    √ incrementar en uno el contador (235ms)
    √ incrementa en cuatro el contador (720ms)


  6 passing (17s)
```

c. Instalo las librerías necesrias para cliente y conecto con enlaces simbólicos las librerías

```
npm install web3 truffle-contract serve

```
Se estalbecen ciertos enlaces simbólicos para no tener que actualizar las librerías

```
cd dapp/js
ln -fs ../../node_modules/truffle-contract/dist/truffle-contract.min.js dapp/js
ln -fs ../build/contracts .
npx serve -S .
```

Se instala metamask

1. Modificar Contador.sol

```
    function decr() public {
        valor--;
        emit Tic("Decrementar", valor);
    }
    
    function reset() public {
        valor = 0;
        emit Tic("Reset", valor);
    }
```

2. Tests

- decr
- reset

```
    it("decrementar en uno el contador", () => {

    let c1, c2;

    return contador.valor.call()
    .then(value => {
      c1 = value;
      return contador.decr(); 
    })
    .then(() => contador.valor.call() )
    .then(value => {
      c2 = value;

      const decremento = c2.sub(c1);
      assert.equal(decremento.toNumber(), 1, "El decremento del valor no es 1.");
    });
  });
  
  it("decrementa en cuatro el contador", async () => {

    let c1 = await contador.valor.call();
    await contador.decr(); 
    await contador.decr(); 
    await contador.decr(); 
    await contador.decr(); 
    let c2 = await contador.valor.call();
 
    const decremento = c2.sub(c1);
    assert.equal(decremento.toNumber(), 4, "El decremento del valor no es 4.");
  });
  
    it("resetea el contador", async () => {

    let c1 = await contador.valor.call();
    await contador.reset(); 
 
    const valor = await contador.valor.call();
    assert.equal(valor.toNumber(), 0, "El valor no es 0.");
  });
```

Output:



3. Dos botones y dos manejadores

En index.html

```
    <button type="button" id="cincr">Incrementar</button>
    <button type="button" id="cdecr">Decrementar</button>
    <button type="button" id="creset">Reset</button>
```
En app.js

```
        // Manejador del botón de decremento.
    handleDecr: async event => { 
        console.log("Se ha hecho Click en el botón.");

        event.preventDefault();

        try {
            const accounts = await App.web3.eth.getAccounts();
            const account = accounts[0];

            if (!account) {
               alert('No se puede acceder a las cuentas de usuario.');
               return;
            }
            console.log("Cuenta =", account);

            // Ejecutar incr como una transacción desde la cuenta account.
            await App.contador.decr({from: account, gas: 200000});
        } catch(error) {
            console.log(error.message || error);
        }
    },
    
    // Manejador del botón de reset.
    handleDecr: async event => { 
        console.log("Se ha hecho Click en el botón.");

        event.preventDefault();

        try {
            const accounts = await App.web3.eth.getAccounts();
            const account = accounts[0];

            if (!account) {
               alert('No se puede acceder a las cuentas de usuario.');
               return;
            }
            console.log("Cuenta =", account);

            // Ejecutar incr como una transacción desde la cuenta account.
            await App.contador.reset({from: account, gas: 200000});
        } catch(error) {
            console.log(error.message || error);
        }
    },
```




