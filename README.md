# ESLint


## Objetivo
----

Esse eslint foi criado com o intuito de padronizar e implementar boas práticas para os códigos Javascript

## Regras
----
### accessor-pairs

- Para todo `get` de um atributo que é implementado em uma classe/objeto deverá ter um `set`, porém caso seja necessário apenas um `set` o `get` não é obrigatório.

```javascript
const object = {
  set a(value) {
    this.val = value;
  },
  get a() {
    return this.val;
  }
};

class Person {
  constructor(name) {
    this._name = name;
  }

  get name() {
    return this._name;
  }

  set name(value) {
    this._name = value;
  }
}
```

### array-bracket-newline

- Quando for criado um array onde os valores serão inicializados no momento da criação do array acima de 4 itens o array deve ser quebrado em multi-linhas onde cada item irá permanecer em uma linha e sendo finalizado por vírgula.

```javascript
const numbers = [1, 2, 3];
const otherNumbers = [1, 2, 3, 4];
```

### array-bracket-spacing

- O array deverá conter espaço entre seus elementos e os colchetes, caso o array tiver apenas um elemento o espaço não será necessário.

```javascript
const array = [];
const array = [1, 2, 3];
const array = [1, 2, 3, 4];
```

### array-callback-return

- Essa regra obriga que o callback de métodos de array tenham o `return`, pois em alguns métodos é necessário o retorno de algum valor, caso contrário será retornado `undefined`.
- Métodos que essa regra se aplica:
  - Array.from
  - Array.prototype.every
  - Array.prototype.filter
  - Array.prototype.find
  - Array.prototype.findIndex
  - Array.prototype.map
  - Array.prototype.reduce
  - Array.prototype.reduceRight
  - Array.prototype.some
  - Array.prototype.sort

```javascript
const indexMap = myArray.reduce(function(memo, item, index) {
  memo[item] = index;
  return memo;
}, {});

const foo = Array.from(nodes, function(node) {
  return node.tagName === "DIV";
});

const bar = foo.map(node => node.getAttribute("id"));
```

### arrow-body-style `as-needed`

- Essa regra define que uma arrow function deve ter seu corpo definido quando for necessário, ou seja, se o retorno da arrow function pode ser feito logo em seguida da seta `=>` o corpo não é necessário.

```javascript
let foo = () => 0;
let foo = (retv, name) => {
  retv[name] = true;
  return retv;
};
let foo = () => ({
  bar: {
      foo: 1,
      bar: 2,
  }
});
let foo = () => { bar(); };
let foo = () => {};
let foo = () => { /* do nothing */ };
let foo = () => {
  // do nothing.
};
```