# BankAccount – egyszerű bankszámla Java nyelven

Egy egyszerű bankszámlát modellező `BankAccount` osztály és a hozzá tartozó JUnit 5 egységtesztek.

## Funkciók

| Metódus | Leírás |
|---|---|
| `void deposit(double amount)` | Befizetés; növeli az egyenleget. |
| `void withdraw(double amount)` | Pénzfelvétel; csökkenti az egyenleget. |
| `double getBalance()` | Visszaadja az aktuális egyenleget. |

Szabályok:

- Az induló egyenleg 0.
- Negatív vagy 0 összegű befizetés / pénzfelvétel nem engedélyezett.
- Nem lehet többet felvenni, mint az aktuális egyenleg.
- Hibás művelet esetén `IllegalArgumentException` kivétel keletkezik, és az egyenleg nem változik.

## Projektstruktúra

```
bank-account/
├── pom.xml
├── README.md
└── src
    ├── main/java/hu/bank/BankAccount.java
    └── test/java/hu/bank/BankAccountTest.java
```

## Követelmények

- Java 17 vagy újabb (JDK)
- Apache Maven 3.8+

Ellenőrzés:

```bash
java -version
mvn -version
```

## Fordítás

```bash
mvn compile
```

## Tesztek futtatása

```bash
mvn test
```

Sikeres futás esetén a kimenet végén ez látható:

```
Tests run: 12, Failures: 0, Errors: 0, Skipped: 0
BUILD SUCCESS
```

Egyetlen teszt futtatása:

```bash
mvn test -Dtest=BankAccountTest#withdrawMoreThanBalanceThrows
```

IDE-ből (IntelliJ IDEA, Eclipse, VS Code) a projekt Maven-projektként megnyitható, a tesztek a `BankAccountTest` osztályon jobb klikk → *Run* paranccsal futtathatók.

## Lefedett tesztesetek

1. Új számla egyenlege 0.
2. `deposit(1000)` után az egyenleg 1000.
3. Több befizetés helyesen összeadódik.
4. Befizetés után a `withdraw()` helyesen csökkenti az egyenleget.
5. A teljes egyenleg felvehető.
6. Túl nagy összeg felvétele `IllegalArgumentException` kivételt dob (üres számláról is).
7. Negatív befizetés kivételt dob.
8. 0 összegű befizetés kivételt dob.
9. Negatív pénzfelvétel kivételt dob.
10. 0 összegű pénzfelvétel kivételt dob.

A hibás esetekben a tesztek azt is ellenőrzik, hogy az egyenleg változatlan marad. Egy külön teszt több sikertelen műveletet futtat egymás után, majd ellenőrzi az egyenleget.
