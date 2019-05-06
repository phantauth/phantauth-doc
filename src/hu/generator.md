# Generator

## Concept

A PhantAuth alap koncepciója az adatok véletlenszerű, de determnisztikus generálása. Ennek megvalósítása ún. pseudorandom number generator (PRNG) használatával történik. Minden objektum típusnak van egy azonosítója (login név a user esetén, client_id a client esetén stb). Ezen azonosítóból egy adott hash algoritmus segítségével képződik a pseudorandom generator seed értéke. Ezt követően az adott objektum minden egyes jellemzője ezen seed értékről indított pseudorandom generator segítségével generálódik. A pseudorandom number generator vagy más néven deterministic random bit generator (DRBG) azon sajátosságát kihasználva, hogy ugyanazon kezdőértékről indítva ugyanazon véletlenszerű érték sorozatot állítja elő, az azonosító egyértelműen meghatározza a belőle generált objektumot. Azaz az azonosító és a generator birtokában az objektum jellemzői bármikor újragenerálhatók.

A fenti koncepciónak köszönhetően a teljes PhantAuth szolgáltatás állapot mentes, nincs szükség háttértároló használatára. Így például egy tetszőlegsen választott bejelentkezési név "létezni" fog, s előállíthatók a hozzá "tartozó" felhasználó jellemzői.

## Identifier

Az egyes objektumokat tehát az azonosítójuk határozza meg. A User és a Client objektum esetén az OpenID Connect specifikációban használatos `sub` illetve `client_id` a neve az azonosítónak. Az egyéb, specifikációban nem szereplő PhantAuth specifikus objektumoknak esetén `sub` az azonosító property neve.

Az azonosító tetszőleges karaktereket tartalmazhat.

## Customization

Az azonosítóból generált jellemzőket időnként szeretnénk testreszabni. Bár az azonosító tetszőleges karaktereket tartalmazhat s nincs előírás a szerkezetére, bizonyos szerkezet használata esetén a generált értékek testreszabhatóak.

### Flags

Az objektum (user, client, stb) egyes jellemzőinek generátorai különböző flag-ekkel testreszabhatók, paraméterezhetők. A flag-ek csoportokra oszthatók, aszerint hogy mely jellemző generálását befolyásolják. A flag maga egy kulcsszó. Egyidejűleg több, eltérő jellemző generálását befolyásoló flag is megadható. A flag-eket egymástól és az azonosító többi részétől pontosvessző `;` karakter választja el:

```
joe;female;kitten
```

A fenti példa a user generator használata esetén a generált felhasználó nőnemű lesz s az avatar-ja egy véletlenszerűen kiválasztott macska rajz lesz. A többi jellemzője a 'joe' névből determinisztikusan generálódik, azaz értékükre nincs hatással a megadott két. A példához tartozó [profile oldal itt](https://phantauth.net/~joe%3bfemale%3bkitten) megtekinthető.

A flag-ek részletes leírása az [API](api.md) dokumentációban található.

Fontos megjegyezni, hogy a flag-ek részét képzik az azonosítónak, lévén használatukkal más objektum generálódik.

### Name

A generált objektumok többnyire rendelkeznek teljes névvel, mely az azonosítóból generálódik. A teljes név generálása kiiktatható, ha az azonosító tartalmaz minimum egy pont (`.`) vagy szóköz (` `) karaktert. Ez esetben e karakterek szeparator szerepet töltenek be a teljes név egyes részei között (pl family name, given name). Azaz a teljes név ilyenkor nem véletlenszerűen generálódik az azonosítóból, hanem a szeparator karaktereket figyelembe véve az azonosító egyes részeiből készül a teljes név (a kezdőbetűk nagybetűssé alakításával). Szóköz helyett célszerű pont karaktert használni.

```
joe.black;sketch
```

A fenti példa a user generator használata esetén a generált felhasználó teljes neve *Joe Black* lesz (az avatar-ja pedig egy rajzos profil kép). A példához tartozó [profile oldal itt](https://phantauth.net/~joe.black%3bsketch) megtekinthető.

### Picture

A generált objektumok többnyire rendelkeznek valamilyen képpel (user esetén avatar, client esetén logo), mely kép az azonosítóból generálódik. Az hogy a kép milyen előre definiált készletből kerül ki, *flag*-ekkel befolyásolható (lásd [flags](#flags)). Ettől nagyobb testreszabhatóság érhető el a [Gravatar](https://gravatar.com) szolgáltatás használatával.

Minden objektumhoz generálódik egy egyedi email cím (user esetén `email`, egyéb objektumok esetén `logo_email`). Az adott objektumhoz tartozó kép testreszabása ezen email címhez történő gravatar kép hozzárendelésével érhető el. Az objektumok alapértelmezés szerint gravatar képpel rendelkeznek s a generált kép csak a gravatar URL default értékeként szerepel. Azaz amint létrehozunk egy gravatar képet az adott email címhez, az fog megjelenni az adott objektum képeként.

### Email

Minden objektumhoz generálódik egy disposable, működő email cím, mely alkalmas email fogadásra. A generált email cím helyett lehetőség van saját emaiél cím használatára is (pl előre létrehozott teszt email címek). Ez esetben az azonosító egy email címet tartalmaz. Az adott objektumhoz tartozó kép értelemszerűen ez esetben az azonosítóban található email címhez tartozó gravatar kép lesz.

```
ivan.test.szkiba@spam4.me
```

A fenti példa user generator használata esetén a generált felhasználó email címe *ivan.test.szkiba@spam4.me* lesz (a neve pedig *Ivan Test Szkiba*). A példához tartozó [profile oldal itt](https://phantauth.net/~ivan.test.szkiba%40spam4.me) megtekinthető.

## Custom Generators

A PhantAuth rendszer képes külső adatforrások s generátorok használatára. Egyetlen megkötés külső generátorok használata során, hogy determinisztikusak legyenek, azaz többszöri hívás esetén ugyanahhoz az azonosítóhoz ugyanazt az objektumot állítsák elő.

A külső generátorok egy speciális esete a külső adatforrás használata. Ez esetben egy comma separated value (CSV) file-ban vagy egy Google Sheet dokumentumben adhatók meg az objektumok jellemzői.

Külső adatforrások és generátorok úgynevezett [tenant](tenant.md)-ok használatával definiálhatók, melyek leírása a [Tenant](tenant.md) fejezetben található.
