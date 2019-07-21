# ESLint

## Objetivo

Esse eslint foi criado com o intuito de padronizar e implementar boas práticas para os códigos Javascript

## Regras
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
### arrow-parens
- Parâmetro(s) de uma arrow function deverá **sempre** ter parênteses

```javascript
() => {};
(a) => {};
(a) => a;
(a) => {'\n'}
a.then((foo) => {});
a.then((foo) => { /* do something */ });
```

### arrow-spacing
- Em volta da seta de uma arrow function deverá conter 1 espaço, antes e depois.

```javascript
// Good
(a) => {};

// Bad
(a)=>{};
```

### block-scoped-var
- Essa regra define que é proibido acessa uma variável fora de seu escopo de declaração.

```javascript
function doIf() {
  var build;

  if (true) {
      build = true;
  }

  console.log(build);
}

function doIfElse() {
  var build;

  if (true) {
      build = true;
  } else {
      build = false;
  }
}

function doTryCatch() {
  var build;
  var f;

  try {
      build = 1;
  } catch (e) {
      f = build;
  }
}
```

### block-spacing
- Caso seja definido um bloco em uma única linha deverá conter espaço separando as chaves do corpo.

```javascript
function foo() { return true; }
if (foo) { bar = 0; }
```

### brace-style
- Ao iniciar um bloco de uma função ou qualquer outra estrutura as chaves deverãos ser abertas logo após a declaração da estrutura com 1 tab de espaçamento entre ambos.

```javascript
function foo() {
  return true;
}

if (foo) {
  bar();
}

if (foo) {
  bar();
} else {
  baz();
}

try {
  somethingRisky();
} catch(e) {
  handleError();
}
```
**Obs.:** Essa regra permite que seja criado o corpo das estruturas em uma linha, porém deverão respeitar a regra [block-spacing](https://github.com/nelsonsinis/eslint-ioasys#block-spacing)

### callback-return
- Para evitar que um `callback` seja chamado diversas vezes podendo gerar erros é necessário fazer o uso do `return`, assim terá maior controle do fluxo que sua função irá seguir e evitando possíveis erros.
- Para que o eslint possa identificar que seu parâmetro é um callback sua função deverá seguir o seguinte padrão de nomes:
  - callback
  - cb
  - next
  - done

```javascript
function foo(err, callback) {
    if (err) {
        return callback(err);
    }
    callback();
}
```

### camelcase
- Como o Javascript é uma linguagem baseada nos padrões da linguagem C suas variáveis, propriedades de objetos e nomes de funções terão que ser escritas em `camelCase`, com exceção apenas de nomes de classes que poderão iniciar com a primeira letra maiúscula.

```javascript
import { no_camelcased as camelCased } from "external-module";

var myFavoriteColor   = "#112C85";
var _myFavoriteColor  = "#112C85";
var myFavoriteColor_  = "#112C85";
var MY_FAVORITE_COLOR = "#112C85";
var foo = bar.baz_boom;
var foo = { qux: bar.baz_boom };

obj.do_something();
do_something();
new do_something();

var { category_id: category } = query;

function foo({ isCamelCased }) {
    // ...
};

function foo({ isCamelCased: isAlsoCamelCased }) {
    // ...
}

function foo({ isCamelCased = 'default value' }) {
    // ...
};

var { categoryId = 1 } = query;

var { foo: isCamelCased } = bar;

var { foo: isCamelCased = 1 } = quz;
```

### class-methods-use-this
- Quando tiver um método de uma classe o mesmo deverá usar o `this` para acessar os atributos da classe, caso o método não precise acessar algum atributo o mesmo deverá ser estático.

```javascript
class A {
  constructor() {
    this.a = "hi";
  }

  print() {
    console.log(this.a);
  }

  static sayHi() {
    console.log("hi");
  }
}

A.sayHi(); // => "hi"
```

### comma-dangle
- Deverá ser inserido a vírgula `,` após os elementos de um array/objeto caso eles estejam em multi-linhas e desde que o último não seja seguido por `]` ou `}`.

```javascript
var foo = {
  bar: "baz",
  qux: "quux",
};

var foo = {bar: "baz", qux: "quux"};
var arr = [1,2];

var arr = [1,
  2];

var arr = [
  1,
  2,
];

foo({
  bar: "baz",
  qux: "quux",
});
```

### comma-spacing
- Sempre que for preciso separar elementos com vírgula deverá ser utilizado espaço depois da mesma, porém antes não deverá existir o espaço.

```javascript
var foo = 1, bar = 2
    , baz = 3;
var arr = [1, 2];
var arr = [1,, 3]
var obj = {"foo": "bar", "baz": "qur"};
foo(a, b);
new Foo(a, b);
function foo(a, b){}
a, b
```

### comma-style
- A vírgula deverá ser usada sempre após o elemento.

```javascript
var foo = 1, bar = 2;

var foo = 1,
  bar = 2;

var foo = ["apples",
  "oranges"];

function bar() {
  return {
    "a": 1,
    "b:": 2
  };
}
```

### computed-property-spacing
- Quando for acessar uma propriedade de um objeto usando `[]` não deverá conter espaço entre os colchetes e a propriedade.

```javascript
obj[foo]
obj['foo']
var x = {[b]: a}
obj[foo[bar]]
```

### consistent-return
