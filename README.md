# ESLint

## Objetivo

Esse eslint foi criado com o intuito de padronizar e implementar boas práticas para os códigos Javascript

## Regras
### [accessor-pairs](https://eslint.org/docs/rules/accessor-pairs)

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

### [array-bracket-newline](https://eslint.org/docs/rules/array-bracket-newline)

- Quando for criado um array onde os valores serão inicializados no momento da criação do array acima de 4 itens o array deve ser quebrado em multi-linhas onde cada item irá permanecer em uma linha e sendo finalizado por vírgula.

```javascript
const numbers = [1, 2, 3];
const otherNumbers = [1, 2, 3, 4];
```

### [array-bracket-spacing](https://eslint.org/docs/rules/array-bracket-spacing)

- O array deverá conter espaço entre seus elementos e os colchetes, caso o array tiver apenas um elemento o espaço não será necessário.

```javascript
const array = [];
const array = [1, 2, 3];
const array = [1, 2, 3, 4];
```

### [array-callback-return](https://eslint.org/docs/rules/array-callback-return)

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

### [arrow-body-style](https://eslint.arrow-body-style/func-name-matching)

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
### [arrow-parens](https://eslint.org/docs/rules/arrow-parens)
- Parâmetro(s) de uma arrow function deverá **sempre** ter parênteses

```javascript
() => {};
(a) => {};
(a) => a;
(a) => {'\n'}
a.then((foo) => {});
a.then((foo) => { /* do something */ });
```

### [arrow-spacing](https://eslint.org/docs/rules/arrow-spacing)
- Em volta da seta de uma arrow function deverá conter 1 espaço, antes e depois.

```javascript
// Good
(a) => {};

// Bad
(a)=>{};
```

### [block-scoped-var](https://eslint.org/docs/rules/block-scoped-var)
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

### [block-spacing](https://eslint.org/docs/rules/block-spacing)
- Caso seja definido um bloco em uma única linha deverá conter espaço separando as chaves do corpo.

```javascript
function foo() { return true; }
if (foo) { bar = 0; }
```

### [brace-style](https://eslint.org/docs/rules/brace-style)
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

### [callback-return](https://eslint.org/docs/rules/callback-return)
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

### [camelcase](https://eslint.org/docs/rules/camelcase)
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

### [class-methods-use-this](https://eslint.class-methods-use-this/func-name-matching)
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

### [comma-dangle](https://eslint.org/docs/rules/comma-dangle)
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

### [comma-spacing](https://eslint.org/docs/rules/comma-spacing)
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

### [comma-style](https://eslint.org/docs/rules/comma-style)
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

### [computed-property-spacing](https://eslint.computed-property-spacing/func-name-matching)
- Quando for acessar uma propriedade de um objeto usando `[]` não deverá conter espaço entre os colchetes e a propriedade.

```javascript
obj[foo]
obj['foo']
var x = {[b]: a}
obj[foo[bar]]
```

### [consistent-return](https://eslint.org/docs/rules/consistent-return)
- Caso sua função necessite de um retorno o mesmo deverá ser consistente, ou seja, sua função deverá retornar um valor, do contrário não será necessário dar um `return` vazio.

```javascript
function doSomething(condition) {
  if (condition) {
    return true;
  } else {
    return false;
  }
}

function Foo() {
  if (!(this instanceof Foo)) {
    return new Foo();
  }

  this.a = 0;
}
```

### [curly](https://eslint.org/docs/rules/curly)
- Sempre que for utilizar alguma estrutura como `if`, `while` ou `for` deverá utilizar chaves para definir o escopo do bloco, mesmo Javascript permitindo utilizar apenas uma linha não é uma boa prática omitir as chaves.

```javascript
if (foo) {
  foo++;
}

while (bar) {
  baz();
}

if (foo) {
  baz();
} else {
  qux();
}
```

