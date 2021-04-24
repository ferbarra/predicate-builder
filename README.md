# predicate-builder

Adding large number of facts to Prolog programs is tedious. **predicate-builder** makes 
it less tedious by reducing the typing necessary to create lists of facts.

## Background

Suppose you have a list of of constants
```
a b c d e
```

... and some unary predicates.
```
predicate1 predicate2 predicate3
```

You want your program to contain the following facts:
```
predicate1(b)
predicate1(c)
predicate1(e)

predicate2(a)
predicate2(b)
predicate2(c)

predicate(d)
predicate(e)
```

Now imagine you have 500 constants instead of 4 and 30 predicates instead of 3.

## Usage

You need only to provide two files: a constants file and a predicate file

The constant files contains a constant per line.
```
a
b
c
d
e
...
```

The predicates file contains the name of unary predicates per line
```
predicate1
predicate2
predicate3
...
```

Using those two files **predicate-builder** generates a form for
assigning unary predicates to constants.

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
