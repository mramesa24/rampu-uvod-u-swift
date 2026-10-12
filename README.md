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

print(pi)   // Ispisuje: 3.14
print(ime)  // Ispisuje: Luka
```

Konstanta ili varijabla mora dobiti vrijednost prije nego što je pokušamo koristiti. Swift može automatski zaključiti tip podatka iz dodijeljene vrijednosti.

## Tipovi podataka

Swift je **strogo tipiziran jezik**: svaka varijabla ili konstanta ima određen tip. Tip se može navesti izravno ili ga Swift može zaključiti (*type inference*).

```swift
// Swift zaključuje da je broj cijeli broj tipa Int.
let broj = 10

// Tip Double navodimo izravno.
let cijena: Double = 12.50

// Ostali česti jednostavni tipovi.
let aktivan: Bool = true
let slovo: Character = "A"
let poruka: String = "Bok!"
let temperatura: Float = 21.5
```

Česti tipovi:

- **Jednostavni:** `Int`, `Double`, `Float`, `Bool`, `String`, `Character`
- **Složeni:** `Optional`, `struct`, `class`, `enum`
- **Kolekcije i grupiranje podataka:** tuple (n-torka), `Array`, `Dictionary`, a često i `Set`

## Operatori

Operatori omogućuju izvođenje izračuna, usporedbi i logičkih operacija.

```swift
let a = 10
let b = 3

// Aritmetički operatori.
print(a + b)  // 13 — zbrajanje
print(a - b)  // 7  — oduzimanje
print(a * b)  // 30 — množenje
print(a / b)  // 3  — dijeljenje cijelih brojeva
print(a % b)  // 1  — ostatak pri dijeljenju

// Operatori usporedbe vraćaju Bool (true ili false).
print(a == b) // false — jednako
print(a != b) // true  — različito
print(a > b)  // true
print(a < b)  // false
print(a >= b) // true
print(a <= b) // false

// Logički operatori kombiniraju uvjete.
print(a > 5 && b < 5) // true — oba uvjeta moraju biti istinita
print(a < 5 || b < 5) // true — dovoljan je jedan istinit uvjet
print(!(a > b))       // false — negacija uvjeta

// Operator pridruživanja sprema vrijednost u varijablu.
var rezultat = 0
rezultat = a + b
print(rezultat) // 13
```

## Kolekcije

Kolekcije omogućuju grupiranje više vrijednosti.

### N-torke (*tuples*)

N-torka grupira više vrijednosti koje ne moraju biti istog tipa. Broj i raspored njezinih elemenata fiksni su.

```swift
// N-torka s imenovanim elementima.
let kartica = (boja: "Crvena", znak: "Srce", vrijednost: 7)

// Pristup imenovanom elementu.
print(kartica.boja)       // Crvena
print(kartica.vrijednost) // 7

// Elementima neimenovane n-torke pristupa se indeksima od 0.
let koordinata = (10, 20)
print(koordinata.0) // 10
print(koordinata.1) // 20

// Vrijednosti iz n-torke možemo raspakirati u zasebne konstante.
let (x, y) = koordinata
print(x) // 10
print(y) // 20
```

### Nizovi (*Array*)

Niz pohranjuje više vrijednosti istog tipa. Može biti prazan, a elementi se dohvaćaju indeksima.

```swift
// Niz imena tipa String.
var imena = ["Ivan", "Karlo", "Marko"]

// Dodavanje jednog elementa na kraj niza.
imena.append("Lovro")

// Možemo dodati i drugi niz elemenata.
imena += ["Ana", "Mia"]

// Indeksi počinju od 0: indeks 3 označava četvrti element.
print(imena[3]) // Lovro

// Broj elemenata u nizu.
print(imena.count) // 6
```

### Rječnici (*Dictionary*)

Rječnik pohranjuje parove **ključ–vrijednost**. Ključ služi za pronalaženje pripadajuće vrijednosti.

```swift
// Ime osobe je ključ, a dob je vrijednost.
var godine = [
    "Marko": 23,
    "Luka": 25,
    "Karlo": 22
]

