FORMAT: 1A
HOST: https://phantauth.net/

# PhantAuth

Random User Generator + OpenID Connect Provider. Like Lorem Ipsum, but for user accounts and authentication.

## User [/user]

A *user* resource az [OpenID Connect Core](https://openid.net/specs/openid-connect-core-1_0.html) specifikációban definiált [Standard Claims](https://openid.net/specs/openid-connect-core-1_0.html#StandardClaims)-eket tartalmazza, kiegészítve néhány PhantAuth specifikus property-vel.

### Get a User [GET /user/{username}]

Ezen végpont használatával véletlenszerű felhasználó generálható. A generálás a path paraméterként megadott felhasználó név alapján történik, determinisztikus módon. Ugyanazon felhasználói név esetén a végpont ugyanazt a user objektumot generálja. A generált user objektum property-ei a felhasználó név alapján véletlenszerűen generálódnak.
A felhasználó név elhagyása esetén minden hívás különböző, véletlenszerűen generált felhasználó névhez tartozó user objektumot generál.

+ Parameters
   + username (optional, string) ... a generáláshoz használt username vagy email

+ Response 200 (application/json)

    + Attributes (User)

    + Body
    
            {
                "locale": "en_US",
                "profile": "https://phantauth.net/user/john.smith/profile",
                "nickname": "John",
                "preferred_username": "jsmith",
                "picture": "https://www.gravatar.com/avatar/54c27dd1891df67163ef53616549933f?s=256&d=https://avatars.phantauth.net/ai/male/Vyb8Yrdv.jpg",
                "sub": "john.smith",
                "website": "https://phantauth.net",
                "email": "john.smith.XPKEFHI@mailinator.com",
                "email_verified": false,
                "gender": "male",
                "birthdate": "1950-02-10",
                "zoneinfo": "America/Chicago",
                "phone_number": "747-178-7374",
                "phone_number_verified": true,
                "updated_at": 1518220800,
                "me": "https://phantauth.net/~john.smith",
                "password": "Opha8TV2",
                "webmail": "https://www.mailinator.com/v3/?zone=public&query=john.smith.XPKEFHI",
                "uid": "tf+gMsdUWj0",
                "family_name": "Smith",
                "given_name": "John",
                "address": {
                    "street_address": "160 Washington Walk",
                    "formatted": "160 Washington Walk\nSan Francisco 98239",
                    "locality": "San Francisco",
                    "postal_code": "98239",
                    "country": "USA"
                },
                "name": "John Smith",
                "@id": "https://phantauth.net/user/john.smith"
            }

### Create a User Selfie [POST]

Selfie token létrehozása felhasználói adatokból. A válasz egy opaqe string token, mely a request-ben küldött user property-ket tartalmazza titkosítot formában.
A selfie token a későbbiekben felhasználható mint belépési név. Ilyenkor a felhasználó adatait a selfie token hordozza, azaz a felhasználó property-jei a token-ből kerülnek kiolvasásra.
A selfie token segítségével lehetőség saját felhasználói objektumok használatára authentikáció során.

Használatát limitálja viszonylag nagy mérete (nagyobb mint 100 karakter), mely sok rendszerben meghaladja a megengedett maximális felhasználói név méretét.

+ Request (application/json)

    + Attributes (User)
  
    + Body
    
              {
                "sub": "john.smith",
                "locale": "en_US",
                "nickname": "John",
                "preferred_username": "jsmith",
                "picture": "https://www.gravatar.com/avatar/54c27dd1891df67163ef53616549933f?s=256&d=https://avatars.phantauth.net/ai/male/Vyb8Yrdv.jpg",
                "email": "john.smith.XPKEFHI@mailinator.com",
                "email_verified": false,
                "gender": "male",
                "birthdate": "1950-02-10",
                "zoneinfo": "America/Chicago",
                "phone_number": "747-178-7374",
                "phone_number_verified": true,
                "updated_at": 1518220800,
                "password": "Opha8TV2",
                "family_name": "Smith",
                "given_name": "John",
                "address": {
                    "street_address": "160 Washington Walk",
                    "formatted": "160 Washington Walk\nSan Francisco 98239",
                    "locality": "San Francisco",
                    "postal_code": "98239",
                    "country": "USA"
                },
                "name": "John Smith"
            }

+ Response 200 (text/plain)

    + Body
    
            eyJlbmMiOiJBMjU2R0NNIiwiYWxnIjoiZGlyIn0..3FlrxAUU5W8t31Rw.2JMhWkDz4aTGnvo4f2T5htzwwtzaUYbNzDZ4zAiqCepjhM5IX6pZMDQohr2M3u5liARhiObS1j1wlpNRdYz6YIDaLNZoRwHml-5LY8s8_1lgC4EQqAag3z9qrCoxc4LCkinruwQAeYuFiGq0YB6pp2FzQKDYh41RA_t3sgqsKAPG3Ql7X_Z0NMa0wMaBYxTLHn-lPbZOSWu3-nQzNQ8652HuBDY3JubCt_0hOBGCuhjrIX1fmq8RJb61pNFvWuJ8CHhx6fAoWi0hCETkYJ27gnrOy_jiPIThcyLrB7pouQ9Xs9xXtPdumfRScX7zx-kE9j_RyJ-HEG7WLBZkKJSHfqMCKB3dVxVdJ6DE3cYkADBb7J_8YLOKgMv1Jiw9yEZjoTQ39LtPBVCsubLPuI3k1SrYvZchNfJWbkFr9YlB46UzTnkt3VYvPfstLYXpYl--o9UIbZMM2wtyi24Szoq-GvPtNRXLvAZt2QeMB8ZGqPC7DcCgs4pba4X1uS0b_-oyjmI1azCve-5ov5UQZ9VRjBiVf3IlMFs2276A5hsxm-x-JcspBD4T83iSzObEnYM5gVX2FLD_QPt61TYknufuSkFyhgSyM8Zw4s1L4zLCljEqtGWFzOg3KrpKH7b4NQN1nuY2NEkhVrrAKZJeUM55KMRXdBTXTUOyWk2hObZs325_2F9mjYE1QTnGHHhuzFLT0uRxxf1HmcguzTfeorwk626Ed_VtSDygH0wbHuV7YOlt6VYkuEknzqS62NINPNkuvCKmkBjl1tIeCaaXXMb_fVcTL-9rueG9YxY4RpX0tvPN25zwuj3wXiEh11YlUnmD3zFh3QoKbJ0GQc8Xc5z0vj59NXMPQUC36xQ0O7KVIY7uKYbKVf71wtKY2rq4sYuWbm0vdOiab0lzvYv3-R5v79KPuq03AyPZeWOfmSPpnTRo4WA6geXID-KAEFkboL_SxHU7r--MpqL2tFeF7nS2IFNYjRchr19LWqZ9bvXtEyfsiqgQAzPmGOQ.QPl0yBPkyUxlb7WuxcOmeA

### Get a User Token [GET /user/{username}/token/{kind}{?scope}]

Különböző OpenID Connect token-ek generálása a path paraméterként megadott nevű felhasználóhoz.

Elsősorban tesztelés során használatos, amikor pl a normál authentication flow során kapott token nem elérhető s teszt kód számára.

+ Parameters

    + username (required, string) ... username or email
    + kind (required, enum[string]) 
    
      Token type
    
      + Members
          + 'access'
          + 'refresh'
          + 'authorization'
          + 'id'
          + 'selfie'
          + 'plain'

    + scope (optional, string) ... OpenID Connect scope

+ Response 200 (text/plain)

    + Body
    
            eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJqb3NoLnNtaXRoIiwidG9rZW5fa2luZCI6IkFDQ0VTUyIsInNjb3BlIjoib3BlbmlkIHByb2ZpbGUgZW1haWwgYWRkcmVzcyBwaG9uZSBpbmRpZWF1dGggdWlkIiwiZXhwIjoxNTU2ODg5NzcxLCJpYXQiOjE1NTY4ODkxNzF9.YBQ_6GlQ1iXjk6OKU7meJhlg3iRDEgeTqnBFdeLDJyI

## Client [/client]


### Get a Client [GET /client/{client_id}]

Ezen végpont használatával véletlenszerű kliens generálható. A generálás a path paraméterként megadott client id alapján történik, determinisztikus módon. Ugyanazon client id esetén a végpont ugyanazt a client objektumot generálja. A generált client objektum property-ei a client id alapján véletlenszerűen generálódnak.
A client id elhagyása esetén minden hívás különböző, véletlenszerűen generált client id-hez tartozó client objektumot generál.

+ Parameters
   + client_id (optional, string) ... client id or email

+ Response 200 (application/json)

    + Attributes (Client)
    
    + Body
    
            {
                "client_id": "magic.toolbox",
                "client_secret": "O68dVlLk",
                "client_name": "Magic Toolbox",
                "client_uri": "https://phantauth.net/client/magic.toolbox/profile",
                "logo_uri": "https://www.gravatar.com/avatar/23a9c0277d8e4062b01f1097037f0d5b?s=256&d=https%3A%2F%2Favatars.phantauth.net%2Ficon%2F9b68RVeE.png",
                "logo_email": "magic.toolbox.OUUWE4A@mailinator.com",
                "tos_uri": "https://phantauth.net/client/magic.toolbox/tos",
                "policy_uri": "https://phantauth.net/client/magic.toolbox/policy",
                "software_id": "igG6Jgx7mfzPdjhBvHvqRQ",
                "software_version": "3.8.0",
                "@id": "https://phantauth.net/client/magic.toolbox"
            }

### Create a Client Selfie [POST]

Selfie token létrehozása client adatokból. A válasz egy opaqe string token, mely a request-ben küldött client property-ket tartalmazza titkosítot formában.
A selfie token a későbbiekben felhasználható mint client id. Ilyenkor a client adatait a selfie token hordozza, azaz a client property-jei a token-ből kerülnek kiolvasásra.
A selfie token segítségével lehetőség saját client objektumok használatára authentikáció során.

+ Request (application/json)

  + Attributes (Client)
  
  + Body
  
            {
                "client_id": "magic.toolbox",
                "client_secret": "O68dVlLk",
                "client_name": "Magic Toolbox",
                "logo_uri": "https://www.gravatar.com/avatar/23a9c0277d8e4062b01f1097037f0d5b?s=256&d=https%3A%2F%2Favatars.phantauth.net%2Ficon%2F9b68RVeE.png",
                "logo_email": "magic.toolbox.OUUWE4A@mailinator.com",
                "tos_uri": "https://phantauth.net/client/magic.toolbox/tos",
                "policy_uri": "https://phantauth.net/client/magic.toolbox/policy",
                "software_id": "igG6Jgx7mfzPdjhBvHvqRQ",
                "software_version": "3.8.0"
            }

+ Response 200 (text/plain)

    + Body
    
            eyJlbmMiOiJBMjU2R0NNIiwiYWxnIjoiZGlyIn0..HQLixaDFwfYXZ2Hu.p4zIoe54Cg3W1hQR2yIXbWMg5fC9X66si7jhz7IuB2-_2m8VuYMP6V3-e3sFsPfZsHlxpdtuSZ5eYphb5qnN-tHEEhnu2OBQDLH6FVmofpSdXVsastRiN7BcESH6-3FaJmsS-gs-C-RFn9YmlE9OdCt2CFwca5584SmSwd5lqC87ljgjKn1afPKTPqG8esxNsj3h_1qkjdzArCo94B-0Gq_dLN3vNImCW0Y9rV4ThviZQh1rFCwD1-hotmsVRwZcGIxGmQd6KtqS9MtSimdFB29QtPm64htB8OPiUZSUeD5MhYty2UyYsru-coyd4Uye59jj8LQWQOi6K5mO46sM6rOOKpVYBDMRyfKZHtw0SEjLKJYFadtnZ4kAAe7faZB8prY50FG-BtVnsWVQRbpbIeuih-iGk-X-5kQ3MEbXcBLkBIEwjVEKT7s9zjLV1NzWNeQHadzMxAa_jMRZi5bpcUxHT5GctLVVRP5_iCQX0lrh7dDkV5oNmxVj0JT7f0Fada709a9uAiVzcQa3maBWx8u7moxMhHT-CeTGXFiGRkKC3q-tXzRItaAFFhYDv38Efj23sTBwjjyK3ldWyhwVXOenzmQP9aesj8lgz0jtpzcjkW_ckRz_POM_fTF-y6M_bHb1eloCXaGem8mfTWBqWydUUWEsH6hmSI5pkmTS2k_9TQ.fu0lDi24J2c1a33NTNwU7g

### Get a Client Token [GET /client/{client_id}/token/{kind}]

Különböző OpenID Connect token-ek generálása a path paraméterként megadott nevűcliend id-jű client-hez.

Elsősorban tesztelés során használatos, amikor pl a normál authentication flow során kapott token nem elérhető s teszt kód számára.

+ Parameters

    + client_id (required, string) ... client id or email
    + kind (required, enum[string]) 
    
      Token type
    
      + Members
          + 'registration'
          + 'selfie'
          + 'plain'

+ Response 200 (text/plain)

    + Body

            eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJtYWdpYy50b29sYm94IiwidG9rZW5fa2luZCI6IlJFR0lTVFJBVElPTiIsInNjb3BlIjoib3BlbmlkIHByb2ZpbGUgZW1haWwgYWRkcmVzcyBwaG9uZSBpbmRpZWF1dGggdWlkIiwiZXhwIjoxNTg4NDI4NDM4LCJpYXQiOjE1NTY4OTI0Mzh9.TGilMHuWIDYiBAjzXyMuBvMiRlnKFLDX7FJJW_flldg


## Team [/team]

### Get a Team [GET /team/{teamname}]

Ezen végpont használatával felhasználók egy csoportja generálható véletlenszerűen. A generálás a path paraméterként megadott team név alapján történik, determinisztikus módon. Ugyanazon team név esetén a végpont ugyanazt a team objektumot generálja. A generált team objektum member user-ei és team property-ei a team név alapján véletlenszerűen generálódnak.
A team név elhagyása esetén minden hívás különböző, véletlenszerűen generált team névhez tartozó team objektumot generál.

+ Parameters
   + teamname (optional, string) ... teamname or email

+ Response 200 (application/json)

    + Attributes (Team)

    + Body
    
            {
                "sub": "dream.team",
                "name": "Dream Team",
                "profile": "https://phantauth.net/team/dream.team/profile",
                "logo": "https://www.gravatar.com/avatar/0d6fbd4eb21c269933ca5bba043ab4aa?s=256&d=identicon",
                "logo_email": "dream.team.HIECLNQ@mailinator.com",
                "@id": "https://phantauth.net/team/dream.team",
                "members": [
                    {
                        "locale": "en_US",
                        "profile": "https://phantauth.net/user/ariana.riley.hudson/profile",
                        "nickname": "Ariana",
                        "preferred_username": "ahudson",
                        "picture": "https://www.gravatar.com/avatar/8b0562dd7dd8ff1d8d872fcf58972d6d?s=256&d=https://avatars.phantauth.net/ai/female/BeXDnkey.jpg",
                        "sub": "ariana.riley.hudson",
                        "website": "https://phantauth.net",
                        "email": "ariana.riley.hudson.VJ2ABXA@mailinator.com",
                        "email_verified": false,
                        "gender": "female",
                        "birthdate": "1938-11-19",
                        "zoneinfo": "America/Chicago",
                        "phone_number": "552-769-0026",
                        "phone_number_verified": true,
                        "updated_at": 1542585600,
                        "me": "https://phantauth.net/~ariana.riley.hudson",
                        "password": "cuTCy0IZ",
                        "webmail": "https://www.mailinator.com/v3/?zone=public&query=ariana.riley.hudson.VJ2ABXA",
                        "uid": "1sKcrGacQtY",
                        "family_name": "Hudson",
                        "given_name": "Ariana",
                        "middle_name": "Riley",
                        "address": {
                            "street_address": "62 Highland Place APT 63",
                            "formatted": "62 Highland Place APT 63\nMiami 30927",
                            "locality": "Miami",
                            "postal_code": "30927",
                            "country": "USA"
                        },
                        "name": "Ariana Hudson",
                        "@id": "https://phantauth.net/user/ariana.riley.hudson"
                    },
                    {
                        "locale": "en_GB",
                        "profile": "https://phantauth.net/user/madeline.randall/profile",
                        "nickname": "Madeline",
                        "preferred_username": "mrandall",
                        "picture": "https://www.gravatar.com/avatar/eb3bac3d1654c56efbb93645770e5a60?s=256&d=https://avatars.phantauth.net/ai/female/pmbkErez.jpg",
                        "sub": "madeline.randall",
                        "website": "https://phantauth.net",
                        "email": "madeline.randall.P545AFI@mailinator.com",
                        "email_verified": true,
                        "gender": "female",
                        "birthdate": "1966-08-28",
                        "zoneinfo": "Europe/London",
                        "phone_number": "747-136-9890",
                        "phone_number_verified": true,
                        "updated_at": 1535414400,
                        "me": "https://phantauth.net/~madeline.randall",
                        "password": "xi89SZWX",
                        "webmail": "https://www.mailinator.com/v3/?zone=public&query=madeline.randall.P545AFI",
                        "uid": "5xjXrNaK8eU",
                        "family_name": "Randall",
                        "given_name": "Madeline",
                        "address": {
                            "street_address": "140 Atkins Avenue APT 126",
                            "formatted": "140 Atkins Avenue APT 126\nSan Francisco 48571",
                            "locality": "San Francisco",
                            "postal_code": "48571",
                            "country": "UnitedKingdom"
                        },
                        "name": "Madeline Randall",
                        "@id": "https://phantauth.net/user/madeline.randall"
                    },
                    {
                        "locale": "fr_CA",
                        "profile": "https://phantauth.net/user/alexa.brooklyn.rollins/profile",
                        "nickname": "Alexa",
                        "preferred_username": "arollins",
                        "picture": "https://www.gravatar.com/avatar/404e4bf6b700625b670d84336fa38d52?s=256&d=https://avatars.phantauth.net/ai/female/pmbkyvez.jpg",
                        "sub": "alexa.brooklyn.rollins",
                        "website": "https://phantauth.net",
                        "email": "alexa.brooklyn.rollins.WHW7KNY@mailinator.com",
                        "email_verified": false,
                        "gender": "female",
                        "birthdate": "1920-02-29",
                        "zoneinfo": "Canada/Central",
                        "phone_number": "335-295-2273",
                        "phone_number_verified": true,
                        "updated_at": 1519776000,
                        "me": "https://phantauth.net/~alexa.brooklyn.rollins",
                        "password": "8h3tEVhM",
                        "webmail": "https://www.mailinator.com/v3/?zone=public&query=alexa.brooklyn.rollins.WHW7KNY",
                        "uid": "ji7mQ76imjY",
                        "family_name": "Rollins",
                        "given_name": "Alexa",
                        "middle_name": "Brooklyn",
                        "address": {
                            "street_address": "104 Herzi Street APT 39",
                            "formatted": "104 Herzi Street APT 39\nWashington 22412",
                            "locality": "Washington",
                            "postal_code": "22412",
                            "country": "Canada"
                        },
                        "name": "Alexa Rollins",
                        "@id": "https://phantauth.net/user/alexa.brooklyn.rollins"
                    },
                    {
                        "locale": "en_AU",
                        "profile": "https://phantauth.net/user/cameron.barnes/profile",
                        "nickname": "Cameron",
                        "preferred_username": "cbarnes",
                        "picture": "https://www.gravatar.com/avatar/6cc04628ef7fb47eaa9a262b56b61e7d?s=256&d=https://avatars.phantauth.net/ai/male/wdL96rej.jpg",
                        "sub": "cameron.barnes",
                        "website": "https://phantauth.net",
                        "email": "cameron.barnes.UW4JUXI@mailinator.com",
                        "email_verified": false,
                        "gender": "male",
                        "birthdate": "1960-07-17",
                        "zoneinfo": "Australia/Sydney",
                        "phone_number": "449-465-925",
                        "phone_number_verified": true,
                        "updated_at": 1531785600,
                        "me": "https://phantauth.net/~cameron.barnes",
                        "password": "OL4y4cpb",
                        "webmail": "https://www.mailinator.com/v3/?zone=public&query=cameron.barnes.UW4JUXI",
                        "uid": "N4DJJyHMhUg",
                        "family_name": "Barnes",
                        "given_name": "Cameron",
                        "address": {
                            "street_address": "139 Aster Court",
                            "formatted": "139 Aster Court\nNew York 20333",
                            "locality": "New York",
                            "postal_code": "20333",
                            "country": "Australia"
                        },
                        "name": "Cameron Barnes",
                        "@id": "https://phantauth.net/user/cameron.barnes"
                    },
                    {
                        "locale": "fr_CA",
                        "profile": "https://phantauth.net/user/kayden.abbott/profile",
                        "nickname": "Kayden",
                        "preferred_username": "kabbott",
                        "picture": "https://www.gravatar.com/avatar/0e72d45f96c44213f80f10b593ccba13?s=256&d=https://avatars.phantauth.net/ai/unknown/X7axLPay.jpg",
                        "sub": "kayden.abbott",
                        "website": "https://phantauth.net",
                        "email": "kayden.abbott.6VBRMHI@mailinator.com",
                        "email_verified": true,
                        "gender": "unknown",
                        "birthdate": "2016-02-28",
                        "zoneinfo": "Canada/Central",
                        "phone_number": "988-622-6683",
                        "phone_number_verified": false,
                        "updated_at": 1519776000,
                        "me": "https://phantauth.net/~kayden.abbott",
                        "password": "RUEJG2Vj",
                        "webmail": "https://www.mailinator.com/v3/?zone=public&query=kayden.abbott.6VBRMHI",
                        "uid": "VHNoCwU/+LE",
                        "family_name": "Abbott",
                        "given_name": "Kayden",
                        "address": {
                            "street_address": "110 Aster Court APT 299",
                            "formatted": "110 Aster Court APT 299\nMiami 16321",
                            "locality": "Miami",
                            "postal_code": "16321",
                            "country": "Canada"
                        },
                        "name": "Kayden Abbott",
                        "@id": "https://phantauth.net/user/kayden.abbott"
                    }
                ]
            }

## Fleet [/fleet]

### Get a Fleet [GET /fleet/{fleetname}]

Ezen végpont használatával client-ek egy csoportja generálható véletlenszerűen. A generálás a path paraméterként megadott fleet név alapján történik, determinisztikus módon. Ugyanazon fleet név esetén a végpont ugyanazt a fleet objektumot generálja. A generált fleet objektum member client-jei és fleet property-ei a fleet név alapján véletlenszerűen generálódnak.
A fleet név elhagyása esetén minden hívás különböző, véletlenszerűen generált fleet névhez tartozó fleet objektumot generál.

+ Parameters
   + fleetname (optional, string) ... fleetname or email

+ Response 200 (application/json)

    + Attributes (Fleet)

    + Body
  
            {
                "profile": "https://phantauth.net/fleet/blue.fleet/profile",
                "sub": "blue.fleet",
                "logo": "https://www.gravatar.com/avatar/60757eca81bdd6768421ed3b669b651d?s=256&d=identicon",
                "logo_email": "blue.fleet.6JBLL7Y@mailinator.com",
                "name": "Blue Fleet",
                "@id": "https://phantauth.net/fleet/blue.fleet",
                "members": [
                    {
                        "logo_email": "zamit.6UTF3FA@mailinator.com",
                        "client_id": "zamit~ueyonuvxhz0",
                        "client_secret": "o0Ie0Ph4",
                        "client_name": "Zamit",
                        "client_uri": "https://phantauth.net/client/zamit%7Eueyonuvxhz0/profile",
                        "logo_uri": "https://www.gravatar.com/avatar/849f9934a6aec97935cb40eadbf06d60?s=256&d=https%3A%2F%2Favatars.phantauth.net%2Ficon%2Fpnelv7bK.png",
                        "tos_uri": "https://phantauth.net/client/zamit%7Eueyonuvxhz0/tos",
                        "policy_uri": "https://phantauth.net/client/zamit%7Eueyonuvxhz0/policy",
                        "software_id": "tzpm4afosVpE65jyw55ZLA",
                        "software_version": "8.0.8",
                        "@id": "https://phantauth.net/client/zamit%7Eueyonuvxhz0"
                    },
                    {
                        "logo_email": "otcom.DVC7D4Y@mailinator.com",
                        "client_id": "otcom~kzwnwi3dcjc",
                        "client_secret": "W0UFeZTo",
                        "client_name": "Otcom",
                        "client_uri": "https://phantauth.net/client/otcom%7Ekzwnwi3dcjc/profile",
                        "logo_uri": "https://www.gravatar.com/avatar/102ea74126cec525eded6e2511ee4960?s=256&d=https%3A%2F%2Favatars.phantauth.net%2Ficon%2FQBeXrkby.png",
                        "tos_uri": "https://phantauth.net/client/otcom%7Ekzwnwi3dcjc/tos",
                        "software_id": "RqrMOl5ZNZeEoYNkCdg1AA",
                        "policy_uri": "https://phantauth.net/client/otcom%7Ekzwnwi3dcjc/policy",
                        "software_version": "8.0.9",
                        "@id": "https://phantauth.net/client/otcom%7Ekzwnwi3dcjc"
                    },
                    {
                        "logo_email": "greenlam.2XD4DYQ@mailinator.com",
                        "client_id": "greenlam~o3sbolv1qjc",
                        "client_secret": "jeXBkxJ4",
                        "client_name": "Greenlam",
                        "client_uri": "https://phantauth.net/client/greenlam%7Eo3sbolv1qjc/profile",
                        "logo_uri": "https://www.gravatar.com/avatar/0d304aa152b8edd056d1e7862364dec2?s=256&d=https%3A%2F%2Favatars.phantauth.net%2Ficon%2FLDdwLJe1.png",
                        "tos_uri": "https://phantauth.net/client/greenlam%7Eo3sbolv1qjc/tos",
                        "policy_uri": "https://phantauth.net/client/greenlam%7Eo3sbolv1qjc/policy",
                        "software_id": "0dQ9wd0fb1v2RPd1de-m6A",
                        "software_version": "6.4.2",
                        "@id": "https://phantauth.net/client/greenlam%7Eo3sbolv1qjc"
                    },
                    {
                        "logo_email": "holdlamis.4AP3BGI@mailinator.com",
                        "client_id": "holdlamis~1jvzg8zw3ie",
                        "client_secret": "N0dEVTVQ",
                        "client_name": "Holdlamis",
                        "client_uri": "https://phantauth.net/client/holdlamis%7E1jvzg8zw3ie/profile",
                        "logo_uri": "https://www.gravatar.com/avatar/14d66b1256d484d2ab268cbe58694bb9?s=256&d=https%3A%2F%2Favatars.phantauth.net%2Ficon%2FRb4x6nbB.png",
                        "tos_uri": "https://phantauth.net/client/holdlamis%7E1jvzg8zw3ie/tos",
                        "policy_uri": "https://phantauth.net/client/holdlamis%7E1jvzg8zw3ie/policy",
                        "software_id": "ReiInzn-af_1XjFhBwl2Kw",
                        "software_version": "9.0.5",
                        "@id": "https://phantauth.net/client/holdlamis%7E1jvzg8zw3ie"
                    },
                    {
                        "logo_email": "asoka.K2ZLAYQ@mailinator.com",
                        "client_id": "asoka~vu9rsfdq16m",
                        "client_secret": "92Qz6rSU",
                        "client_name": "Asoka",
                        "client_uri": "https://phantauth.net/client/asoka%7Evu9rsfdq16m/profile",
                        "logo_uri": "https://www.gravatar.com/avatar/7acc74527505772449417aed086c3b24?s=256&d=https%3A%2F%2Favatars.phantauth.net%2Ficon%2F6dBB3xd7.png",
                        "tos_uri": "https://phantauth.net/client/asoka%7Evu9rsfdq16m/tos",
                        "policy_uri": "https://phantauth.net/client/asoka%7Evu9rsfdq16m/policy",
                        "software_id": "s0GXgtm6HqPy0nayXt8g4w",
                        "software_version": "3.9.6",
                        "@id": "https://phantauth.net/client/asoka%7Evu9rsfdq16m"
                    }
                ]
            }

## Tenant [/tenant]

### Get a Tenant [GET /tenant/{tenantname}]

Ezen végpont segítségével egy adott PhantAuth tenant adatai kérdezhetők le. A PhantAuth szolgáltatások igénybevételéhez nincs szükség ezen végpont használatára.
Elsősorban tehát debug/diagnosztikai céllal használatos tenant customizáció során.

A tenantname a lekérdezni kívánt tenant teljes DNS domain neve. Official és shared tenant-ok esetén (phantauth.net és phantauth.cf DNS domain) a DNS domain elhagyható (pl *default* vagy *faker*).

+ Parameters
   + tenantname (required, string) ... tenantname

+ Response 200 (application/json)

    + Attributes (Tenant)
    
    + Body
    
            {
                "sub": "faker",
                "issuer": "https://phantauth.net/_faker",
                "subtenant": false,
                "domain": false,
                "flags": "small",
                "logo": "https://phantauth-faker.now.sh/faker-logo.svg",
                "theme": "https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/united/bootstrap.min.css",
                "template": "https://default.phantauth.net{/resource}",
                "factories": [
                    "team",
                    "user"
                ],
                "website": "https://phantauth.net/_faker",
                "name": "PhantAuth Faker",
                "factory": "https://faker.phantauth.net/api{/kind,name}",
                "@id": "https://phantauth.net/_faker/tenant/faker"
            }

## Domain [/domain]

### Get a Domain [GET /domain/{domainname}]

Ezen végpont segítségével egy adott PhantAuth domain adatai kérdezhetők le. A PhantAuth szolgáltatások igénybevételéhez nincs szükség ezen végpont használatára.
Elsősorban tehát debug/diagnosztikai céllal használatos tenant customizáció során.

A domainname a lekérdezni kívánt domain teljes DNS domain neve (pl *phantauth.net* vagy *phantauth.cf*).

+ Parameters
   + domainname (required, string) ... domainname

+ Response 200 (application/json)

    + Attributes (Domain)

    + Body
    
            {
                "profile": "https://phantauth.net/domain/phantauth.net/profile",
                "sub": "phantauth.net",
                "logo": "https://www.phantauth.net/logo/phantauth-logo.svg",
                "name": "PhantAuth Domain",
                "@id": "https://phantauth.net/domain/phantauth.net",
                "members": [
                    {
                        "issuer": "https://phantauth.net",
                        "sub": "default",
                        "subtenant": false,
                        "domain": false,
                        "logo": "https://default.phantauth.net/logo/phantauth-logo-light.svg",
                        "favicon": "https://default.phantauth.net/logo/phantauth-favicon.png",
                        "template": "https://default.phantauth.net{/resource}",
                        "website": "https://phantauth.net",
                        "name": "PhantAuth Default",
                        "@id": "https://phantauth.net/tenant/default"
                    },
                    {
                        "issuer": "https://phantauth.net/_gods",
                        "sub": "gods",
                        "subtenant": false,
                        "domain": false,
                        "depot": "https://docs.google.com/spreadsheets/d/1Xa4mRcLWroJr2vUDhrJXGBcobYmpS8fNZxFpXw-M9DY/gviz/tq?tqx=out:csv",
                        "depots": [
                            "user",
                            "team"
                        ],
                        "flags": "medium",
                        "logo": "https://cdn.staticaly.com/favicons/www.theoi.com",
                        "favicon": "https://default.phantauth.net/logo/phantauth-favicon.png",
                        "theme": "https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/sandstone/bootstrap.min.css",
                        "attribution": "God pictures come from  [Theoi Project](https://www.theoi.com/), a site exploring Greek mythology and the gods in classical literature and art.",
                        "template": "https://default.phantauth.net{/resource}",
                        "website": "https://phantauth.net/_gods",
                        "name": "Greek Gods",
                        "@id": "https://phantauth.net/_gods/tenant/gods"
                    },
                    {
                        "issuer": "https://phantauth.net/_casual",
                        "sub": "casual",
                        "subtenant": false,
                        "domain": false,
                        "logo": "https://www.phantauth.net/logo/phantauth-logo-gray.svg",
                        "favicon": "https://default.phantauth.net/logo/phantauth-favicon.png",
                        "theme": "https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css",
                        "template": "https://default.phantauth.net{/resource}",
                        "factories": [
                            "user"
                        ],
                        "website": "https://phantauth.net/_casual",
                        "name": "PhantAuth Casual",
                        "factory": "https://wt-51217f7b3eee6aead0123eeafe3b83e8-0.sandbox.auth0-extend.com/user{?name}",
                        "@id": "https://phantauth.net/_casual/tenant/casual"
                    },
                    {
                        "issuer": "https://phantauth.net/_faker",
                        "sub": "faker",
                        "subtenant": false,
                        "domain": false,
                        "flags": "small",
                        "logo": "https://phantauth-faker.now.sh/faker-logo.svg",
                        "favicon": "https://default.phantauth.net/logo/phantauth-favicon.png",
                        "theme": "https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/united/bootstrap.min.css",
                        "template": "https://default.phantauth.net{/resource}",
                        "factories": [
                            "team",
                            "user"
                        ],
                        "website": "https://phantauth.net/_faker",
                        "name": "PhantAuth Faker",
                        "factory": "https://faker.phantauth.net/api{/kind,name}",
                        "@id": "https://phantauth.net/_faker/tenant/faker"
                    },
                    {
                        "issuer": "https://phantauth.net/_uinames",
                        "sub": "uinames",
                        "subtenant": false,
                        "domain": false,
                        "flags": "small",
                        "logo": "https://uinames.com/assets/img/ios-precomposed.png",
                        "favicon": "https://default.phantauth.net/logo/phantauth-favicon.png",
                        "theme": "https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/minty/bootstrap.min.css",
                        "attribution": "User data generated using [uinames.com API](https://uinames.com).",
                        "template": "https://default.phantauth.net{/resource}",
                        "website": "https://phantauth.net/_uinames",
                        "name": "uinames",
                        "@id": "https://phantauth.net/_uinames/tenant/uinames",
                        "script": "https://www.phantauth.net/selfie/uinames.js"
                    },
                    {
                        "issuer": "https://phantauth.net/_chance",
                        "sub": "chance",
                        "subtenant": false,
                        "domain": false,
                        "flags": "small",
                        "logo": "https://phantauth-chance.now.sh/chance-logo.png",
                        "favicon": "https://default.phantauth.net/logo/phantauth-favicon.png",
                        "theme": "https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/united/bootstrap.min.css",
                        "template": "https://default.phantauth.net{/resource}",
                        "factories": [
                            "user",
                            "team"
                        ],
                        "website": "https://phantauth.net/_chance",
                        "name": "PhantAuth Chance",
                        "factory": "https://chance.phantauth.net/api{/kind,name}",
                        "@id": "https://phantauth.net/_chance/tenant/chance"
                    },
                    {
                        "issuer": "https://phantauth.net/_sketch",
                        "sub": "sketch",
                        "subtenant": false,
                        "domain": false,
                        "flags": "sketch;small",
                        "logo": "https://www.phantauth.net/logo/phantauth-sketch.svg",
                        "favicon": "https://default.phantauth.net/logo/phantauth-favicon.png",
                        "theme": "https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/sketchy/bootstrap.min.css",
                        "template": "https://default.phantauth.net{/resource}",
                        "website": "https://phantauth.net/_sketch",
                        "name": "PhantAuth Sketch",
                        "@id": "https://phantauth.net/_sketch/tenant/sketch"
                    },
                    {
                        "issuer": "https://phantauth.net/_randomuser",
                        "sub": "randomuser",
                        "subtenant": false,
                        "domain": false,
                        "flags": "small",
                        "logo": "https://cdn.staticaly.com/favicons/randomuser.me",
                        "favicon": "https://default.phantauth.net/logo/phantauth-favicon.png",
                        "theme": "https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/sandstone/bootstrap.min.css",
                        "attribution": "User data generated using [RANDOM USER GENERATOR](https://randomuser.me/).",
                        "template": "https://default.phantauth.net{/resource}",
                        "website": "https://phantauth.net/_randomuser",
                        "name": "RANDOM USER",
                        "@id": "https://phantauth.net/_randomuser/tenant/randomuser",
                        "script": "https://www.phantauth.net/selfie/randomuser.js"
                    },
                    {
                        "issuer": "https://phantauth.net/_mockaroo",
                        "sub": "mockaroo",
                        "subtenant": false,
                        "domain": false,
                        "flags": "small",
                        "logo": "https://www.phantauth.net/selfie/kongaroo.svg",
                        "favicon": "https://default.phantauth.net/logo/phantauth-favicon.png",
                        "theme": "https://stackpath.bootstrapcdn.com/bootswatch/4.2.1/minty/bootstrap.min.css",
                        "attribution": "User data generated using [Mockaroo's Mock APIs](https://mockaroo.com/mock_apis).",
                        "template": "https://default.phantauth.net{/resource}",
                        "website": "https://phantauth.net/_mockaroo",
                        "name": "Mockaroo",
                        "@id": "https://phantauth.net/_mockaroo/tenant/mockaroo",
                        "script": "https://www.phantauth.net/selfie/mockaroo.js"
                    },
                    {
                        "issuer": "https://mockuser.ga",
                        "sub": "mockuser.ga",
                        "subtenant": false,
                        "domain": false,
                        "logo": "https://www.phantauth.net/brand/mockuser/mockuser-logo-light.svg",
                        "favicon": "https://www.phantauth.net/brand/mockuser/mockuser-favicon.png",
                        "theme": "https://www.phantauth.net/brand/mockuser/bootstrap-mockuser.min.css",
                        "template": "https://default.phantauth.net{/resource}",
                        "website": "https://www.mockuser.ga",
                        "name": "Mock User",
                        "@id": "https://mockuser.ga/tenant/mockuser.ga"
                    }
                ]
            }    

# Data Structures

## User (object)

+ sub (required, string)
  Subject - Identifier for the User at the Issuer.
  
+ name (optional, string)
  User's full name in displayable form including all name parts, possibly including titles and suffixes, ordered according to the End-User's locale and preferences.

+ address (optional, Address)
  User's preferred postal address.

+ given_name (optional, string)
  Given name(s) or first name(s) of the User.

+ family_name (optional, string)
  Surname(s) or last name(s) of the User.

+ middle_name (optional, string)
  Middle name(s) of the User.

+ nickname (optional, string)
  Casual name of the User that may or may not be the same as the given_name.

+ preferred_username (optional, string)
  Shorthand name by which the User wishes to be referred to at the Relying Party.

+ profile (optional, string)
  URL of the User's profile page.

+ picture (optional, string)
  URL of the User's profile picture.
  
+ website (optional, string)
  URL of the User's Web page or blog.

+ email (optional, string)
  User's preferred e-mail address.

+ email_verified (optional, boolean)
  True if the User's e-mail address has been verified; otherwise false.

+ gender (optional, string)
  End-User's gender. Possible values are female and male and unknown.

+ birthdate (optional, string)
  User's birthday, represented as an ISO 8601:2004 [ISO8601‑2004] YYYY-MM-DD format.

+ zoneinfo (optional, string)
  String from zoneinfo time zone database representing the User's time zone. For example, Europe/Paris or America/Los_Angeles.

+ locale (optional, string)
  User's locale, represented as a BCP47 [RFC5646] language tag. This is an ISO 639-1 Alpha-2 language code in lowercase and an ISO 3166-1 Alpha-2 country code in uppercase, separated by a dash.

+ phone_number (optional, string)
  User's preferred telephone number.

+ phone_number_verified (optional, boolean)
  True if the End-User's phone number has been verified; otherwise false.

+ updated_at (optional, number)
  Time the User's information was last updated. Its value is a JSON number representing the number of seconds from 1970-01-01T0:0:0Z as measured in UTC until the date/time.

+ me (optional, string)
  Simplified URL of the User's profile page.
  
+ password (optional, string)
  User's generated password.

+ uid (optional, string)
  Simplified, shortened identifier for the User at the Issuer.
  
+ webmail (optional, string)
  URL of User's mailbox in a web mail application. 

+ @id (optional, string)
  URL of the User's JSON representation.

## Address (object)

+ formatted (optional, string)
  Full mailing address, formatted for display or use on a mailing label. This field MAY contain multiple lines, separated by newlines. Newlines can be represented either as a carriage return/line feed pair or as a single line feed character.

+ street_address (optional, string)
  Full street address component, which MAY include house number, street name, Post Office Box, and multi-line extended street address information. This field MAY contain multiple lines, separated by newlines. Newlines can be represented either as a carriage return/line feed pair or as a single line feed character.

+ locality (optional, string)
  City or locality component.

+ region (optional, string)
  State, province, prefecture, or region component.

+ postal_code (optional, string)
  Zip code or postal code component.

+ country (optional, string)
  Country name component.

## Client (object)

+ client_id (required, string)
  OAuth 2.0 client identifier string.
  
+ client_secret (optional, string)
  OAuth 2.0 client secret string. 
  
+ redirect_uris (optional, array[string])
  Array of redirection URI strings for use in redirect-based flows such as the authorization code and implicit flows.

+ token_endpoint_auth_method  (optional, string)
  String indicator of the requested authentication method for the token endpoint.

+ grant_types (optional, array[string])
  Array of OAuth 2.0 grant type strings that the client can use at the token endpoint.

+ response_types (optional, array[string])
  Array of the OAuth 2.0 response type strings that the client can use at the authorization endpoint.
  
+ client_name (optional, string)
  Human-readable string name of the client to be presented to the end-user during authorization.

+ client_uri (optional, string)
  URL string of a web page providing information about the client.
  
+ logo_uri (optional, string)
  URL string that references a logo for the client.

+ scope (optional, string)
  String containing a space-separated list of scope values (as described in Section 3.3 of OAuth 2.0 [RFC6749]) that the client can use when requesting access tokens.

+ contacts (optional, array[string])
  Array of strings representing ways to contact people responsible for this client, typically email addresses.
  
+ tos_uri (optional, string)
  URL string that points to a human-readable terms of service document for the client that describes a contractual relationship between the end-user and the client that the end-user accepts when authorizing the client.
  
+ policy_uri (optional, string)
  URL string that points to a human-readable privacy policy document that describes how the deployment organization collects, uses, retains, and discloses personal data.

+ jwks_uri (optional, string)
  URL string referencing the client's JSON Web Key (JWK) Set [RFC7517] document, which contains the client's public keys.
  
+ jwks (optional, array[string])
  Client's JSON Web Key Set [RFC7517] document value, which contains the client's public keys.  The value of this field MUST be a JSON object containing a valid JWK Set.
  
+ software_id (optional, string)
  A unique identifier string (e.g., a Universally Unique Identifier (UUID)) assigned by the client developer or software publisher used by registration endpoints to identify the client software to be dynamically registered.
  
+ software_version (optional, string)
  A version identifier string for the client software identified by software_id.

+ @id (optional, string)
  URL of the Client's JSON representation.

+ logo_email (optional, string)
  A gravatar.com logo_uri generáláshoz használatos email cím.

## Team (object)

+ sub (string) - subject
+ name (string) - name
+ members (optional, array[User])


## Fleet (object)

+ sub (string) - subject
+ name (string) - name
+ members (optional, array[Client])

## Tenant (object)

+ sub (required, string)

+ issuer

+ website

+ template

+ factory

+ factories

+ depot

+ depots

+ userinfo

+ id

+ name

+ logo

+ favicon

+ theme

+ script

+ sheet

+ summary

+ attribution

+ about

+ domain (optional, boolean)

+ subtenant (optional, boolean)



## Domain (object)

+ sub (string) - subject
+ name (string) - name
+ tenants (optional, array[Tenant])
