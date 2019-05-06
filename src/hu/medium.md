# Medium

Az alábbi írások olyan gondolatokat, ötleteket mutatnak be, melyek következményeként született meg a PhantAuth project. Az írás időpontjában már elkészült a PhantAuth, ily módon az alábbiak nem csak elméleti ötleteknek tekintendők, megvalósíthatóságukat működő implementáció igazolja. Az egyes írások Medium.com cikkekként jelennek (jelentek) meg.

# How to get unlimited number of test users?

> Testing OpenID Connect authenticated applications with random generated users.

**Authentikált alkalmazások tesztelése nem egyszerű**, rendszerint szükség van hozzá előre generált teszt felhasználókra. Külső Identity Provider-t használó alkalmazásoknál a helyzetet tovább bonyolítja, hogy a teszt felhasználókat az Identity Provider-nél (Facebook, Google, stb) kellene létrehozni.

Ideális esetben a teszt az előkészítő lépések során automatikusan létre hozza a teszt felhasználókat a külső Identity Provider-nél majd a teszt futását követően megszünteti őket. Még ha az Identity Provider lehetőséget is ad ilyen műveletekre, ez speciális jogosultásgokat igényel a teszt futtása során.

## Fake Identity Provider

A külső Identity Provider-t használó alkalmazások rendszerint több külső provider-t képesek használni, azaz több külső Identity Provider-t integrálnak. Léteznek olyan Identity Provider-ek, melyek eleve több külső Identity Provider-t integrálnak levéve ezzel a különböző integrációk nehézégeit az alkalmazás fejlesztő váláról.

Azaz egy újabb Identity Provider integrálása tesztelési céllal többnyire nem okoz nagy nehézséget, különösen ha ez a provider standard OpenID Connect provider. Tehát a teszt felhasználók kezelésére egy lehetséges megoldás egy speciális Fake Identity Provider integrálása s használata.

A teszt az előkészítés során létrehozhat tetszőleges számú, az adott teszthez szükséges teszt felhasználót, majd a teszt futása után törölheti azokat. Az alkalmazás a Fake Identity Provider-t ugyanolyan OpenID Connect Provider-nek látja mint bármely más provider-t.

Authentikáció integrátor szolgáltatáson keresztül (pl Auth0, Amazon Cognito, Azure AD B2C, stb) a Fake Indetity Provider akár az alkalmazás módosítása nélkül is beköthető.

## Random User Generator

A teszt felhasználók létrehozásához, különösen ha nagy mennyiségről van szó, célszerű valamilyen Random User Generator tool-t vagy szolgáltatást használni. A teszt előkészítéseként tehát a Random User Generator által generált felhasználókat be kell tölteni a Fake Identity Provider-be, a futást követően pedig célszerű törölni onnan.

## Fake Identity Generator

Mi lenne, ha a Random User Generator-t kereszteznénk a Fake Identity Provider-rel? Az így kapott Fake Identity Generator alkalmas lenne felhasználók véletlenszerű generálására, valamint ezen felhasználók authentikációjára OpenID Connect protokollal. Amennyiben a felhasználók generálása a login név alapján történik determinisztikus módon, úgy a felhasználók adatainak tárolása sem szükséges, hiszen bármikor újragenerálhatók.

## Unlimited number of test users

Fake Identity Generator birtokában a tesztek korlátlan számú teszt felhasználóval rendelkeznek, anélkül hogy le kellene gyártaniuk ezeket a teszt felhasználókat, hiszen tetszőleges login névhez a Fake Identity Generator automatikusan gyárt felhasználót, s szolgáltat hozzá authentikációt. Szükség esetén a teszt lekérheti az adott login névhez tartozó teszt felhasználót a Fake Identity Generator-tól.

## Is it theoretical?

Nem. Az authentikált alkalmazások tesztelése valós probléma, melyre valós megoldást kerestem. A fenti gondolatok mentén készült a PhantAuth névre hallgató Fake Identity Generator, mely nem más mint egy Random User Generator és egy OpenID Connect Provider ötvözése. **Ingyenes szolgáltatásként az alábbi címen érhető el**: https://www.phantauth.net

## Best Practice

Külső authentikáció használata esetén célszerű a nagyobb Identity Providereket (Facebook, Google) direkt módon integrálni, a többi Identity Provider-t pedig valamely integrator szolgáltatáson (pl Auth0) keresztül. A teszteléshez az arra használt környezetekben (dev, test) célszerű a PhantAuth Fake Identity Generatort az authentikációs integrator-on keresztül (pl Auth0) bekötni az alkalmazás módosítása nélkül.

