# Integration

A PhantAuth elsősorban egy OpenID Connect Provider, mely támogatja az OpenID Connect specifikációban szereplő workflow-kat (Hybrid, Implicit, Authorization Code) valamint az OAuth 2.0 specifikációban szerepő Resource Owner grant type-ot. Az integrálás mikéntje az adott authentikációs library, vagy identity integrátor szolgáltatás lehetőségeinek megfelelően történik. Jelen dokumentum tartalmazza az integráláshoz szükséges információkat, módszereket, valamint néhány konkrét környezetbe történő integrálás lépéseit. 

# Parameters

Az integráláshoz jellemzően az alábbi paraméterek szükségesek:

 - [Issuer](#issuer)
 - [Discovery Endpoint](#discovery-endpoint)
 - [Authorization Endpoint](#authorization-endpoint)
 - [Token Endpoint](#token-endpoint)
 - [Client Credentials](#client-redentials)
 - [Scope](#scope)

## Issuer

Az Issuer URL azonosítja az OpenID Connect Providert, PhantAuth default [tenant](tenant.md) esetén az értéke:

```
https://phantauth.net
```

PhantAuth esetén az Issuer URL egy dokumentációs web lap is egyben, mely tartalmazza az adott [tenant](tenant.md) használatához szükséges információkat.

## Discovery Endpoint

Amennyiben az adott authentikációs library támogatja az OpenID Connect Discovery 1.0 specifikáció Obtain OpenID Provider Configuration Information fejezetében definiált konfigurációs protokollt, úgy nem szükséges a különböző végpontok egyedi konfiurálása. Bár a specifikáció rögzíti az Issuer URL-hez relatívan a Discovery Endpoint címét, néhány authentikációs library elvárja ennek manuális beállítását. PhantAuth default [tenant](tenant.md) esetén a Discovery Endpoint címe:

```
https://phantauth.net/.well-known/openid-configuration
```

## Authorization Endpoint

Mindhárom OpenID Connect Flow esetén szükséges az Authorization Endpoint címének megadása amennyiben az adott authentikációs library nem implementálja az OpenID Connect Discovery specifikációt. PhantAuth default [tenant](tenant.md) esetén az Authorization Endpoint címe:

```
https://phantauth.ml/auth/authorize
```

## Token Endpoint

Authorization Code Flow és Hybrid Flow esetén szükséges a Token Endpoint címének megadása amennyiben az adott authentikációs library nem implementálja az OpenID Connect Discovery specifikációt. PhantAuth default [tenant](tenant.md) esetén az Token Endpoint címe:

```
https://phantauth.ml/auth/token
```

## Client Credentials

## Scope

A PhantAuth támogatja az OpenID Connect specifikációban szereplő scope értékeket, így azok bármelyike használható. A felhasználó standard adatainak lekérdezéséhez az alábbi scope lista megadása szükséges:

```
openid profile email phone address
```

Bizonyos esetben a PhantAuth által visszaadott `sub` claim értéke túl hosszú az adott környezet (pl Auth0) számára. Ilyenkor használható a `uid` scope, mely az adott felhasználó rövidített felhasználói azonosítóját tartalmazó `uid` claim lekérését jelenti. Azaz a teljes támogatott scope lista:

```
openid profile email phone address uid
```

Az `uid` scope és claim nem szabványos, PhantAuth specifikus!

## User Info Endpoint

Rendszerint az authentikációs library-k nem igénylik a User Info Endpoint beállítását (egy két kivételtől eltekintve), azonban hasznos lehet az adott felhasználó adatainak lekérdezéséhez. PhantAuth default [tenant](tenant.md) esetén az User Info Endpoint címe:

```
https://phantauth.ml/auth/userinfo
```

## Client Registration Endpoint

A PhantAuth implementálja az OAuth 2.0 Dynamic Client Registration Protocol-t. Amennyiben az adott library támogatja a dinamikus regisztrációt, úgy nem szükséges a [Client Credentials](#client-credentials) pontban leírtaknak megfelelő credentials értékek beállítása. PhantAuth default [tenant](tenant.md) esetén a Client Registration Endpoint címe:

```
https://phantauth.ml/auth/register
```

## JWKS Endpoint

Rendszerint az authentikációs library-k nem igénylik a JWKS Endpoint beállítását. PhantAuth default [tenant](tenant.md) esetén értéke:

```
https://phantauth.ml/auth/jwks
```

# Samples

## Direct integration

 - [Direct OpenID Connect integration](https://www.phantauth.net/test/oidc)

## Auth0

 - [Auth0 Social Connections integration](https://www.phantauth.net/test/auth0)

## Azure AD B2C 

 - [Azure Active Directory B2C integration](https://www.phantauth.net/test/azure)