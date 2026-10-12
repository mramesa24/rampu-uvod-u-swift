# Swift — osnove programskog jezika
---
## Pohranjivanje podataka

Podatke pohranjujemo u **konstante** i **varijable**.

- `let` definira konstantu čiju vrijednost nakon dodjele ne možemo promijeniti.
- `var` definira varijablu čiju vrijednost možemo promijeniti.

```swift
// Konstanta: vrijednost pi ostaje ista.
let pi = 3.14

// Varijabla: vrijednost se može promijeniti.
var ime = "Ivan"
ime = "Luka"

print(pi)
print(ime)
```

Ispis
```
3.14
Luka
```

Konstanta ili varijabla mora dobiti vrijednost prije nego što je pokušamo koristiti.

## Tipovi podataka

Swift je strogo tipiziran jezik, svaka konstanta ili varijabla se definra s statičkim tipom podataka koji pohranjuje. Tip se može navesti izravno ili ga Swift može zaključiti (*type inference*).

```swift
// Swift zaključuje da je broj cijeli broj tipa Int.
let broj = 10

// Tip Double navodimo izravno.
let cijena: Double = 12.50

// Ostali česti jednostavni tipovi.
let aktivan: Bool = true
let slovo: Character = "A"
let ime: String = "Ivan"
let temperatura: Float = 21.5
```

Česti tipovi:

- **Jednostavni:** `Int`, `Double`, `Float`, `Bool`, `String`, `Character`
- **Složeni:** `Optional`, `struct`, `class`, `enum`
- **Kolekcije i grupiranje podataka:** tuple (n-torka), `Array`, `Dictionary`, a često i `Set`

## Operatori

```swift
let a = 10
let b = 3

// Aritmetički operatori.
print(a + b)  // zbrajanje
print(a - b)  // oduzimanje
print(a * b)  // množenje
print(a / b)  // dijeljenje cijelih brojeva
print(a % b)  // ostatak pri dijeljenju

// Operatori usporedbe vraćaju Bool (true ili false).
print(a == b) // jednako
print(a != b) // različito
print(a > b)
print(a < b)
print(a >= b)
print(a <= b)

// Logički operatori kombiniraju uvjete.
print(a > 5 && b < 5) // oba uvjeta moraju biti istinita
print(a < 5 || b < 5) // dovoljan je jedan istinit uvjet
print(!(a > b))       // negacija uvjeta

// Operator pridruživanja sprema vrijednost u varijablu.
var rezultat = 0
rezultat = a + b
print(rezultat)
```

Ispis

```
13
7
30
3
1

false
true
true
false
true
false

true
true
false

13
```

## Kolekcije

Kolekcije omogućuju Pohranjivanje i imenovanje složenijih informacijama.

### N-torke (*tuples*)

N-torka je kolekcija fiksne velicine sa najmanje 2 informacije
Ako informacije u n-torki nisu imenovane pozivaju se sa 0,1,2,3,...

```swift
// N-torka s imenovanim elementima.
let card = (color: "Red", suit: "Heart", value: 7)

// Pristup imenovanom elementu.
print(card.color)
print(card.value)

// Neimenovana N-torka.
let brojevi = (10, 20)

// Pristup neimenovanim elementima pomoću indeksa
print(brojevi.0)
print(brojevi.1)

// Vrijednosti iz n-torke možemo spremiti u konstante
let (prvi, drugi) = brojevi
print(prvi)
print(drugi)
```

Ispis
```
Red
7

10
20

10
20
```

### Nizovi (*Array*)

Niz pohranjuje više vrijednosti istog tipa promjenjive dužine. Može biti prazan

```swift
// Niz imena tipa String.
var names = ["Ivan", "Karlo", "Marko"]

// Dodavanje jednog elementa na kraj niza.
names.append("Lovro")

// Možemo dodati i drugi niz elemenata.
names += ["Ana", "Mia"]

// Indeksi počinju od 0: indeks 3 označava četvrti element.
print(names[3])

// Broj elemenata u nizu.
print(names.count)
```

