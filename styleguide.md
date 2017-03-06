#StyleGuide

##TypeScript {#typescript}

1. [Comandos basicos](styleguide.md#T1)
2. [Do & Don'ts](styleguide.md#T2)
    * [1.Nomes](styleguide.md#nomes)
    * [2.Tipos - `number`, `string`,`boolean`, `any` VS `Number`, `String`, `Boolean` e `Object`](styleguide.md#tipos)
    * [3.`null` vs. `undefined`](styleguide#nullvsundefined)
    * [4.Ficheiros auto-gerados `".generated.*`](styleguide.md#files)
    * [5.Imutabilidade](styleguide.md#imutabilidade)
    * [6.Callback Types](styleguide.md#callbacktypes)
    * [7. Parâmetros Opcionais em Callbacks](styleguide.md#callbacktypes2)
    * [8. Overloads e Callbacks](styleguide.md#overloads)
    * [9. Ordenação](styleguide.md#ordem)
    * [10. Evitar arrasto de pârametros através de opcionais](styleguide.md#arrasto)
    * [11. Union Types (ex: `number|string`)](styleguide.md#union)

[Documentação Oficial](https://www.typescriptlang.org/docs/tutorial.html)


####1. Comandos basicos {#T1}

1. Instalar
```
npm install -g typescript
```

2. Verificar a versão
```
tsc -v
Version 1.8.10
```

3. Compilar em javascript
```
tsc main.ts
```
Irá gerar o ficheiro `main.js`

4. Outros comandos

Compila vários ficheiros em simultâneo, gerando main.js e worker.js.
```
tsc main.ts worker.ts    
```

Compila todos os ficheiros .ts na pasta atual. Não funciona recursivamente
```
tsc *.ts
```

`--watch` compila automaticamente o ficheiro TypeScript sempre que forem feitas alterações
```
# Initializes a watcher process that will keep main.js up to date.
tsc main.ts --watch
```


### Do & Don'ts  {#T2}

####1. Nomes {#nomes}

1. Usar PascalCase para type names.
    
2. Não usar "I" como prefixo pra interface names.
    
3. Usar PascalCase para enum values.
    
4. Usar camelCase para nomes de funções.
  
5. Usar camelCase para nomes de propriedades e variáveis locais.
    
6. Não utilizar "_" como prefixo para propriedades privadas.
    
7. Utilizar palavras completas em nomes, sempre que possivel.

####2. Tipos: `number`, `string`,`boolean`, `any` VS `Number`, `String`, `Boolean` e `Object` {#tipos}
Nunca use os tipos `Number`, `String`, `Boolean` ou `Object`. Esses tipos referem-se a objetos não-primitivos que quase nunca são usados adequadamente em código JavaScript.

```typescript

/* WRONG */
function reverse(s: String): String;

```

Use os tipos number, string, and boolean.

```typescript

/* OK */
function reverse(s: string): string;

```

**Dica***: Em vez de usar o tipo `Object` poderá utilizar o tipo `any`. Por vezes um tipo só é conhecido no runtime. Nestas situações, pode usar o tipo `any`


Não introduzir novos types/valores no global namespace.

Types partilhados devem ser definidos em 'types.ts'.

Num ficheiro, definições de type devem aparecer primeiro.

###3. `Null` não é nosso amigo {#nullvsundefined}
Utilizar `undefined` em vez de `null`  ([*`null` vs. `undefined` in TypeScript land by Basarat*](https://medium.com/@basarat/null-vs-undefined-in-typescript-land-dc0c7a5f240a#.mcq4te64w))


####4. Ficheiros auto-gerados `".generated.*` {#files}

Apenas um ficheiro por componente lógico (e.g. parser, scanner, emitter, checker).

Ficheiros com sufixo ".generated.*" são auto-gerados, não os edite manualmente.

###5. Imutabilidade (#imutabilidade)
Considere objetos como Nodes, Símbolos, etc. são imutáveis fora do componente que os criou. Não os mude.
Considere arrays como imutáveis por padrão após a criação.

####6. Callback Types {#callbacktypes}
Não usar o tipo `any` para callbacks cujo valor será ignorado
```typescript
/* WRONG */
function fn(x: () => any) {
    x();
}
```
Em vez de `any`, usar o tipo `void`, pois é mais seguro,impede o uso acidental do valor de retorno de x, de uma maneira não controlada.
```typescript
/* OK */
function fn(x: () => void) {
    x();
}
```

Exemplo do uso correcto de `void`:
```typescript
function fn(x: () => void) {
    var k = x(); // oops! meant to do something else
    k.doSomething(); // error, but would be OK if the return type had been 'any'
}
```

####7. Parâmetros Opcionais em Callbacks {#callbacktypes2}
Não usar parâmetros opcionais em callbacks, a não ser que sejam efetivamente opcionais. ([Ver abaixo](styleguide.md#arrasto))

####8. Overloads e Callbacks {#overloads}
Não escrever overloads separadas que diferem apenas no número de argumentos do callback. É preferivel escrever apenas um overload com o máximo número de argumentos.
```typescript
/* WRONG */
declare function beforeAll(action: () => void, timeout?: number): void;
declare function beforeAll(action: (done: DoneFn) => void, timeout?: number): void;
```

Um callback pode sempre desconsiderar um parâmetro, pelo que não há necessidade de ter um overload mais curto. Assim, evita-se que funções digitadas incorretamente sejam passadas por corresponderem ao primeiro overload.

```typescript
/* OK */
declare function beforeAll(action: (done: DoneFn) => void, timeout?: number): void;
```

####9. Ordenação {#ordem}
É recomendado não colocar overloads gerais antes de overload especificos.
Na resolução de funções, Typescript escolhe o primeiro overload correspondente (*first matching overload*). Quando o overload interpretado é mais geral, as seguintes são ocultadas, não sendo chamadas.
```typescript
/* WRONG */
declare function fn(x: any): any;  //geral
declare function fn(x: HTMLElement): number;  //específico
declare function fn(x: HTMLDivElement): string; //específico

var myElem: HTMLDivElement;
var x = fn(myElem); // x: any, wat?
```

```typescript
/* OK */
declare function fn(x: HTMLDivElement): string; //específico
declare function fn(x: HTMLElement): number; //específico
declare function fn(x: any): any; //geral

var myElem: HTMLDivElement;
var x = fn(myElem); // x: string, :)
```

####10. Evitar arrasto de pârametros através de opcionais {#arrasto}
Não escrever overloads que diferem apenas em parâmetros de arrasto.

```typescript
/* WRONG */
interface Example {
    diff(one: string): number;
    diff(one: string, two: string): number;
    diff(one: string, two: string, three: boolean): number;
}
```
Quanto têm o mesmo return type, é preferivel utilizar parâmetros opcionais:
```typescript
/* OK */
interface Example {
    diff(one: string, two?: string, three?: boolean): number;
}
```

####11. Union Types (ex: `number|string`) {#union}
Não escrever overloads que diferem apenas no tipo, em apenas uma posição de argumento.

```typescript
/* WRONG */
interface Moment {
    utcOffset(): number;
    utcOffset(b: number): Moment;
    utcOffset(b: string): Moment;
}
```

Em vez disso, utilizar union types, pois permite ter um valor com varias representações ou formatos na mesma posição de memória.

```typescript
/* OK */
interface Moment {
    utcOffset(): number;
    utcOffset(b: number|string): Moment;
}
```

Tal nomemclatura é importante para quando se está a passar um valor à função:
```typescript
function fn(x: string): void;
function fn(x: number): void;
function fn(x: number|string) {
    // When written with separate overloads, incorrectly an error
    // When written with union types, correctly OK
    return moment().utcOffset(x);
```