# Random User Generator vs Deterministic User Generator

> Use determinitic test user generator instead of loading random user data

User authentikációt használó rendszerek tesztelése esetén visszatérő feladat a véletlenszerű felhasználó generálás. Számos library létezik véletlenszerű felhasználó generálásra valamint léteznek REST service-ek is hasonló céllal.

Ezen generátorok többnyire pseudorandom number generator alapúak s lehetővé teszik a generátor induló seed értékének megadását. Ily módon ha egyszer legenerálunk pl 100 db felhasználót egy adott seed értékből kiindulva, úgy ugyanazt a 100 db felhasználót ugyanazon seed érték felhasználásával bármikor újra le tudjuk generálni. Ez annak köszönhető, hogy a pseudorandom number generator egy olyan véletlennek tűnő számsort állít elő, melyet az induló seed érték egyértelműen meghatároz. Mivel a felhasználók minden jellemzőjének generálása során ezt a számsort használják a generátorok, így a generált felhasználókat is meghatározza a generátor induló seed értéke.

Ez érdekes, de nem tűnik különösen hasznosnak.


# distributed service configuration database for free

> Use DNS as service configuration database

Bár rendszerint nem így gondolunk rá, de az internet egyik legrégebbi s leggyakrabban használt disztributált, key-value alapú konfigurációs adatbázisa a Doman Name System (DNS).

A legtöbbünknek a nevek feloldása, a domain regisztráció, a köré épülő, olykor spekulatív domain név kereskedelem jut eszébe a DNS kapcsán. Valóban a DNS egyik elsődleges feladata a domain nevek IP címre történő feloldása. Kevésbé ismert, hogy a név feloldáson kívül számos különböző információ megisztására használható és használatos a DNS. Ezek egyike az úgynevezett TXT resource record, amikor is a domain névhez tetszőleges szöveges információ rendelhető.

A TXT resource record tehát egy key/value bejegyzés, azaz alkalmas konfigurációs property-k tárolására.

## Előnyök

A DNS alapvetően egy **disztributált** rendszer. Az adatok az adott donain-t kiszolgáló névszerverek között automatikusan frissülnek.

Amennyiben egy kliens egy domain név feloldását kezdeményezi, úgy a köztes névszerverek **automatikusan cache-elik** a választ. Azaz a domain saját névszerverein kívül számos egyéb névszerver is részt vesz az információ cache-elésében annak érdekében, hogy az minél gyorsabban eljusson a klienshez. 