Ispis
```
Lovro
6
```


### Rječnici (*Dictionary*)

Rječnik pohranjuje parove ključ–vrijednost. Ključ služi za pronalaženje pripadajuće vrijednosti.

```swift
// Ime osobe je ključ, a dob je vrijednost.
var godine = [
    "Marko": 23,
    "Luka": 25,
    "Karlo": 22
]

// Dohvaćanje vrijednosti preko ključa.
print(godine["Luka"])

// Rezultat je Optional jer ključ možda ne postoji.
print(godine["Marko"] ?? 0) // 23

// Dodavanje ili ažuriranje vrijednosti.
godine["Ivan"] = 21
godine["Marko"] = 24

print(godine["Ivan"] ?? 0)
print(godine["Marko"] ?? 0)
```

Ispis
```
Optional(25)

23

21
24
```

## Optionals — opcionalne vrijednosti

Opcionalni tip podataka omogućuje da se pohranjuje nul vrjednost (nil)

```swift
// <tip>? znači da varijabla može sadržavati String ili nil.
var moguciString: String? = nil

// Opcionalni tipovi mogu se koristiti i s nizovima i cijelim brojevima.
var moguciNiz: [Int]? = nil
var moguciBroj: Int? = 10

print(moguciBroj)
```

Ispis
```
Optional(10)
```


### Opcionalno povezivanje

```swift
var name: String? = "Ivan"

if let unwrappedName = name {
    print(unwrappedName)
} else {
    print("Vrijednost ne postoji")
}
```

Ispis
```
Ivan
```

### Operator `??`

```swift
let clan: String? = nil

// Ako clan sadrži vrijednost, koristi se ona.
// Ako je nil, koristi se tekst "Gost".
let imeClana = clan ?? "Gost"

print(imeClana)
```

Ispis
```
Gost
```

### Prisilno odmotavanje (`!`)

```swift
var possibleInt: Int? = 10

possibleInt! *= 2

print(possibleInt!)
```

Ispis
```
20
```

## Strukture i enumeracije

### Strukture (`struct`)

Strukture su najosnovniji načingrupiranja različitih podataka

```swift
struct Student {
    var ime: String
    var prezime: String
}

let najboljiStudent = Student(ime: "Marko", prezime: "Marić")

print(najboljiStudent.ime)
print(najboljiStudent.prezime)
```

Ispis
```
Marko
Marić
```

### Enumeracije (`enum`)

Enumeracije su skupine povezanih vrjednosti za neku vrjednost

```swift
enum osnovneBoje {
    case Crvena
    case Zelena
    case Plava
}

var boja = osnovneBoje.Crvena
print(boja)

// Ako Swift može zaključiti tip, naziv tipa može se izostaviti.
boja = .Plava

print(boja)
```

Ispis
```
Crvena
Plava
```

## Uvjetni iskazi

```swift
var temperatura = 30

if temperatura > 10 && temperatura < 30 {
    print("Vani je ugodnih \(temperatura) stupnjeva")
} else {
    print("Vani nije ugodno")
}
```

Ispis
```
Vani nije ugodno
```


## Petlje

### `for`

```swift
let brojevi = [1, 2, 3, 4, 5]

for broj in brojevi {
    print(broj)
}
```

### `while`

```swift
var broj = 5

while broj > 0 {
    broj -= 1 // Smanjujemo broj za 1.
    print(broj)
}
```

## Prekidači (`switch`)

```swift
var broj = 1

switch broj {
case 1:
    print("Jedan")
case 2:
    print("Dva")
default:
    print("Nepoznat")
}
```

## Funkcije

Linearna kolekcija koda koja se može pokretati više puta kada se poziva imenom

```swift
// Funkcija prima parametar ime tipa String i vraća String.
func pozdrav(ime: String) -> String {
    return "Zdravo \(ime)"
}

let poruka = pozdrav(ime: "Ivan")

print(poruka)
```

