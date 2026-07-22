# discrete-structures

A Datalog interpreter written in C++: it lexes, parses, and evaluates a small logic-query language over an in-memory relational database.

## What this demonstrates

The program reads a Datalog source file and runs it end to end. A hand-written scanner turns the raw text into tokens, a recursive-descent parser builds a Datalog program made of schemes, facts, rules, and queries, and a relational engine answers the queries. Rules are evaluated to a fixed point: the interpreter keeps applying them until no new tuples are derived, which is how recursive rules resolve.

It was one of my first real projects, built for a discrete-structures course to connect the theory (relations, tuples, set operations, fixed-point evaluation) to working code. The whole thing lives in header files, which I would not do today, but it runs.

## Concepts demonstrated

- Lexical analysis: a hand-written scanner producing a typed token stream (`Token.h`, `Scanner.h`)
- Recursive-descent parsing into a Datalog AST of schemes, facts, rules, and queries (`Parser.h`, `DatalogP.h`)
- A relational database of named relations, each a set of tuples over a scheme (`Database.h`)
- Relational algebra operations (select, project, rename) used to answer queries
- Natural join of relations to evaluate rule bodies
- Fixed-point rule evaluation: iterate until the derived tuple set stops growing
- Parse-error detection that halts evaluation before running a malformed program

## What's implemented

- `Token.h` — token types and the `Token` class
- `Scanner.h` — the lexer that tokenizes an input file
- `Parser.h` / `DatalogP.h` — the parser and the Datalog program representation
- `Database.h` — relations, tuples, schemes, and the query/rule evaluation engine
- `Driver.cpp` — reads a file, scans, parses, then evaluates rules and queries

## Stack

- C++ (STL: `vector`, `set`, `map`, streams)

## Usage

Compile the driver and pass a Datalog input file:

```bash
g++ -std=c++17 Driver.cpp -o datalog
./datalog input.txt
```

The program prints rule evaluation and query results, or a parse error if the input is malformed.
