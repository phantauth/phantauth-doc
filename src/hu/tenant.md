# Tenant

## Concept

A PhantAuth belső felépítése kellően moduláris ahhoz, hogy az egyes alkotóelemei testreszabhatók, vagy akár lecserélhetők legyenek. A testreszabott PhantAuth példányok tekinthetők önálló, az eredetitől különböző szolgáltatásnak. A testreszabott PhantAuth példányokat az egyszerűség kedvéért nevezük **tenant**-oknak.

A testreszabott PhantAuth példányok (tenant-ok) más URL-en jelennek meg mint az eredeti (default tenant). Technológiai és cloud hosting szempontok alapján ezen URL-eket úgy praktikus megválasztani, hogy csak az URL path komponensének elejében térjenek el az eredeti PhantAuth URL-től. Szintén praktikus szempontok alapján a tenant URL path komponense egy speciális karakterrel (aláhúzás '_') kezdődik. A tenant URL általános formája tehát:

```
https://phantauth.net/_TENANT
```

Ahol a `TENANT` a tenant neve. A tenant név egyben egy DNS domain név, mely végéről a `.phantauth.net` valamint a `.phantauth.cf` elhagyható.

## DNS for configuration

A PhantAuth egyik tervezési szempontja hogy üzemeltetéséhez ne legyen szükség adatbázisra, viszont felhasználók által konfigurálható legyen. Ez úgy érhető el, hogy a tenant konfiguráció tárolására a Domain Name System (DNS) speciális TXT rekordjait használja a rendszer az [RFC 6763](https://tools.ietf.org/html/rfc6763) specifikációban definiált módon. A tenant név tehát egy vagy több DNS TXT rekord. Ezen TXT rekordokban találhatók a konfigurációs property-k NAME=VALUE formában.

Ily módon bárki lértehozhat saját tenant-ot, egyszerűen egy DNS domain valamint azon belüli TXT rekordok létrehozásával. A [Freenom](https://www.freenom.com) szolgáltatónál lehetőség van néhány top level domain-en belül (.tk, .ml, .ga, .cf, .gq) ingyenes regisztrációra. Az így regisztrált domain kezelhető a Freenom web felületén vagy átvihető valamely kényelmesebb (szintén ingyenes) DNS name server szolgáltatóhoz (pl [CloudFlare](https://www.cloudflare.com/)). Ezen kívül a [FreeDNS](https://freedns.afraid.org/) szolgáltatás lehetőséget ad közösség számára megosztott vagy magán tulajdonban lévő második vagy harmadik szintű domain-en belüli DNS rekordok létrehozására. Itt a `phantauth.cf` domain-en belül érdemes létrehozni bejegyzéseket, mert ez esetben a `.phantauth.cf` elhagyható a tenant névből az URL-ben. Azaz egy `mytenant.phantauth.cf` nevű tenant a `https://phantauth.net/_mytenant.phantauth.cf` URL helyett hivatkozható az rövidebb `https://phantauth.net/_mytenant` formában is. A `.phantauth.cf`-hez hasonlóan a `phantauth.net` is elhagyható, így a hivatalosan támogatott vagy példa tenant-ok is hivatkozhatók rövid névvel (pl https://phantauth.net/_faker).

Öszefoglalva tehát az alábbi módon hozható létre tenant:

 - Freenom szolgáltatónál regisztrált domain-en belüli TXT rekordok segítségével vagy a Freenom web felületén vagy más free DNS szolgáltató web felületén (pl CloudFlare)

 - FreeDNS szolgáltatás használatával valamely közösség számára megosztott második vagy harmadik szintű domain-ben létrehozott TXT rekordok segítségével

 - Saját létező DNS domain-ben létrehozott TXT rekordok segítségével tetszőleges DNS software használatával

## Parameters

Az alábbi táblázat a tenant-ok működését befolyásoló tenant paraméterek összefoglalását tartalmazza.

property                    | leírás
----------------------------|-------
[name](#name)               | a tenant megjelenítendő neve
[flags](#flags)             | login oldalt befolyásoló generator flag-ek
[theme](#theme)             | Bootstrap theme címe
[template](#template)       | HTML oldal template-ek címe
[factory](#factory)         | külső user generator címe
[depot](#depot)             | külső user adatbázis címe
[sheet](#sheet)             | user adatbázist tartalmazó Google Sheet azonosítója
[script](#script)           | a HTML oldalakra beszúrandó JavaScript URL-je
[summary](#summary)         | a tenant egy soros summary-ja
[about](#about)             | a tenant részletesebb leírása
[attribution](#attribution) | külső forrás megjelölés
[logo](#logo)               | a tenant logo-ja
[favicon](#favicon)         | a tenant web lapjainak favicon-ja

### name

A tenant megjelenítendő neve a `name` paraméterben adható meg. Hiánya esetén a tenant DNS neve jelenik meg. E név jelenik meg a tenant web lapjainak címsorában.

### flags

A tenant működését befojásoló flageket tartalmazó paraméter (lásd [Flags](generator#flags)). Jelenleg a team méretét befolyásoló flag-nek van szerepe a login képernyőn. Amennyiben szerepel a flag-ek között team méret flag, úgy beviteli mező helyett egy listából lehet kiválasztani a felhasználót a login képernyőn. Lehetséges értékei:

 - tiny
 - small
 - medium
 - large

### theme

A tenant-ok HTML oldalainak template-jei a Bootstrap library használatával készültek. Ennek köszönhetően az oldalak kinézete, színei külső Bootstrap CSS file-okkal testreszabhatók. A `theme` paraméter az oldalakon használandó Bootstrap CSS file URL-jét tartalmazza. Megadása nem kötelező, hiánya esetén a [PhantAuth developer portal](https://www.phantauth.net)-on látható default kinézettel jelennek meg a tenant HTML oldalai.

### template

A tenant HTML oldalainak template-jeinek helyét a `template` paraméter adja meg. A paraméter értéke egy [RFC 6570 - URI temaplate](https://tools.ietf.org/html/rfc6570) kifejezés. Az URI template egy `resource` paraméterben kapja meg az oldal nevét.

A `template` paraméter alapértelmezett értéke:

```
https://default.phantauth.net{/resource}
```

A `resource` URI template paraméter lehetséges értékei:

érték        | leírás
-------------|-------
tenant.html  | tenant web oldala, itt található a tenant rövid leírása s belépési pontjai
user.html    | user profile oldal
login.html   | bejelentkezés során használt login oldal
consent.html | bejelentkezés során használt consent oldal
team.html    | felhasználói csoport profile oldal
client.html  | client profile oldal
fleet.html   | client csoport profile oldal
policy.html  | client privacy policy
tos.html     | client term of service
test.html    | user generátor és OpenID Connect login test oldal

Saját template-ek használatával az oldalak teljes mértékben testreszabhatóak. A template-ek kifejtéséhez [Thymeleaf](https://www.thymeleaf.org/) template engine használatos, mely rugalmas template lehetőségeket biztosít. A default template-ek forrása a [phantauth-default](https://github.com/phantauth/phantauth-default) GitHub repository-ban elérhető. Saját template-ek készítése során célszerű ezekből a template-ekből kiindulni.

### factory

A PhantAuth lehetőséget ad saját random resource (user, team) generator használatára, melynek címét a `factory` tenant paraméterben lehet megadni. A paraméter értéke egy [RFC 6570 - URI temaplate](https://tools.ietf.org/html/rfc6570) kifejezés. Az URI template a `kind` paraméterben kapja meg a generálandó objektum típusát (user, team), a `name` paraméterben pedig a generálandó objektum azonosítóját.

### factories

A `factories` paraméterben adható meg, hogy a `factory` paraméterben beállított külső generátor milyen resource típusokat képes generálni. Értéke egy vagy több string az alábbiak közül: `user`, `team`.

### depot

Lehetőség van a user és team resource-ok generálása helyett egy előre létrehozott készletből történő véletlenszerű kiválasztásra. Ez esetben a resource adatokat tartalmazó CSV file URL-jét a `depot` pareméterben lehet megadni. A paraméter értéke egy [RFC 6570 - URI temaplate](https://tools.ietf.org/html/rfc6570) kifejezés. Az URI template a `kind` paraméterben kapja meg a generálandó objektum típusát (user, team). 

A CSV file első sora tartalmazza a resource property neveket, a további sorok pedig az adatokat. Egymásba ágyazott property-k esetén a property névben '.' karakter választja el a név egyes elemeit (pl address.formatted). 

### depots

A `depots` paraméterben adható meg, hogy a `depot` paraméterben beállított külső forrást mire használja a rendszer. Értéke egy vagy több string az alábbiak közül: `user`, `team`.

### sheet

Lehetőség van a user adatok Google Sheet dokumentumból történő véletlenszerű kiválasztására. A `sheet` paraméterben egy publikus Google Sheet dokumentum azonosítója adható meg. A táblázat első sora tartalmazza a user property neveket, a további sorok pedig az adatokat. Egymásba ágyazott property-k esetén a property névben '.' karakter választja el a név egyes elemeit (pl address.formatted).

A `sheet` paraméter használatára példa a `gods` nevű tenant, mely egy [publikus Google Sheets](https://docs.google.com/spreadsheets/d/1Xa4mRcLWroJr2vUDhrJXGBcobYmpS8fNZxFpXw-M9DY/) dokumentumban írja le a felhasználók adatait. Ez esetben a sheet azonosítója `1Xa4mRcLWroJr2vUDhrJXGBcobYmpS8fNZxFpXw-M9DY`, így az ezt leíró DNS TXT record:

```
gods	120	IN	TXT	"sheet=1Xa4mRcLWroJr2vUDhrJXGBcobYmpS8fNZxFpXw-M9DY"
```

### script

A login.html, consent.html és test.html oldalakra automatikusan beilleszthető egy custom JavaScript file, aminek az URL-je a `script` paraméterben adható meg. Ennek segítségével akár kliens oldali random user generátor is beköthető. 

### summary

A `summary` paraméterben egy rövid, egy soros leírás, szlogen adható meg a tenant-hoz. Ez a tenant nyitó oldalán jelenik meg valamint azokon az oldalakon ahol az elérhető tenant-ok listája szerepel.

### about

Az `about` paraméterben adható meg részletesebb leírás a tenant-ról. Amennyiben értéke egy URL, úgy a leírás a megadott URL-ről töltődik le, ellenkező esetben az érték maga a leírás. A leírásban Markdown formázás használható.

### attribution

Külső adatforrás, random user generator használata esetén az `attribution` paraméterben adható meg attribution. Az attribution-ban Markdown formázás használható, így megadhatók kiemelések, link-ek a külső forrásra:

```
randomuser	120	IN	TXT	"attribution=User data generated using [RANDOM USER GENERATOR](https://randomuser.me/)."
```

### logo

A tenant logo-jának URL-je. E címen található kép jelenik meg a tenant web lapjainak címsorában.

### favicon

A `favicon` paraméterben adható meg a favicon URL-je. E címen található kép jelenik meg a tenant web lapjainak látogatása során mint shortcut icon a böngészőben.

## Példák

A PhantAuth rendszer számos példát tartalmaz custom tenant létrehozására. Ezek használatra kész tenant-ok, bár elsősorban példaként készültek, a customizálás demonstrálására.

### faker

A [PhantAuth Faker](https://phantauth.net/_faker) tenant a JavaScript Faker library-ra épülő generátor tartalmaz. A generátor az ingyenes [ZEIT Now](https://now.sh) serverless deployment platform-on fut. Forráskódja a [phantauth-faker](https://github.com/phantauth/phantauth-faker) GitHub repository-ban érhető el. DNS konfigurációja:

```
faker.phantauth.net. 120	IN	TXT	"factories=team"
faker.phantauth.net. 120	IN	TXT	"factories=user"
faker.phantauth.net. 120	IN	TXT	"flags=small"
faker.phantauth.net. 120	IN	TXT	"factory=https://phantauth-faker.now.sh/api{/kind,name}"
faker.phantauth.net. 120	IN	TXT	"userinfo=Dream Team"
faker.phantauth.net. 120	IN	TXT	"theme=https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/united/bootstrap.min.css"
faker.phantauth.net. 120	IN	TXT	"logo=https://phantauth-faker.now.sh/faker-logo.svg"
faker.phantauth.net. 120	IN	TXT	"name=PhantAuth Faker"
```

### chance

A [PhantAuth Chance](https://phantauth.net/_chance) tenant a JavaScript Chance library-ra épülő generátor tartalmaz. A generátor az ingyenes [ZEIT Now](https://now.sh) serverless deployment platform-on fut. Forráskódja a [phantauth-chance](https://github.com/phantauth/phantauth-chance) GitHub repository-ban érhető el. DNS konfigurációja:

```
chance.phantauth.net. 120	IN	TXT	"flags=small"
chance.phantauth.net. 120	IN	TXT	"name=PhantAuth Chance"
chance.phantauth.net. 120	IN	TXT	"factory=https://phantauth-chance.now.sh/api{/kind,name}"
chance.phantauth.net. 120	IN	TXT	"factories=team"
chance.phantauth.net. 120	IN	TXT	"factories=user"
chance.phantauth.net. 120	IN	TXT	"theme=https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/united/bootstrap.min.css"
chance.phantauth.net. 120	IN	TXT	"logo=https://phantauth-chance.now.sh/chance-logo.png"
```

### casual

A [PhantAuth Casual](https://phantauth.net/_casual) tenant a JavaScript Casual library-ra épülő generátor tartalmaz. A generátor az ingyenes [Auth0 Webtask](https://webtask.io) serverless deployment platform-on fut. Forráskódja a [phantauth-casual](https://github.com/phantauth/phantauth-casual) GitHub repository-ban érhető el. DNS konfigurációja:

```
casual.phantauth.net. 120	IN	TXT	"logo=https://www.phantauth.net/logo/phantauth-logo-gray.svg"
casual.phantauth.net. 120	IN	TXT	"name=PhantAuth Casual"
casual.phantauth.net. 120	IN	TXT	"factory=https://wt-51217f7b3eee6aead0123eeafe3b83e8-0.sandbox.auth0-extend.com/user{?name}"
casual.phantauth.net. 120	IN	TXT	"theme=https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css"
```

### gods

A [Greek Gods](https://phantauth.net/_gods) tenant esetén egy [publikus Google Sheets](https://docs.google.com/spreadsheets/d/1Xa4mRcLWroJr2vUDhrJXGBcobYmpS8fNZxFpXw-M9DY/) dokumentum tartalmazza a felhasználók adatait. DNS konfigurációja:

```
gods.phantauth.net.	120	IN	TXT	"attribution=God pictures come from  [Theoi Project](https://www.theoi.com/), a site exploring Greek mythology and the gods in classical literature and art."
gods.phantauth.net.	120	IN	TXT	"name=Greek Gods"
gods.phantauth.net.	120	IN	TXT	"flags=medium"
gods.phantauth.net.	120	IN	TXT	"theme=https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/sandstone/bootstrap.min.css"
gods.phantauth.net.	120	IN	TXT	"logo=https://cdn.staticaly.com/favicons/www.theoi.com"
gods.phantauth.net.	120	IN	TXT	"sheet=1Xa4mRcLWroJr2vUDhrJXGBcobYmpS8fNZxFpXw-M9DY"
```

### randomuser

A [RANDOM USER](https://phantauth.net/_randomuser) tenant a népszerű https://randomuser.me szolgáltatást használja random user generálásra. A randomuser.me service hívása kliens oldalon történik, a hívást a `script` paraméterben megadott [randomuser.js](https://www.phantauth.net/selfie/randomuser.js) script tartalmazza. DNS konfigurációja:

```
randomuser.phantauth.net.	120	IN	TXT	"attribution=User data generated using [RANDOM USER GENERATOR](https://randomuser.me/)."
randomuser.phantauth.net.	120	IN	TXT	"script=https://www.phantauth.net/selfie/randomuser.js"
randomuser.phantauth.net.	120	IN	TXT	"flags=small"
randomuser.phantauth.net.	120	IN	TXT	"name=RANDOM USER"
randomuser.phantauth.net.	120	IN	TXT	"logo=https://cdn.staticaly.com/favicons/randomuser.me"
randomuser.phantauth.net.	120	IN	TXT	"theme=https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/sandstone/bootstrap.min.css"
```

### uinames

A [uinames](https://phantauth.net/_uinames) tenant a https://uinames.com szolgáltatást használja random user generálásra. A uinames.com service hívása kliens oldalon történik, a hívást a `script` paraméterben megadott [uinames.js](https://www.phantauth.net/selfie/uinames.js) script tartalmazza. DNS konfigurációja:

```
uinames.phantauth.net.	120	IN	TXT	"attribution=User data generated using [uinames.com API](https://uinames.com)."
uinames.phantauth.net.	120	IN	TXT	"logo=https://uinames.com/assets/img/ios-precomposed.png"
uinames.phantauth.net.	120	IN	TXT	"flags=small"
uinames.phantauth.net.	120	IN	TXT	"theme=https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/minty/bootstrap.min.css"
uinames.phantauth.net.	120	IN	TXT	"name=uinames"
uinames.phantauth.net.	120	IN	TXT	"script=https://www.phantauth.net/selfie/uinames.js"
```

### mockaroo

A [Mockaroo](https://phantauth.net/_mockaroo) tenant a https://mockaroo.com szolgáltatást használja random user generálásra. A mockaroo.com service hívása kliens oldalon történik, a hívást a `script` paraméterben megadott [mockaroo.js](https://www.phantauth.net/selfie/mockaroo.js) script tartalmazza. DNS konfigurációja:

```
mockaroo.phantauth.net.	120	IN	TXT	"attribution=User data generated using [Mockaroo's Mock APIs](https://mockaroo.com/mock_apis)."
mockaroo.phantauth.net.	120	IN	TXT	"script=https://www.phantauth.net/selfie/mockaroo.js"
mockaroo.phantauth.net.	120	IN	TXT	"logo=https://www.phantauth.net/selfie/kongaroo.svg"
mockaroo.phantauth.net.	120	IN	TXT	"flags=small"
mockaroo.phantauth.net.	120	IN	TXT	"theme=https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/minty/bootstrap.min.css"
mockaroo.phantauth.net.	120	IN	TXT	"name=Mockaroo"
```
