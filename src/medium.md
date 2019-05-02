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
