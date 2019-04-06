# PhantAuth

> Random User Generator + OpenID Connect Provider.
> Like Lorem Ipsum, but for user accounts and authentication.

## TL;DR

**A PhantAuth célja a tesztelés egyszerűbbé tétele OpenID Connect autentikációt használó alkalmazások számára, véletlenszerűen generált felhasználók segítségével.**

végpont  | cím
---------|-----
issuer   | https://phantauth.net
discovery| https://phantauth.net/.well-known/openid-configuration

## OpenID Connect Provider

A PhantAuth OpenID Connect Provider-e támogatja az OpenID Connect specifikációban szereplő flow-kat (Hybrid, Implicit, Authorization Code) valamint az OAuth 2.0 specifikációban szereplő Resource Owner Password grant type-ot. A PhantAuth mint OpenID Connect Provider, intergrálható web alkalmazásokhoz, mobil alkalmazásokhoz, backend alkalmazásokhoz egyaránt. Az integráció törénhet direkt módon mint OpenID Connect Provider vagy történhet authentikációs integrátor szolgáltatásokon keresztül mint pl az Auth0 vagy Azure Active Directory B2C. További részletek az [Integration](integration.md) fejezetben.

Példák:

 - [Direct OpenID Connect integration](https://www.phantauth.net/test/oidc)
 - [Auth0 Social Connections integration](https://www.phantauth.net/test/auth0)
 - [Azure Active Directory B2C integration](https://www.phantauth.net/test/azure)

## Random User Generator

A PhantAuth véletlenszerű felhasználó generátora használható önállóan is, az OpenID Connect Provider szolgáltatástól függetlenül. Tetszőleges számú test felhasználó generálható. A generált felhasználók adatai bármikor újragenerálhatók a felhasználói név ismeretében (OpenID Connect *sub* claim). A generált felhasználók rendelkeznek egyedi, működő, eldobható email címmel, több készletből választható profil képpel s a szokásos profil adatokkal. Lehetőség van saját email cím és profil kép megadására is. A PhantAuth saját véletlenszerű felhasználó generátora is testreszabható, de ezen kívül lehetőség van küső generátorok bekötésére is. További részletek a [Generator](generator.md) fejezetben.

Teszt oldalak:

 - [Default Generator Test Page](https://phantauth.net/test/user) (embedded generator)
 - [Greek Gods Generator Test Page](https://phantauth.net/_gods/test/user) (embedded generator works from Google Sheet)
 - [Faker Generator Test Page](https://phantauth.net/_faker/test/user) (external generator using Javascript Faker library)
 - [Chance Generator Test Page](https://phantauth.net/_chance/test/user) (external generator using Javascript Chance library)
 - [Casual Generator Test Page](https://phantauth.net/_casual/test/user) (external generator using Javascript Casual library)
 - [Randomuser Generator Test Page](https://phantauth.net/_randomuser/test/user) (client side generator using https://randomuser.me)
 - [uinames Generator Test Page](https://phantauth.net/_uinames/test/user) (client side generator using https://uinames.com)
 - [Mockaroo Generator Test Page](https://phantauth.net/_mockaroo/test/user) (client side generator using https://mockaroo.com)

A véletlenszerűen generált felhasználókhoz profile oldal is készül, melyen a profil adatok egy egyszerű egyoldalas formában megtekinthetők.

Példa profilok:

 - [Random Profile](https://phantauth.net/~joe.black)
 - [Random Greek God Profile](https://phantauth.net/_gods/~zeus)
 - [Random Faker Profile](https://phantauth.net/_faker/~harry.houdini)
 - [Random Chance Profile](https://phantauth.net/_chance/~peter.pan)
 - [Random Casual Profile](https://phantauth.net/_casual/~john.smith)

## CodeSandbox Samples

A véletlenszerű felhasználó generátor használatát és a direkt OpenID Connect integrációt egyszerű CodeSandbox példák mutatják be. A példa alkalmazások közvetlenül a CodeSandbox-ről futnak, így a forráskód egyszerűen megtekinthető, szerkeszthető, kipróbálható.

Példák:

 - [Random User Generator usage exampe](https://4xyj8lw394.codesandbox.io/)
 - [OpenID Connect direct integration exampe](https://8z77681269.codesandbox.io/)

## Customizable Tenants

A PhantAuth rendkívül sokoldalúan testreszabható. Lehetőség van saját véletlenszerű felhasználó generátor service használatára, felhasználók külső CSV-ből vagy Google Sheet-ből történő generálására. A megjelenés testre szabható Bootstrap témák használatával, ezen kívül a megjelenés nagyobb mértékben megváltozattható egyéni HTML template-ek használatával. További részletek a [Tenant](tenant.md) fejezetben.

A testreszabás ún. tenant-ok segítségével történik. Egy egy tenant tekinthető úgy mint egy önálló PhantAuth szolgáltatás. A tenant-ok saját véletlenszerű felhasználó generátor végpontokkal valamint OpenID Connect végpontokkal rendelkeznek.

A tenant-ok ún. domain-ekbe szervezhetők. A domain gyakorlatilag egy DNS zóna, mely tartalmazza az egyes tenant-ok beállításait. A tenant-ok is s a domain maga is DNS TXT rekordok segítségével konfigurálhatók.

A PhantAuth Domain a default tenant mellett tartalmaz néhány példa tenant-ot, melyek elsősorban a testre szabhatóságot, különböző hosting lehetőségeket, külső szolgáltatások bekötését hivatottak demonstrálni. A legtöbb esetben elegendő a [default tenant](https://phantauth.net) használata.

 - [PhantAuth Default](https://phantauth.net) - default tenant, based on Java Fairy library
 - [Greek Gods](https://phantauth.net/_gods) - based on Google Sheet document
 - [PhantAuth Faker](https://phantauth.net/_faker) - based on Javascript Faker library, hosted at https://now.sh
 - [PhantAuth Chance](https://phantauth.net/_chance) - based on Javascript Chance library, hosted at https://now.sh
 - [PhantAuth Casual](https://phantauth.net/_casual) - based on Javascript Casual library, hosted at https://webtask.io
 - [RANDOM USER](https://phantauth.net/_randomuser) - based on https://randomuser.me service
 - [uinames](https://phantauth.net/_uinames) - based on https://uinames.com service
 - [Mockaroo](https://phantauth.net/_mockaroo) - based on  https://mockaroo.com service

A domain-t és tenant-okat bárki létrehozhat. Az egymás közötti egyszerűbb tenant megosztást segíti a [PhantAuth Shared Domain](https://shared.phantauth.net). A shared domain-hez a [phantauth.cf](http://phantauth.cf) DNS zóna tartozik, melyben bárki létrehozhat tenant konfigurációs bejegyzéseket a [FreeDNS](https://freedns.afraid.org/) szolgáltatás segítségével.

## Pricing

A PhantAuth ingyenes, nyílt forráskódú, non profit szolgáltatás. Amennyiben hasznosnak találja a szolgáltatást s teheti, kérjük járuljon hozzá támogatásával az üzemeltetési költségekhez (domain regisztráció, service hosting, stb).

[Donate on Ko-fi](https://ko-fi.com/Q5Q0T7C7) | [Donate on Liberapay](https://liberapay.com/szkiba/donate) | [Donate on PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=VXLCJ3EZRAE7G&source=url)
