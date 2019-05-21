<!--

author:   André Dietrich
email:    andre.dietrich@ovgu.de
version:  0.0.2
language: en
narrator: US English Female

script:   https://curiosity-driven.github.io/prolog-interpreter/parser.js
          https://curiosity-driven.github.io/prolog-interpreter/interpreter.js

@Prolog.db
<script>
var rules = parser(lexer(`@input`)).parseRules();
window['@0'] = new Database(rules);
"database " + "@0" + " loaded";
</script>
@end

@Prolog.shell
<script>
var rslt = "";
var goal = parser(lexer(`@input`)).parseTerm();
for (var item of window['@0'].query(goal)) {
    rslt += "Yes: " + item + "\n";
}
if (rslt === "") {
   'No';
} else {
   rslt;
}
</script>
@end

@Prolog.ui
```prolog
@2
```
@Prolog.db(@0)


```prolog
@1
```
@Prolog.shell(@0)
@end
-->

# Curiosity-Prolog - Template

                         --{{0}}--
This document defines some basic macros for applying the JavaScript
Prolog-Interpreter https://curiosity-driven.org/prolog-interpreter interpreter
in [LiaScript](https://LiaScript.github.io) to make Prolog programs in Markdown
executeable and editable.

__Try it on LiaScript:__

https://liascript.github.io/course/?https://raw.githubusercontent.com/liaTemplates/curiosity-prolog/master/README.md

__See the project on Github:__

https://github.com/liaTemplates/curiosity-prolog

                         --{{1}}--
There are three ways to use this template. The easiest way is to use the
`import` statement and the URL of the raw text-file of the master branch or any
other branch or version. But you can also copy the required functionality
directly into the header of your Markdown document, see therefor the
[last slide](#4). And of course, you could also clone this project and change
it, as you wish.

    {{1}}
1. Load the macros via

   `import: https://raw.githubusercontent.com/liaTemplates/curiosity-prolog/master/README.md`

2. Copy the definitions into your Project

3. Clone this repository on GitHub

## `@Prolog.db` & `@Prolog.shell`

```prolog
mother_child(trude, sally).

father_child(tom, sally).
father_child(tom, erica).
father_child(mike, tom).

sibling(X, Y)      :- parent_child(Z, X), parent_child(Z, Y).

parent_child(X, Y) :- father_child(X, Y).
parent_child(X, Y) :- mother_child(X, Y).
```
@Prolog.db(family.pro)


** Queries **

```prolog
sibling(sally, erica).
```
@Prolog.shell(family.pro)


## `@Prolog.ui`



```prolog @Prolog.ui(db_full_etc,`sibling(sally, erica).`)
mother_child(trude, sally).

father_child(tom, sally).
father_child(tom, erica).
father_child(mike, tom).

sibling(X, Y)      :- parent_child(Z, X), parent_child(Z, Y).

parent_child(X, Y) :- father_child(X, Y).
parent_child(X, Y) :- mother_child(X, Y).
```

## Implementation

                         --{{0}}--
The code shows how the macros were implemented. If you want to use a fully
functional Prolog implementation for your course, see the more mature
[Tau-Prolog](https://github.com/liaTemplates/tau-prolog).


````js
script:   https://curiosity-driven.github.io/prolog-interpreter/parser.js
          https://curiosity-driven.github.io/prolog-interpreter/interpreter.js

@Prolog.db
<script>
var rules = parser(lexer(`@input`)).parseRules();
window['@0'] = new Database(rules);
"database " + "@0" + " loaded";
</script>
@end

@Prolog.shell
<script>
var rslt = "";
var goal = parser(lexer(`@input`)).parseTerm();
for (var item of window['@0'].query(goal)) {
    rslt += "Yes: " + item + "\n";
}
if (rslt === "") {
   'No';
} else {
   rslt;
}
</script>
@end

@Prolog.ui
```prolog
@2
```
@Prolog.db(@0)


```prolog
@1
```
@Prolog.shell(@0)
@end
````

                         --{{1}}--
If you want to minimize loading effort in your LiaScript project, you can also
copy this code and paste it into your main comment header, see the code in the
raw file of this document.

{{1}} https://raw.githubusercontent.com/liaTemplates/curiosity-prolog/master/README.md
