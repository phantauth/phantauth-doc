FORMAT: 1A
HOST: https://phantauth.net/

# PhantAuth

Random User Generator + OpenID Connect Provider. Like Lorem Ipsum, but for user accounts and authentication.

## User [/user]

### Get a User [GET /user/{username}]

Get

+ Parameters
   + username (optional, string) ... username or email

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

Create self contained token (selfie token) from user registration data.

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

Get a user token.

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

Get

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

Create self contained token (selfie token) from client registration data.

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

Get a client token.

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

Get

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

Get

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
                        "policy_uri": "https://phantauth.net/client/otcom%7Ekzwnwi3dcjc/policy",
                        "software_id": "RqrMOl5ZNZeEoYNkCdg1AA",
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

Get

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

Get

+ Parameters
   + domainname (required, string) ... domainname

+ Response 200 (application/json)

    + Attributes (Domain)

# Data Structures

## User (object)

+ sub (string) - valami
+ name (string) - name

## Client (object)

+ client_id (string) - valami
+ name (string) - name

## Team (object)

+ sub (string) - valami
+ name (string) - name

## Fleet (object)

+ sub (string) - valami
+ name (string) - name

## Tenant (object)

+ sub (string) - valami
+ name (string) - name

## Domain (object)

+ sub (string) - valami
+ name (string) - name