// Dohvaćanje vrijednosti preko ključa.
// Rezultat je Optional jer ključ možda ne postoji.
print(godine["Marko"] ?? 0) // 23

// Dodavanje ili ažuriranje vrijednosti.
godine["Ivan"] = 21
godine["Marko"] = 24

print(godine["Ivan"] ?? 0)  // 21
print(godine["Marko"] ?? 0) // 24
```

## Optionals — opcionalne vrijednosti

Opcionalni tip (`Optional`) može sadržavati vrijednost određenog tipa ili `nil`, što znači da vrijednost trenutačno nije određena

```swift
// String? znači da varijabla može sadržavati String ili nil.
var moguciString: String? = nil

// Opcionalni tipovi mogu se koristiti i s nizovima i cijelim brojevima.
var moguciNiz: [Int]? = nil
var moguciBroj: Int? = 10

// Ispis opcionalne vrijednosti prikazuje i da je riječ o Optional tipu.
print(moguciBroj) // Optional(10)
```

### Opcionalno povezivanje (*optional binding*)

```swift
var ime: String? = "Ivan"

if let odmotanoIme = ime {
    // Ovaj se blok izvršava samo ako ime sadrži vrijednost.
    print(odmotanoIme) // Ivan
} else {
    // Ovaj se blok izvršava ako je ime nil.
    print("Vrijednost ne postoji")
}
```

### Operator `??` — zadana vrijednost

```swift
let nadimak: String? = nil

// Ako nadimak sadrži vrijednost, koristi se ona.
// Ako je nil, koristi se tekst "Gost".
let prikaznoIme = nadimak ?? "Gost"

print(prikaznoIme) // Gost
```

### Prisilno odmotavanje (`!`)

```swift
var moguciBroj: Int? = 10

// Prisilno odmotavamo vrijednost i množimo je s 2.
moguciBroj! *= 2

print(moguciBroj!) // 20
```

## Strukture i enumeracije

### Strukture (`struct`)

```swift
struct Student {
    // Svojstva koja opisuju studenta.
    var ime: String
    var prezime: String
}

// Stvaranje instance strukture i dodjela vrijednosti svojstvima.
let najboljiStudent = Student(ime: "Marko", prezime: "Marić")

print(najboljiStudent.ime)     // Marko
print(najboljiStudent.prezime) // Marić
```

### Enumeracije (`enum`)

```swift
enum OsnovnaBoja {
    case crvena
    case zelena
    case plava
}

// Odabir jedne od mogućnosti enumeracije.
var boja = OsnovnaBoja.crvena

// Ako Swift može zaključiti tip, naziv tipa može se izostaviti.
boja = .plava

print(boja) // plava
```

## Uvjetni iskazi

```swift
var temperatura = 25

// Oba uvjeta moraju biti istinita da bi se izvršio prvi blok.
if temperatura > 10 && temperatura < 30 {
    print("Vani je ugodnih \(temperatura) stupnjeva")
} else {
    // Izvršava se ako barem jedan od uvjeta nije istinit.
    print("Vani nije ugodno")
}
```

## Petlje

### `for-in`

```swift
let brojevi = [1, 2, 3, 4, 5]

// U svakom prolazu varijabla broj poprima sljedeći element niza.
for broj in brojevi {
    print(broj)
}
```

### `while`

```swift
var broj = 5

// Petlja se ponavlja dok je uvjet broj > 0 istinit.
while broj > 0 {
    broj -= 1 // Smanjujemo broj za 1.
    print(broj)
}

// Ispis: 4, 3, 2, 1, 0
```

## Prekidači (`switch`)

`switch` uspoređuje vrijednost s više mogućih slučajeva i izvršava odgovarajući blok.

```swift
let vrijednost = 2

