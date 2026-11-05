# Library Management System (C++)

An object-oriented library management system written in C++17. It manages different kinds of books (physical, digital, audiobooks), users and loans, and includes an automatic late-return penalty system.

Built as a university project for the Object-Oriented Programming course (Stefan cel Mare University of Suceava, Faculty of Electrical Engineering and Computer Science). Developed and tested on Linux (WSL).

## Features

- Class hierarchy of books: fiction, technical, digital (PDF/EPUB/MOBI) and audiobooks
- Users with their own list of borrowed books
- Loan management: borrowing, returning and availability checks
- Automatic penalty calculation for late returns (0.5 lei per day)
- Penalty report for all users
- Unit tests and a Makefile-based build

## Project structure

```
src/                      C++ source code
  Carte.h / .cpp          Base class and derived book classes
  Utilizator.h / .cpp     User management
  Biblioteca.h / .cpp     Main library logic
  Imprumut.h / .cpp       Loans and penalties
tests/                    Unit tests (test_carte.cpp)
Makefile                  Build system
```

## Class design

```
Carte (title, author, isbn, available)
 |- CarteFictiune   (genre)
 |- CarteTehnica    (domain)
 |- CarteDigitala   (format, download link, size in MB)
 |- Audiobook       (narrator, duration in minutes)

Utilizator   (name, id, list of borrowed ISBNs)
Imprumut     (user id, isbn, loan date, day limit)
Biblioteca   (vector<Carte*>, vector<Utilizator>, vector<Imprumut>)
```

## OOP concepts used

| Concept | Where |
|---|---|
| Classes and objects | All classes |
| Encapsulation | Private attributes with getters and setters |
| Inheritance | Four book types extend `Carte` |
| Polymorphism | Virtual `afiseazaDetalii()` overridden in each derived class |
| STL | `vector` of books, users and loans |

## Late-return penalties

Each loan stores its exact date using `time_t`. The program computes the days of delay against the loan limit, applies a penalty of 0.5 lei per day, and prints a report with the total for every user.

## Requirements

- g++ with C++17 support
- make
- Linux or WSL (Windows Subsystem for Linux)

```bash
sudo apt update && sudo apt install -y g++ make
```

## Build and run

```bash
make          # compile
./app         # run
make test     # run the unit tests
make clean    # remove build files
```

## Example output

```
=== Catalog Biblioteca ===
[FICTIUNE - SF] Carte: Dune | Autor: Frank Herbert | ISBN: ISBN001 | Disponibila
[TEHNIC - Programare] Carte: Clean Code | Autor: Robert Martin | ISBN: ISBN002 | Disponibila
[AUDIOBOOK | 4h 30min | Narator: Mike Chamberlain] Carte: Atomic Habits | Autor: James Clear | ISBN: ISBN005 | Disponibila

[LOG] Ion Popescu a imprumutat: ISBN001 (limita: 14 zile)
[LOG] EROARE: Cartea ISBN001 nu este disponibila!
```

## Git workflow

Two branches: `main` for the stable version and `develop` for active development.

## Author

Mathias Bucsa
