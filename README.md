<!--

author:   Andre Dietrich
email:    dietrich@ivs.cs.uni-magdeburg.de
version:  1.0.0
language: en
narrator: US English Female

script:   https://curiosity-driven.github.io/prolog-interpreter/parser.js
          https://curiosity-driven.github.io/prolog-interpreter/interpreter.js

@prolog_db
<script>
var rules = parser(lexer(`{{0}}`)).parseRules();
window['@0'] = new Database(rules);
"database loaded";
</script>
@end

@prolog_shell
<script>
var rslt = "";
var goal = parser(lexer(`{{0}}`)).parseTerm();
for (var item of window['@0'].query(goal)) {
    rslt += "Yes: " + item + "<br>";
}
if (rslt === "") {
   'No';
} else {
   rslt;
}
</script>
@end

@prolog_ui
```prolog
@2
```
@prolog_db(@0)


```prolog
@1
```
@prolog_shell(@0)
@end
-->

# Prolog template

Template for the JavaScript Prolog-Interpreter https://curiosity-driven.org/prolog-interpreter

## Plain HTML

** Load Database and Rules: **

```prolog
mother_child(trude, sally).

father_child(tom, sally).
father_child(tom, erica).
father_child(mike, tom).

sibling(X, Y)      :- parent_child(Z, X), parent_child(Z, Y).

parent_child(X, Y) :- father_child(X, Y).
parent_child(X, Y) :- mother_child(X, Y).
```
<script>
var rules = parser(lexer(`{{0}}`)).parseRules();
window['prolog_db'] = new Database(rules);

"database loaded";
</script>

** Queries **

```prolog
sibling(sally, erica).
```
<script>
var rslt = "";

var goal = parser(lexer(`{{0}}`)).parseTerm();

for (var item of window.prolog_db.query(goal)) {
    rslt += "Yes: " + item + "<br>";
}

if (rslt === "") {
   'No';
} else {
   rslt;
}
</script>


## Macros-Separated

```prolog
mother_child(trude, sally).

father_child(tom, sally).
father_child(tom, erica).
father_child(mike, tom).

sibling(X, Y)      :- parent_child(Z, X), parent_child(Z, Y).

parent_child(X, Y) :- father_child(X, Y).
parent_child(X, Y) :- mother_child(X, Y).
```
@prolog_db(db_name_whatever)

** Queries **

```prolog
sibling(sally, erica).
```
@prolog_shell(db_name_whatever)

## Full-Macro

```prolog
@prolog_ui(db_full_etc,`sibling(sally, erica).`)
mother_child(trude, sally).

father_child(tom, sally).
father_child(tom, erica).
father_child(mike, tom).

sibling(X, Y)      :- parent_child(Z, X), parent_child(Z, Y).

parent_child(X, Y) :- father_child(X, Y).
parent_child(X, Y) :- mother_child(X, Y).
```
