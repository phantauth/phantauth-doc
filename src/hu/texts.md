# Texts

A PhantAuth HTML oldalainak lokalizálása jelenleg manuális folyamat. Itt találhatók a különböző oldalakon, template-ekben megjelenő rövidebb szöveg részletek, melyeket a PhantAuth lokalizálásához le kell fordítani.

## tenant.html

https://phantauth.net | https://phantauth.net/_

### Issuer

This is the issuer endpoint for *PLACEHOLDER* tenant. You can get OpenID Connect endpoint addresses and client credentials here.

### Test Page

You can test authentication on tenant's *OpenID Connect Test* page or you can try random user generation on *Random User Test page*.

### Domain

This domain tenant aggregates several other tenants. Before actual tenant login, user should select which tenant to use. The table below shows the aggregated member tenants. You can use member tenants directly as issuer or domain tenant as aggregating issuer. If you are not care about tenants, lets use *PhantAuth Default* as issuer.

### OpenID Connect Endpoints

The table bellow contains standard OpenID Connect Endpoint addresses. You don't need to enter these endpoint addresses manually, if your provider/library supports OpenID Connect Discovery. In this case you should give ony the issuer location, or discovery location (depens on implementation).

### Client registration

You do not need to register your client software, just pick a client_id and use it. Some OpenID Connect workflow require client_secret. Just type your client_id in the input box bellow and press generate button. You will see your client_secret next to the client_id. The generated logo and software name will displayed too. Leaving empty the client_id field, you can generate random client_id and client_secret. 

Check *PhantAuth Developer Portal* for more information.

### Resource Endpoints

This tenant generate users using client side script so not all resource endpoints are exposed.

The table bellow contains REST endpoints for random generated resources. 

Check *PhantAuth API documentation* for more information.

### Configuration

The table bellow contains tenant configuration parameters. These parameters are coming from tenant's DNS zone.

## test.html

### User

User Genarator test page for PLACEHOLDER tenant.

A *generate* gomb segítségével generálhat új random user-t. A *Login name or blank* mezőben adható meg a generálandó user login neve. Amennyiben megadja, úgy a user a login név alapján generálódik. Ellenkező esetben a *generate* gomb megnyomásával minden esetben új user generálódik.

### OpenID

OpenID Connect authentication test page for PLACEHOLDER tenant. 

Kipróbálhatja hogyan működik az OpenID Connect authentikáció ezzel a tenant-tal. A sikeres authentikációt követően egy user profile oldalt fog látni melyen az IdToken-ből származó claim-ek jelennek meg. A visszaadott claim-ek száma függ a tenant által használt random generátortól.

## auth0.html

Auth0 integration test page. You can try how authentication works with Auth0 Social Connection integration. After successfull authentication you will see returned OIDC claims in a user profile form. This page uses *Auth0.js SDK* for authentication.

A bejelentkezés első lépéseként ki kell választani az authentikációs forrást. A három választási lehetőség:

 - PhantAuth: a PhantAuth default tenant használata bejelentkezéshez

 - Sketch: a PhantAuth Sketch tenant használata bejelentkezéshez

 - Domain: a PhantAuth tenant-okat összefogó domain tenant használata bejelentkezéshez. Ez esetben egy újabb lapon kell kiválasztani az összes lehetséges tenant közül (6-8 db) a használni kívántat

Sikeres bejelentkezést követően a profile lap jelenik meg. Innen a *logout* gomb segítségével ki lehet jelentkezni s újrapróbálható a bejelentkezés.

## aure.html

Azure AD B2C integration test page. You can try how authentication works with Azure AD B2C integration. After successfull authentication you will see returned OIDC claims in a user profile form. This page uses *Microsoft Authentication Library* for Javascript for authentication.

A bejelentkezés első lépéseként ki kell választani az authentikációs forrást. A három választási lehetőség:

 - LOG IN WITH PHANTAUTH: a PhantAuth default tenant használata bejelentkezéshez

 - LOG IN WITH SKETCH: a PhantAuth Sketch tenant használata bejelentkezéshez

 - LOG IN WITH DOMAIN: a PhantAuth tenant-okat összefogó domain tenant használata bejelentkezéshez. Ez esetben egy újabb lapon kell kiválasztani az összes lehetséges tenant közül (6-8 db) a használni kívántat

Sikeres bejelentkezést követően a profile lap jelenik meg. Innen a *logout* gomb segítségével ki lehet jelentkezni s újrapróbálható a bejelentkezés.
