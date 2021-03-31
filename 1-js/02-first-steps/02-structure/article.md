# A kód struktúra

A legelső dolgok amikről tanulni fogunk, azok a kódolás építő kövei.

## Utasítások

Az utasítások azok szintaktikai struktúrák amelyek parancsokat hajtanak végre.

Már láttunk egy ilyen utasítást, a(z) `alert('Hello, világ!')`-t, ami egy pop-up-ban kiírja, hogy "Hello, világ!".

A kódunkba annyi utasítást tehetünk ahányat csak akarunk. Ezeket az utasításokat pontosvesszővel választjuk el egymástól.

Ebben a példában a "Hello World" üzenetet 2 külön alert utasításra osztjuk:

```js run no-beautify
alert('Hello'); alert('World');
```

Az utasítások általában külön sorokba írjuk, hogy könnyebben olvashatók legyenek:

```js run no-beautify
alert('Hello');
alert('World');
```

## A pontosvessző [#semicolon]

Amennyiben a parancsok külön sorokba vannak osztva, a pontosvessző elhanyagolható.

Ez a kód blokk is hiba nélkül fog lefutni:

```js run no-beautify
alert('Hello')
alert('World')
```

Itt a JavaScript az új sorokra egy úgynevezett "láthatatlan pontosvesszőként" tekint. Ezt [automatikus pontosvessző kihejezés](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion)-nek nevezzük.

**A leghtöbb esetben egy új sor egy pontosvesszőt jelképez. De a "legtöbb esetben" nem jelenti azt, hogy ez "mindig" így van!**

Bizonyos esetekben egy új sor nem egyenlő egy pontosvesszővel. Például:

```js run no-beautify
alert(3 +
1
+ 2);
```

A kód `6`-ot ad vissza, mivel a JavaScript itt nem veszi az új sort pontosvesszőnek. Hiszen, magától adódik, hogy ha a sor egy `"+"` jellel végződik akkor az egy befejeztlen parancs, tehát a pontosvessző nem kell. Ebben az esetben a kód az elvárásoknak megfelelően fog működni.

**De viszont előfordul, hogy a JavaScriptnek "elfelejt" az új sorokra pontos vesszőként tekinteni**

Az ilyen problémák miatt fellépő hibák nagyon zavaróak, tekintve hogy nehéz megtalálni és kijavítani őket.

````smart header="Példa egy ilyen hibára"
Ha esetleg kíváncsi vagy, hogy ilyen hibát képező kód blokk hogy néz ki pontosan, akkor itt lenne egy:

```js run
[1, 2].forEach(alert)
```

A szögletes zárójelekkel `[]` és a `forEach`-el egyelőre ne foglalkozz. Arra majd kitérünk később. Egyelőre ennek a kód blokknak az eredményét jegyezzük meg, ami egy `1`-es és egy `2`-es.

Na akkor tegyünk egy `alert` utasítást a sor elejére és **ne** használjunk pontosvesszőt.

```js run no-beautify
alert("Itt egy hiba lesz!")

[1, 2].forEach(alert)
```

Hogyha az előbbi kód blokkot lefutatjuk az eredmény az "Itt egy hiba lesz!" felirat és egy hiba lesz!

De ha az `alert` után teszünk pontosvesszőt minden megoldódik:
```js run
alert("Mostmár minden rendben");

[1, 2].forEach(alert)  
```

Mostmár a "Mostmár minden rendben" üzenetet, majd az `1` és `2` számokat fogjuk kapni eredményül.


Ez a jiba azért történik, mivel a JavaScript sosem tesz szögletes zárójelek `[...]` elé pontosvesszőt automatikusan.

So, because the semicolon is not auto-inserted, the code in the first example is treated as a single statement. Here's how the engine sees it:

```js run no-beautify
alert("There will be an error")[1, 2].forEach(alert)
```

But it should be two separate statements, not one. Such a merging in this case is just wrong, hence the error. This can happen in other situations.
````

We recommend putting semicolons between statements even if they are separated by newlines. This rule is widely adopted by the community. Let's note once again -- *it is possible* to leave out semicolons most of the time. But it's safer -- especially for a beginner -- to use them.

## Comments [#code-comments]

As time goes on, programs become more and more complex. It becomes necessary to add *comments* which describe what the code does and why.

Comments can be put into any place of a script. They don't affect its execution because the engine simply ignores them.

**One-line comments start with two forward slash characters `//`.**

The rest of the line is a comment. It may occupy a full line of its own or follow a statement.

Like here:
```js run
// This comment occupies a line of its own
alert('Hello');

alert('World'); // This comment follows the statement
```

**Multiline comments start with a forward slash and an asterisk <code>/&#42;</code> and end with an asterisk and a forward slash <code>&#42;/</code>.**

Like this:

```js run
/* An example with two messages.
This is a multiline comment.
*/
alert('Hello');
alert('World');
```

The content of comments is ignored, so if we put code inside <code>/&#42; ... &#42;/</code>, it won't execute.

Sometimes it can be handy to temporarily disable a part of code:

```js run
/* Commenting out the code
alert('Hello');
*/
alert('World');
```

```smart header="Use hotkeys!"
In most editors, a line of code can be commented out by pressing the `key:Ctrl+/` hotkey for a single-line comment and something like `key:Ctrl+Shift+/` -- for multiline comments (select a piece of code and press the hotkey). For Mac, try `key:Cmd` instead of `key:Ctrl` and `key:Option` instead of `key:Shift`.
```

````warn header="Nested comments are not supported!"
There may not be `/*...*/` inside another `/*...*/`.

Such code will die with an error:

```js run no-beautify
/*
  /* nested comment ?!? */
*/
alert( 'World' );
```
````

Please, don't hesitate to comment your code.

Comments increase the overall code footprint, but that's not a problem at all. There are many tools which minify code before publishing to a production server. They remove comments, so they don't appear in the working scripts. Therefore, comments do not have negative effects on production at all.

Later in the tutorial there will be a chapter <info:code-quality> that also explains how to write better comments.
