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

property              | leírás
----------------------|-------
[name](#name)         | a tenant megjelenítendő neve
[flags](#flags)       | login oldalt befolyásoló generator flag-ek
[theme](#theme)       | Bootstrap theme címe
[template](#template) | HTML oldal template-ek címe
[factory](#factory)   | külső user/client generator címe
[depot](#depot)       | külső user/client adatbázis címe
[sheet](#sheet)       | user adatbázist tartalmazó Google Sheet azonosítója


### name

A tenant megjelenítendő neve a `name` paraméterben adható meg. Hiánya esetén a tenant DNS neve jelenik meg. E név jelenik meg a tenant web lapjainak címsorában.

### flags

A tenant működését befojásoló flageket tartalmazó paraméter (lásd [Flags](generator.md#flags)). Jelenleg a team méretét befolyásoló flag-nek van szerepe a login képernyőn. Amennyiben szerepel a flag-ek között team méret flag, úgy beviteli mező helyett egy listából lehet kiválasztani a felhasználót a login képernyőn. Lehetséges értékei:

 - tiny
 - small
 - medium
 - large

### theme

A tenant-ok HTML oldalainak template-jei a Bootstrap library használatával készültek. Ennek kösöznhetően az oldalak kinézete, színei külső Bootstrap CSS file-okkal testreszabhatók. A `theme` paraméter az oldalakon használandó Bootstrap CSS file URL-jét tartalmazza. Megadása nem kötelező, hiánya esetén a [PhantAuth developer portal](https://www.phantauth.net)-on látható default kinézettel jelennek meg a tenant HTML oldalai.

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
policy.html  | tenant privacy policy
tos.html     | tenant term of service
test.html    | user generátor és OpenID Connect login test oldal

Saját template-ek használatával az oldalak teljes mértékben testreszabhatóak. A template-ek kifejtéséhez [Thymeleaf](https://www.thymeleaf.org/) template engine használatos, mely rugalmas template lehetőségeket biztosít. A default template-ek forrása a [phantauth-default](https://github.com/phantauth/phantauth-default) GitHub repository-ban elérhető. Saját template-ek készítése során célszerű ezekből a template-ekből kiindulni.

### factory

A PhantAuth lehetőséget ad saját random resource (user, team, client, fleet) generator használatára, melynek címét a `factory` tenant paraméterben lehet megadni. A paraméter értéke egy [RFC 6570 - URI temaplate](https://tools.ietf.org/html/rfc6570) kifejezés. Az URI template a `kind` paraméterben kapja meg a generálandó objektum típusát (user, team), a `name` paraméterben pedig a generálandó objektum azonosítóját.

### factories

A `factories` paraméterben adható meg, hogy a `factory` paraméterben beállított külső generátor milyen resource típusokat képes generálni. Értéke egy vagy több string az alábbiak közül: `user`, `team`.

### depot

Lehetőség van a user és team resource-ok generálása helyett egy előre létrehozott készletből történő véletlenszerű kiválasztásra. Ez esetben a resource adatokat tartalmazó CSV file URL-jét a `depot` pareméterben lehet megadni. A paraméter értéke egy [RFC 6570 - URI temaplate](https://tools.ietf.org/html/rfc6570) kifejezés. Az URI template a `kind` paraméterben kapja meg a generálandó objektum típusát (user, team). 

A CSV file első sora tartalmazza a resource property neveket, a további sorok pedig az adatokat. Egymásba ágyazott property-k esetén a property névben '.' karakter választja el a név egyes elemeit (pl address.formatted). 

### depots

A `depots` paraméterben adható meg, hogy a `depot` paraméterben beállított külső forrást mire használja a rendszer. Értéke egy vagy több string az alábbiak közül: `user`, `team`.

### sheet

Lehetőség van a user adatok Google Sheet dokumentumból történő véletlenszerű kiválasztására. A `sheet` paraméterben egy publikus Google Sheet dokumentum azonosítója adható meg. A táblázat első sora tartalmazza a user property neveket, a további sorok pedig az adatokat. Egymásba ágyazott property-k esetén a property névben '.' karakter választja el a név egyes elemeit (pl address.formatted).