### [dot-location](https://eslint.org/docs/rules/dot-location)
- Caso queira por organização acessar uma propriedade de um objeto e colocar cada propriedade em uma linha, o ponto deverá vir antes do nome da propriedade podendo também utilizar na mesma linha, conforme o exemplo abaixo:.

```javascript
var foo = object
  .property;

var bar = object.property;
```

### [dot-notation](https://eslint.org/docs/rules/dot-notation)
- No Javascript é possível acessar uma propriedade de um objeto utilizando o ponto `.` e colchetes `[]`, porém por ser mais legível e menos verbososo é para ser utilizado o ponto, com exceção de caso seja utilizado o valor de uma variável para acessar a propriedade.

```javascript
var x = foo.bar;

var x = foo[bar];
```

### [eol-last](https://eslint.org/docs/rules/eol-last)
- Adicionar uma linha vazia no final do arquivo é uma boa prática geralmente de sistemas UNIX, pois facilita quando for preciso concatenar ou adicionar a saída de algum comando ao final do arquivo.

```javascript
function doSmth() {
  var foo = 2;
}\n
```

### [eqeqeq](https://eslint.org/docs/rules/eqeqeq)
- É considerado boa prática utilizar os operadores `===` e `!==` ao invés dos operadores de comparação `==` e `!=`, porque com eles você consegue validar o além do valor o tipo dos dados, porque no Javascript comparações como as seguintes são consideradas como `true`:

  - [] == false
  - [] == ![]
  - 3 == "03"

```javascript
a === b
foo === true
bananas !== 1
value === undefined
typeof foo === 'undefined'
'hello' !== 'world'
0 === 0
true === true
foo === null
```

### [func-call-spacing](https://eslint.org/docs/rules/func-call-spacing)
- Não será permitido inserir um espaço entre o nome da função e os parênteses na sua chamada.

```javascript
fn();
```

### [func-name-matching](https://eslint.org/docs/rules/func-name-matching)
- Essa regra define que uma função não precisa ter o mesmo nome da variável que ela for atribuída.

```javascript
var foo = function bar() {};
var foo = function() {};
var foo = () => {};
foo = function bar() {};

obj.foo = function bar() {};
obj['foo'] = function bar() {};
obj['foo//bar'] = function foo() {};
obj[foo] = function foo() {};

var obj = {foo: function bar() {}};
var obj = {[foo]: function foo() {}};
var obj = {'foo//bar': function foo() {}};
var obj = {foo: function() {}};

obj['x' + 2] = function bar(){};
var [ bar ] = [ function bar(){} ];
({[foo]: function bar() {}})

module.exports = function foo(name) {};
module['exports'] = function foo(name) {};
```

### [func-names](https://eslint.org/docs/rules/func-names)
- Quando for necessário atribuir a uma variável uma função não será permitido nomear a função, basta atribuí-la à variável.

```javascript
Foo.prototype.bar = function() {};

(function() {
  // ...
}())
```

### [func-style](https://eslint.org/docs/rules/func-style)
- Quando for necessário criar uma função a mesma deverá ser declarada, essa regra se aplica para `arrow functions`.

```javascript
function foo() {
  // ...
}

// Methods (functions assigned to objects) are not checked by this rule
SomeObject.foo = function() {
  // ...
};

var foo = () => {};
```

### [function-paren-newline](https://eslint.org/docs/rules/function-paren-newline)
- Não será permitido colocar os parâmetros de uma função em multi-linhas.

```javascript
function foo(bar, baz) {}

var foo = function(bar, baz) {};

var foo = (bar, baz) => {};

foo(bar, baz);
```

### [generator-star-spacing](https://eslint.org/docs/rules/generator-star-spacing)
- Ao criar uma função ou método [Generator](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Generator) o asterisco deverá conter um espaço antes e logo após deverá vir o nome da função ou método.

```javascript
function *generator() {}

var anonymous = function *() {};

var shorthand = { *generator() {} };
```

### [global-require](https://eslint.org/docs/rules/global-require)