Ispis
```
Zdravo Ivan
```

## Klase i objekti

Klasa je predložak za stvaranje objekata. Može sadržavati svojstva (podatke) i metode (funkcije povezane s objektom). Za razliku od struktura, klase su referentni tipovi.

```swift
class Osoba {
    var ime: String

    // Inicijalizator/Konstruktor se poziva pri stvaranju objekta.
    init(ime: String) {
        self.ime = ime
    }

    func predstaviSe() {
        print("Ja sam \(ime)")
    }
}

let osoba = Osoba(ime: "Ivan")

osoba.predstaviSe()
```

Ispis
```
Ja sam Ivan
```

## Kontrola pristupa

Kontrola pristupa određuje gdje se svojstvima, metodama i drugim deklaracijama može pristupiti.
- public: Moze mu pristupiti svkai kod koji uveze modul
- private: Dostupan samo unutar podrucja deklaracije
- internal: Samo isti modul ili aplikacija

## Nasljeđivanje

```swift
class Osoba {
    var ime: String

    init(ime: String) {
        self.ime = ime
    }

    func predstaviSe() {
        print("Ja sam \(ime)")
    }
}

// Student nasljeđuje svojstvo ime i metodu predstaviSe iz klase Osoba.
class Student: Osoba {
    // Nadjačavamo metodu iz Osoba klase
    override func predstaviSe() {
        print("Ja sam student \(ime)")
    }
}

let student = Student(ime: "Ivan")
student.predstaviSe()
```

Ispis
```
Ja sam student Ivan
```

## Agregacija i kompozicija

### Agregacija

Svojstvo agregacije ima objekt koji koristi druge objekte, ali ti objekti mogu postojati neovisno o njemu

```swift
class Student {
    let ime: String

    init(ime: String) {
        self.ime = ime
    }
}

class Fakultet {
    // Fakultet sadrži reference na studente.
    // Studenti se mogu stvoriti i postojati i bez ovog objekta Fakultet.
    var studenti: [Student] = []
}

var noviStudent = Student(ime: "Ivan")
let fakultet = Fakultet()

fakultet.studenti.append(noviStudent)

print(fakultet.studenti[0].ime)
```

Ispis
```
Ivan
```

### Kompozicija

```swift
struct Motor {
    var snaga: Int
}

struct Kotaci {
    var velicina: Int
}

struct Vrata {
    var boja: String
}

class Automobil {
    var snagaMotora: Motor
    var velicinaKotaca: Kotaci
    var bojaVrata: Vrata

    init(snagaMotora: Motor, velicinaKotaca: Kotaci, bojaVrata: Vrata) {
        self.snagaMotora = snagaMotora
        self.velicinaKotaca = velicinaKotaca
        self.bojaVrata = bojaVrata
    }

    func statistika(){
        print("Snaga: \(snagaMotora.snaga)")
        print("Velicina kotaca \(velicinaKotaca.velicina)")
        print("Boja vrata \(bojaVrata.boja)")
    }
}

let automobil: Automobil = Automobil(
    snagaMotora: Motor(snaga: 100),
    velicinaKotaca: Kotaci(velicina: 30),
    bojaVrata: Vrata(boja: "Plava")
)

automobil.statistika()
```

Ispis
```
Snaga 100
Velicina kotaca 30
Boja vrata Plava
```

## Protokoli

Protokol je uvjet koji tip može imati zbog kojeg se obavezuje da će pružiti određeno sučelje drugim komponentama.

```
protocol predstavljanje {
    func predstaviSe()
}

class Student: predstavljanje{
    // Ako Student ne sadržava metodu "predstaviSe" program se nece kompajlirati
    func predstaviSe() {
        print("Pozdrav moje ime je Ivan")
    }
}

var Ivan: Student = Student()
Ivan.predstaviSe()
```

Ispis
```
Pozdrav moje ime je Ivan
```