A DNS egy **ingyenes** key/value adatbázis, a benne tárolt adatokért a szolgáltatók nem számolnak fel külön költséget. Léteznek teljesen ingyenes DNS névszerver szolgáltatók is (pl [CloudFlare](https://www.cloudflare.com), [Hurricane Electric](https://dns.he.net)), amikor magáért a domain kezeléséért sem kell fizetni. Ezen kívül léteznek ingyenes DNS domain regisztrációs szolgáltatások (pl [Freenom](https://www.freenom.com)), melyek használatával bizonyos top level domain-eken belül ingyenesen regisztrálhatók domain nevek.

## Hátrányok

A DNS-ben tárolt adatok **publikusan** elérhetők, azaz nem szabályozható, hogy ki mely adathoz férhet hozzá. Konfiguráció DNS-ben tárolása esetén ez okozhat problémát, ugyanis lehetnek érzékeny konfigurációs adatok. Ez ezen adatokat vagy nem DNS-ben célszerű tárolni, vagy titkosítva érdemes tárolni őket.

A cache miatt a változások csak **késleltetve** jelennek meg. A késleltetés maximális mértéke a cache úgynevezett time to live (ttl) értékével azonos. Ennek ajánlott minimum értéke 5 perc, de bizonyos szolgáltatók (pl CloudFlare) ettől rövidebb értékek (pl 2 perc) használatát is megengedik. E késleltetés rendszerint nem probléma, azonban a késleltetés miatt pillanatszerű konfiguráció váltásra nem alkalmas.

A disztributáltság és a cache következményeként a DNS-ben tárolt adatok nem mindig konzisztensek, leginkább **eventually consistent**-nek tekinthetők. Az eseteg többségében ez nem okoz problémát, azonban atomikus konfiguráció cserére ezen tulajdonsága miatt nem alkalmas.

A TXT rekordokban tárolt **érték mérete limitált, maximum 255 karakter** hosszú lehet. Pontosabban egy string érték, ugyanis ugyanazon névhez több érték is rendelhető, de ezeket már a kliensnek kell kezelnie, összefűznie. A konfigurációs beállítások tölbbségénél ez nem jelent problémát.

## Megvalósítás

Tetszőleges string értékek tárolhatók egy adott domain névhez tartozó TXT recordban, valamint egy domain névhez több érték is tárolható. Ez lehetővé tesz egy olyan mappelést amikor is a konfigurációs property-k a domain nevek, a konfigurációs property értékek pedig egyszerűen a névhez tartozó TXT rekord értékei. Ezzel a mappinggel akár a tömb típusú konfigurációs property értékek is természetes módon kezelhetők.

```
property1   120	IN	TXT	"value1"
property2   120	IN	TXT	"value2"
array1      120	IN	TXT	"item2"
array1      120	IN	TXT	"item1"
```

Egy másik lehetséges mapping, amikor a domain név csak a konfigurációs objektumot azonosítja s a konfigurációs property-k s értékeik a domain névhez tartozó TXT rekordba kerülnek property=value formátumban.

```
	        120	IN	TXT	"property1=value1"
            120	IN	TXT	"property2=value2"
            120	IN	TXT	"array1=item1"
            120	IN	TXT	"array1=item2"
```

Ez utóbbi megoldás előnye, hogy létezik RFC mely ezt a fajta mappinget definiálja ([RFC 1464](https://tools.ietf.org/html/rfc1464), [RFC 6763](https://tools.ietf.org/html/rfc6763)), s ebből adódóan elterjedtebb, több opensource tool támogatja (pl [sdget](https://github.com/govau/sdget))

## When to use

Amennyiben a service üzemeltetést függetleníteni szeretnénk a konfiguráció kezeléstől, azaz **delegálni** szeretnénk a konfiguráció kezelést, abban az esetben kimondottan jól használható a DNS alapú konfiguráció.

Képzeljünk el egy szolgáltatást, melynek készítője/üzemeltetője szeretné ha szolgáltatás anélkül lenne testreszabható, hogy felhasználó regisztrációt, konfiguráció kezelő felületet készítene hozzá vagy anélkül hogy a felhasználók saját példányt üzemeltessenek a szolgáltatásból. Ez esetben kézenfekvő megoldás a konfigurációt delegálni a felhasználónak DNS TXT rekordokon keresztül. Így a service számára elegendő egyetlen paraméterként a domain név, s a konfigurációt ezen domain névhez tartozó TXT rekordokban várja. A DNS elérése kellően gyors, ismételt elérése gyorsabb mint bármely key/value adatbázisé, lévén nem csak a DNS szerverek de az adott futtató környezet lokális DNS resolvere is cache-eli a DNS adatokat. Ugyanakkor a konfigurációt a felhasználók szabadon szerkeszthetik a saját domain nevük alatt.

## Példák

Számos URL redirect szolgáltatás létezik. Ezek többnyire saját adminisztrációs felülettel rendelkeznek s megkövetelik a felhasználótól a regisztrálást. A [redirect.name](https://redirect.name/) ezzel szemben regisztráció nélkül tesz lehetővé URL átirányítást, oly módon, hogy az átirányítás konfigurációját a felhasználó domain-jában elhelyezett CNAME és TXT rekordokban várja.

A [Forward Email](https://forwardemail.net) szolgáltatás email-ek továbbítását teszi lehetővé custom domain-ek számára. A továbbítási konfigurációt az adott domain-hez tartozó TXT rekordokban várja, így a használatához nem szükséges regisztráció.

A [DNS-Based Service Discovery](https://tools.ietf.org/html/rfc6763) számos microservices környezetben alapja vagy kiegészítő megoldása a service discovery-nek. Jó példa erre a [SkyDNS](https://github.com/skynetservices/skydns) vagy a [HashiCorp Consul](https://www.consul.io/docs/agent/dns.html).

A fenti példák inspirálták a [PhantAuth - Random User Generator + OpenID Connect Provider](https://www.phantauth.net) tenant konfiguráció kezelését, mely szintén DNS alapú. A szolgáltatás tenant-okon keresztül szabható testre. Egy-egy tenant nem más mint egy DNS név s a hozzá tartozó TXT rekordok tartalmazzák a testreszabás paramétereit. Így a rendszer felhasználói anélkül módosíthatják a szolgáltatás működését, hogy saját példányt futtatnának belőle. A testreszabás odáig terjed, hogy akár külső plugin jellegű modulok is bekonfigurálhatók, melyeket a PhantAuth REST API-n keresztül hív.