switch vrijednost {
case 1:
    print("Jedan")
case 2:
    print("Dva")
default:
    // Izvršava se ako nijedan prethodni slučaj ne odgovara.
    print("Nepoznat")
}
```

## Funkcije

Funkcija je imenovana cjelina koda koju možemo pozvati više puta. Može primati parametre i vraćati rezultat, ali ne mora raditi ni jedno ni drugo.

```swift
// Funkcija prima parametar ime tipa String i vraća String.
func pozdrav(ime: String) -> String {
    return "Zdravo \(ime)"
}

// Poziv funkcije i spremanje rezultata.
let poruka = pozdrav(ime: "Ivan")

print(poruka) // Zdravo Ivan
```

- `func` označava početak definicije funkcije.
- `ime: String` definira parametar i njegov tip.
- `-> String` označava da funkcija vraća vrijednost tipa `String`.
- `return` vraća rezultat pozivatelju funkcije.

## Klase i objekti

Klasa je predložak za stvaranje objekata. Može sadržavati svojstva (podatke) i metode (funkcije povezane s objektom). Za razliku od struktura, klase su **referentni tipovi**.

```swift
class Osoba {
    // Svojstvo koje opisuje osobu.
    var ime: String

    // Inicijalizator se poziva pri stvaranju objekta.
    init(ime: String) {
        self.ime = ime
    }

    // Metoda koja koristi svojstvo objekta.
    func predstaviSe() {
        print("Ja sam \(ime)")
    }
}

// Stvaramo objekt klase Osoba i predajemo ime inicijalizatoru.
let osoba = Osoba(ime: "Ivan")

// Pozivamo metodu objekta.
osoba.predstaviSe() // Ja sam Ivan
```

`self.ime` označava svojstvo objekta, dok `ime` s desne strane označava parametar inicijalizatora. Inicijalizator (`init`) služi za pripremu novog objekta s početnim vrijednostima.

## Kontrola pristupa

Kontrola pristupa određuje gdje se svojstvima, metodama i drugim deklaracijama može pristupiti.

- `public` — dostupno izvan modula, ali se javne klase i članovi ne mogu slobodno nadjačavati izvan modula kao `open`.
- `internal` — zadana razina; dostupno unutar mjesta gdje je definiran
- `private` — dostupno unutar pripadajućeg ograničenog područja deklaracije, uključujući odgovarajuće ekstenzije tog tipa u istoj datoteci.

```swift
class Racun {
    // Dostupno samo unutar klase Racun i dopuštenih povezanih područja.
    private var stanje: Double = 0

    // Javna metoda omogućuje sigurno mijenjanje stanja računa.
    func uplati(_ iznos: Double) {
        if iznos > 0 {
            stanje += iznos
        }
    }

    // Metoda omogućuje čitanje stanja bez izravnog pristupa privatnom svojstvu.
    func prikaziStanje() {
        print(stanje)
    }
}

let racun = Racun()
racun.uplati(50)
racun.prikaziStanje() // 50
```

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
    // Nadjačavamo metodu iz nadklase.
    override func predstaviSe() {
        print("Ja sam student \(ime)")
    }
}

let student = Student(ime: "Ivan")
student.predstaviSe() // Ja sam student Ivan
```

## Agregacija i kompozicija

### Agregacija

Kod agregacije jedan objekt koristi ili grupira druge objekte, ali oni mogu postojati neovisno o njemu.

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

let ana = Student(ime: "Ana")
let fakultet = Fakultet()

// Postojeći objekt studenta dodajemo u kolekciju fakulteta.
fakultet.studenti.append(ana)

print(fakultet.studenti[0].ime) // Ana
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

struct Automobil {
    // Automobil sadrži svoje dijelove kao svojstva.
    var motor: Motor
    var kotaci: Kotaci
    var vrata: Vrata
}

// Pri stvaranju automobila stvaramo i vrijednosti njegovih dijelova.
let automobil = Automobil(
    motor: Motor(snaga: 100),
    kotaci: Kotaci(velicina: 30),
    vrata: Vrata(boja: "Plava")
)

print(automobil.motor.snaga) // 100
print(automobil.kotaci.velicina) // 30
print(automobil.vrata.boja) // Plava
```
