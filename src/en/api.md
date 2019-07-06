FORMAT: 1A
HOST: https://phantauth.net/

# PhantAuth

Random User Generator + OpenID Connect Provider. Like Lorem Ipsum, but for user accounts and authentication.

The PhantAuth API documentation is available on the following API documentation sites:

- [apiary](https://phantauth.docs.apiary.io) (primary source)
- [speca](https://speca.io/phantauth/phantauth)
- [PhantAuth Developer Portal](https://www.phantauth.net/api)

### TL;DR

**PhantAuth was designed to simplify testing for applications using OpenID Connect authentication by making use of random generated users.**

endpoint  | address
--------- | -------
issuer    | https://phantauth.net
discovery | https://phantauth.net/.well-known/openid-configuration

credential    | value
------------- | -----
client_id     | test.client
client_secret | UTBcWwt5

## OpenID Connect

The OpenID Connect Provider of PhantAuth supports the flows listed in the OpenID Connect specifications (Hybrid, Implicit, Authorization Code), as well as the Resource Owner Password grant type, specified in the OAuth 2.0 specifications. PhantAuth as an OpenID Connect Provider can be integrated with a variety of web applications, mobil applications, and  backend applications. The integration can be either direct, as in the case of the OpenID Connect Provider, or through an authentication integration service, as in the case of Auth0 or Azure Active Directory B2C. To learn more, please go to chapter [Integration](https://doc.phantauth.net/#/integration).

Examples:

- [Direct OpenID Connect integration](https://www.phantauth.net/test/oidc)
- [Auth0 Social Connections integration](https://www.phantauth.net/test/auth0)
- [Azure Active Directory B2C integration](https://www.phantauth.net/test/azure)

## Random User

The random user generator of PhantAuth can also be used separately, independent of the OpenID Connect Provider. You can generate an optional number of test users. In the knowledge of their user name, the data of the generated users can be regenerated at any time (OpenID Connect *sub* claim). The generated users have a unique, operational, disposable email address, a profile picture selected from one of the multiple pools of pictures, and the usual profile data. Custom email addresses and profile pictures may also be added. The random user generator of PhantAuth can be fully customized. Additionally, you can link an external generator to the application. For details,please go to chapter [Generator](https://doc.phantauth.net/#/generator).

Test pages:

- [Default Generator Test Page](https://phantauth.net/test/user) (embedded generator)
- [Greek Gods Generator Test Page](https://phantauth.net/_gods/test/user) (embedded generator working from a Google Sheet)
- [Faker Generator Test Page](https://phantauth.net/_faker/test/user) (external generator using Javascript Faker library)
- [Chance Generator Test Page](https://phantauth.net/_chance/test/user) (external generator using Javascript Chance library)
- [Casual Generator Test Page](https://phantauth.net/_casual/test/user) (external generator using Javascript Casual library)
- [Randomuser Generator Test Page](https://phantauth.net/_randomuser/test/user) (client side generator using https://randomuser.me)
- [uinames Generator Test Page](https://phantauth.net/_uinames/test/user) (client side generator using https://uinames.com)
- [Mockaroo Generator Test Page](https://phantauth.net/_mockaroo/test/user) (client side generator using https://mockaroo.com)

Every random generated user has a profile page, which contains their profile data in a simple one-page format.

Profile examples:

- [Random Profile](https://phantauth.net/%7Ejoe.black)
- [Random Greek God Profile](https://phantauth.net/_gods/%7Ezeus)
- [Random Faker Profile](https://phantauth.net/_faker/%7Eharry.houdini)
- [Random Chance Profile](https://phantauth.net/_chance/%7Epeter.pan)
- [Random Casual Profile](https://phantauth.net/_casual/%7Ejohn.smith)

## CodeSandbox

The use of the random user generator and the direct integration of  the OpenID Connect is demonstrated through a set of CodeSandbox samples. The sample applications are run directly from CodeSandbox, so the source code is easy to view, edit, and test.

Examples:

- [Random User Generator usage exampe](https://4xyj8lw394.codesandbox.io/)
- [OpenID Connect direct integration exampe](https://8z77681269.codesandbox.io/)

## Tenants

The PhantAuth is extremely versatile and customizable. You can use your own random user service, or generate users from an external .csv file or Google Sheet. You can use a set of Bootstrap themes to tailor the look and feel of the profile, morover, you can fundamentally change the same look and feel by the use of your own HTML templates. To find out more, please go to chapter [Tenant](https://doc.phantauth.net/#/tenant).

To customize the application, you need to use one or more so-called tenants. A tenant can be consiered as an independent PhantAuth service. A tenant has its own random user generator endpoints and OpenID Connect endpoints.

The tenants can be organised into so-called domains. Practically, a domain is a DNS zone, which contains the settings of the given tenant(s). The tenants as well as the domain can be configured by the use of DNS TXT records.

In addition to the default tenant, the PhantAuth Domain contains some sample tenants, which are primarily designed to demonstrate customitability, a range of hosting possibilities, and the links to external services. In most cases, using the [default tenant](https://phantauth.net) is enough.

- [PhantAuth Default](https://phantauth.net) - default tenant, based on a Java Fairy library
- [Greek Gods](https://phantauth.net/_gods) - based on a Google Sheet document
- [PhantAuth Faker](https://phantauth.net/_faker) - based on a Javascript Faker library, hosted at https://now.sh
- [PhantAuth Chance](https://phantauth.net/_chance) - based on a Javascript Chance library, hosted at https://now.sh
- [PhantAuth Casual](https://phantauth.net/_casual) - based on a Javascript Casual library, hosted at https://webtask.io
- [RANDOM USER](https://phantauth.net/_randomuser) - based on https://randomuser.me service
- [uinames](https://phantauth.net/_uinames) - based on https://uinames.com service
- [Mockaroo](https://phantauth.net/_mockaroo) - based on  https://mockaroo.com service

Anyone can create a domain and the tenants. Sharing the tenants is facilitated by the [PhantAuth Shared Domain](https://shared.phantauth.net). A shared domain is connected to the [phantauth.cf](http://phantauth.cf) DNS zone, where anyone can create tenant configuration notes by the use of the [FreeDNS](https://freedns.afraid.org/) service.

## Pricing

PhantAuth is a free, open-source, non-profit application. If you find this service useful and can afford, please make a small donation as a contribution to the operation costs (domain registration, service hosting, etc.)

[Donate on Ko-fi](https://ko-fi.com/Q5Q0T7C7) | [Donate on Liberapay](https://liberapay.com/szkiba/donate) | [Donate on PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=VXLCJ3EZRAE7G&source=url)

## Generator

The basic concept of PhantAuth is that it generates data in a random but deterministic way. To achieve this goal, a so-called pseudorandom number generator (PRNG) is used. Each object type has an identifier (login name for user, client_id for client, etc.) By using a given hash algorithm, the value of the pseudorandom generator seed is produced from this identifier. Then, every property of the given object is generated with the pseudorandom generator started from this seed value. Taking advantage of the special feature of the pseudorandom number generator, also called as deterministic random bit generator (DRBG), that is, it generates the same random value series started from the same seed, the identifier clearly defines the object generated from it. That is, by the use of an identifier and generator, you can regenarate the properties of a given object at any time.

Based on the above concept, PhantAuth is absolutely stateless, and no storage medium is necessary. So, a randomly selected login name will "exist", and the properties of the "associated" user can be generated.

### Identifier

In brief, an object is defined by its identifier. The name of the identifier of a user or client object is `sub` or `client_id` used in the OpenID Connect specifications. The name of the identifier property of other PhantAuth-specific objects that are not included in the specifications is `sub`.

The identifier may contain any character.

### Customization

Sometimes you may want to customize the properties generated from the identifier. Although the identifier may contain any character, and its structure is optional, you can customize the generated values if a certain structure is used.

#### Flags

You can use a variety of flags to customize or give the parameters of certain object properties (user, client, etc.). The flags can be grouped by their effect on the generation of the properties. Basically, a flag is a keyword. You can set more than one flags to affect the generation of a variety of properties at the same time. To separate the flags from one another and the rest of the identifier, you need to use a semicolon `;`:

```
joe;female;kitten
```

In the above example, the user generated by the user generator is female, and her avatar is a randomly selected sketched kitten avatar. The other features are deterministically generated from the name "joe", that is, their values are not affected by the two flags. The [profile page](https://phantauth.net/%7Ejoe%3bfemale%3bkitten) of this example can be found [here](https://phantauth.net/%7Ejoe%3bfemale%3bkitten).

Please note that the flags form part of the identifier, as a different flag allows you to generate a different object.

##### User gender flags

The following flags modify the gender of the generated user.

Flag | Description
--- | ---
male | The `gender` property of the generated user is male, independent of the user's name
female | The `gender` property of the generated user is female, independent of the user's name
guess | The `gender` property is defined on the basis of the generated user's given name (default)
nogender | The generated user doesn't have a `gender` property

##### User avatar flags

The following flags modify the generated avatar image.

Avatar | Flag | Description
--- | --- | ---
![](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAQCAwMDAgQDAwMEBAQEBQkGBQUFBQsICAYJDQsNDQ0LDAwOEBQRDg8TDwwMEhgSExUWFxcXDhEZGxkWGhQWFxb/2wBDAQQEBAUFBQoGBgoWDwwPFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhb/wgARCAAgACADAREAAhEBAxEB/8QAGAAAAwEBAAAAAAAAAAAAAAAABQcIBgT/xAAZAQACAwEAAAAAAAAAAAAAAAACBQEDBAb/2gAMAwEAAhADEAAAAC6Xe29GzHjM+gFAVhqJajyCeLlrIXbWPewzZijGPPvG/NwoetBt08tMkn//xAAqEAABBAEDAwMDBQAAAAAAAAABAgMEBREABhIHITETIkEIFWEjMlFxof/aAAgBAQABPwDoBVvmxe3DuSZCnJjKxAaaaBSlwYJcJz8ZSB+VDVjQ3Ni+L+ukOh9LRaS1IkFCSknvhKchJyB/IOB21vOduKNt+TC3LspNpVvHhKWC26koPYqcb4+5I+SSSPOrjpbVN2D1bt+ImJEkMpDjshCXHsqySGjjKRxKR7jnIOuhUaMxtlguVqY7rbi2kxArJCXMcV4wAByB8Z8E6n9TaSv3Wjbv2+zmPuKS0XWWx6SV+AknlkHP41Y9SqSbuqZtX7baR5rZWxzdY/RWvuCnkVd/6A8d9b86uWjd1Pq9gbUfdlR3lx3LFTBOVpUQotj9oTnwfONdEdwsU0lFHcwr+NYT3S5BVYyUSBz9MFaUnlyCQhkrHYgYWdXG762DdoW/ErgtlHMvynkMKkZ8IZUrty+T+AE5Gci26m1CGLO+broZQ0y9JcLcptx2MpIK1IdKSQOXwO5GoHVSss7kzbWqkyovqKWquE/0m3CpWTlSEBXgkY/0+Da9L7fY/wBUNYuXbxp1TupiwjUCe6HIkhtv1g0sEcQVMtuoCwdX93XVT8ytvYMkpT7WltoQpaUgkcClYOCDkeDqvsdoXcKTAuSKiisIsiqYfslAqlzZDZaQhtKQSSjklftHtJSdVzEqC7IiTWiw/FcWy6kkHgtJwpJI7ZBBGc41/8QAJREAAgIABQIHAAAAAAAAAAAAAQIAEQMEEjFBIVEFEyIycYHB/9oACAECAQE/AMsFY6wKqM/WxDiudhNbXqPEyTgYTKxsi4XrrvFY77QgM2omhMNhiMShBrtMJgxvtPc6qOYnhgVvU9/VfsbKocu2FhKF+O8S1NHoZkcvqfzX42nM/8QAIhEAAgICAgICAwAAAAAAAAAAAQIAEQMhBDESIhNBBTJx/9oACAEDAQE/ALLHcXB600PEXxu4cSeOonFyL4mtE9/yLjJNHUyLQI7FQkra9kTj8la+I/e9wJ61ZsxwqYmLH9RG5pK0q0Zg5ATMrt0DFfVg2J+W5nr8SffcB1P/2Q==) | ai | [AI](https://thispersondoesnotexist.com/) type generated, photo-like avatars (default)
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAABelBMVEX////uuIw6TFomLDQ4SljuuYovQ1Hvuo5KMSztuI4xRFIxQ1DsuY3storvuY3+///zvY8nLTLc4ePx17zvxqPzvpP2wZHvuYrVpnyjfVycdlw1SFcyRlWWc1QjN0YqOEMoLDVMMCxILipFKyb6/Pv9/vn3+Pju8vPu8PDo6+337d/Bxcets7eHkZn1wZXotYrutonsuYiViobQonj7///79+/28unx4M3y2cbx3MO3v8Ozq6nov5ruvpLktYvxuIfpt4bbqYCnlIDQo33MoHlxdXmEd3O+k3C5kGqlgGA7TVueeVltXFktP0p2VURrTD0qNDsmMTgoLjIfJS8iKC1DMyX9/vvl6evq6Of28OHb1djb1NjEycvGwr/Jwb+yub3Cu7nu0rjt0bi3sazfvp7evZzpvJPdtZN+ipPpvJKdko/uvIx1gYrisIVxfIXRonqJe3pWZXGCb2iuhWRDU1+dd11pV1SGZE6BYU4tQE5iT0pXQkFDLylBKSPfP9FbAAABsklEQVQ4y62SV1fCMBhAm5C0tLWlIFOGAoqAAgLuvfdW3Hvvvcd/NynnCJLy5n3p+XJv25y03D+zttOV+Zy+qC2jNz6+w6FgMGjeNPbb4aA5T3jPyNeGQm9VhOfHWXM4wnpL19erA1AqhNnQoYUt7uacIB9UOOcyHMv0GFE0EEU8NmoQvFyqjqQAgOBwqNdGwYNz3ONxY+z2eMadmWbGt/T2ZDUNEwQt23PawgSVLqBOTNFXTE2oAFcaBWBoGBCGh4BR0JGmsimVaqLXdAcT1O0rRCjZW4UGB+z3Wmmlt2rJpEaOKt1qYZ/AdfcB4M/l/AD0dZORJd4vioLfL4hif5wzpE0RscuFRaWNK0P8RAVAPV/nytF87B4YcB9ZynmbzU5P0m6zGdloAgXq7fR3sNcHUCJa6hu8kATtCsZKezSAIGr46zt9EPL8SGww1TsYG+F5CKXOYr9KPJSkhWXT0pJpeUGSyOiLFW32hiwgXppfrCEszks8IgtXBR+R9YCvtpoI1mr+PXGGoBwp3iFBKgS++ycIvVu/QSOigVeeMenMyPqMdkuCSVnWvVWWJ/WgkbofGhc3SydvBmYAAAAASUVORK5CYII=) | sketch | sketched photo-like [avataaars](https://getavataaars.com/) avatars
![](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAQDAwMDAgQDAwMEBAQFBgoGBgUFBgwICQcKDgwPDg4MDQ0PERYTDxAVEQ0NExoTFRcYGRkZDxIbHRsYHRYYGRj/2wBDAQQEBAYFBgsGBgsYEA0QGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBj/wgARCAAgACADAREAAhEBAxEB/8QAGAAAAwEBAAAAAAAAAAAAAAAABAcIBgP/xAAZAQEAAwEBAAAAAAAAAAAAAAAFAwQGAAH/2gAMAwEAAhADEAAAAKqCXmKa6P3Ur6dnoLS3qPAoU9InlVzAmWDq+q42gRzMJepNsBxZvCPWhP8A/8QALRAAAQQBAwMCAwkAAAAAAAAAAQIDBBEFAAYSByExE0EUFVEWIiMyQmFxkbH/2gAIAQEAAT8A+bIwOSlTA20iGpbzrzjaAXClKeXbt3rW8989V944c5+LGcfxU0r9CKy4GwGQriApI48/BNm71sHq71E2dPZjZfGvyMGshDsSSeaRyIFIJFJJ1Kw70zIJf2rFfeZUn8RvtTS+xKeRP0I89voT7TszHm4lczmlh1cFL7bJPZRWSKH8CzoTcpBlYrbLO3XlwxFQgzw4kJQoJF/cq6v31Ekqy3zLETNvS47ENbZTIk0W1lDyDYoX7WD5/bT+2mZ60oRkIhkFRWFsZN5pZUfJtKQfP11kus2zoKMWJ+OkyBFYZbRKQsUhSKBUgBXe/NEdxpzqTPlNujb8JhbuNQiPKTOfS1wVVd0+SCBYI1M6m42BDbi7i4QMpIPNccH1BxokKtN0OVV58HWG3jh1vw3JOIeeiLbDhkR5iSSon8vZsitSp7z7LranFEA3V/2f919stvbnxrOcTuc7czDjKGsi36XqJf4CgSixzr9JBujRB1ms+5kt2TJ6JcmQ2FhDbsmgtaU0ORA7C6Jr2urNXrozuCa9siZF+NcQwyQQk0QVEAEkHz4Tr//EACURAAICAQMCBwEAAAAAAAAAAAECAAMRBBIhMlEFExUiMUFxsf/aAAgBAgEBPwCtsEmeaith4GR+kxQzdIyJYhryByBLCQeJpF2glp6U46WENG4nJ+ZYWW7b9TSA2kl4umA9xPH7NvaHR2iwo67lzwe2ZVUKkCAYxPFw6otinAGf5xP/xAAgEQACAQUAAgMAAAAAAAAAAAABAgADBBESIQUxFSJx/9oACAEDAQE/AGTYCUbIlcr7lezKjMLhOMcGWxFZlU82MtlGvTL8FgFp+zifJUx7WCi66lTggyxVKqAM2DPIbp9KOCex3dTow7+Q1jgiU7ykUFVX1bHRHuGZ2cnMtwrkhhk8n//Z) | photo | photo avatars
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAASFBMVEX///AoHCf/4LXP1Yz////EzHL/3K3Tmob/5sRURUXWuppMNzoKBgnWz8Df0rhXhIg+NC0uIyrf5+jz9eTf2cr44sHZ15VMPj4HhT4EAAAAlElEQVQ4y72S2w6CMBBEpYhstRXx+v9/Ko4LS1sgmRfOQzPZOWnSy2FHqgxW8FVJ0vfT+Aw+Q/LL+zvgsy2sVW6BFFyvtRGCCRgcf7gskkJnQncvBZGriBvjSxJhlfSYNreLIoScTaFtOQF4rcDSl3lGzC4AMUb2T4ITQGSFdw2ax/COTf1n3ms9ogorQNGlFBI44QtzCgcBd0pFOQAAAABJRU5ErkJggg==) | dice | pixel art-style [DiceBear](https://github.com/DiceBear/avatars) avatars
![](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAQCAwMDAgQDAwMEBAQEBQkGBQUFBQsICAYJDQsNDQ0LDAwOEBQRDg8TDwwMEhgSExUWFxcXDhEZGxkWGhQWFxb/2wBDAQQEBAUFBQoGBgoWDwwPFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhb/wgARCAAgACADAREAAhEBAxEB/8QAGQAAAgMBAAAAAAAAAAAAAAAABAYDBQgH/8QAGwEAAgMAAwAAAAAAAAAAAAAABQYBAwQAAgf/2gAMAwEAAhADEAAAANaJeOCqOd+iDnkJur0WoZYGhWcmLanlnJDCsyquYXZ9NWmmUpTHqfadDPhj/8QAKhAAAgICAQMDAwQDAAAAAAAAAQIDBAUREgAGIQciMRMVQSNCUXEyUmH/2gAIAQEAAT8Az3cdmbvpoqlmdqsE8dOKGFggaYuY3ck6J0zlNbA2m/J11lO985i+9rmOatHchV2P0nKxmFdnhpvnRXRPtY+V8aPXcnrtnKdmCnat0KkwTlYjhgkeSJ0mMb71vanTsnjzwAIcHz6HeoWb7zyUMZ4S0oIXWWyYDE9kr+8qQvBgSgKga9zHWtazNRZ8pnpnhlcUpLVmIQ+11lW0oVw2wVADOSR5A2RsgDpObF5XkeWSV2klkk1ykdjssQAACT+AAB8AADXSxVIu5ESDEsbeQhkaS5DVGiIyihJZB52eY4qd7CN/r1grAjz1evjK9iI1L1YN9CLgk6mdecaP/idPHp1HkFdEeR01atW9V7ONvQI9TMVXVY2GwxcBzv8AsxTf9G16z3Y9jHRvPQngejChZhM4jaFAP51xIA/JK6A+D1QTKXpoExKvWtyv+k0yKVQ+dc15r4PwAGB2QD/B9P8AsrK0cn937lyy3bKbaKCCNUhjZiWL6ABJ2ToHlrQPJm2x9R8NYvUosljQfuOOb6kPEbLgENrX5IKhgD86K/uJ67m7myncMfAwT16qIA1KA8nsOB7ixHll3sKh0NeXGzpOxe4Z4IMPnM/WnipySWK9yNNgpKkwVCfOw6hGP9+NAkdROskYdGBVgCpHwQev/8QALhEAAQMCBAMGBwEAAAAAAAAAAQIDEQQhAAUxgRJBURMUYXGRoQYQIiMzscHR/9oACAECAQE/AH83WM1TSoEpsDHXn6C2KrPHqOodS4ApIVAGhiAdb9eY3wxldPVNU9U09DawCQdTIsARoZsbcjjM+NjOVUrY+3w8XOb6e8jxicNMTXVrhMFMwehJ12/WKh9x91TrhlRwFvushHaEpSRCZOpm6RtfzGMuVVU1c32hMrIBBmYkfvQHzw22lnOXUKH0uoncWP8ATiu+FlcRXTrEdFct/wDcUFK49VBtogqGhmPQx/MUOUlp7vFQeJYsNbbmPYAXNtIzOkcdQl1j8jZkePUb4zTO6irUKanBSDY9Z5jyGMqR3SrVKZTYT0tNt42+X//EACwRAAIBAwEFBgcAAAAAAAAAAAECAwAEIRESMUFR8AWBkbHB0RATFBUyQqH/2gAIAQMBAT8Ae5P1IiFS3RhJ1znTTuHGvus+pATrrNWF286ja3jf78s0iazTNxFSOzsWbfQUspIPLHHNWu3FKuv7eNKoW6bkw8qm7OJJKN4+9QRFpNlT/dPT0qK22W2239dbhU8ZcBl/Jcj276ubt5D8tMc6t0EUxxjHl8P/2Q==) | kitten | [ROBOHASH](https://robohash.org/)-generated sketched kitten avatars
![](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAcFBQYFBAcGBQYIBwcIChELCgkJChUPEAwRGBUaGRgVGBcbHichGx0lHRcYIi4iJSgpKywrGiAvMy8qMicqKyr/2wBDAQcICAoJChQLCxQqHBgcKioqKioqKioqKioqKioqKioqKioqKioqKioqKioqKioqKioqKioqKioqKioqKioqKir/wgARCAAgACADAREAAhEBAxEB/8QAGQAAAgMBAAAAAAAAAAAAAAAAAAUDBAYB/8QAGgEBAAMAAwAAAAAAAAAAAAAAAAIDBAEFBv/aAAwDAQACEAMQAAAAc9Z7oAAFM8lXmOgr25uzDMTxt5Ku5DQgtxWBpXr/AP/EACgQAAICAQMDBAEFAAAAAAAAAAECAwQRBRIhAAYxEBMiUQdBRXFzwv/aAAgBAQABPwD0BBzgg444Prc1F1p+7PQtiNZzkIoYlEG7ewPhcjwfOP1z1oGqi7BLLQRrETXNkkjZVtpiQiTHOcnB8+Gz6d394J2tQSdKZuu03tOqvsEZ2hvk2DgkHjqHvLQZHENm/WqzGNHMU0yHAZQw+QJU8H7/AJA6m7p0CooD6rTHgKkcgY/QAA603uGC/repaU0FivZoOqSrPGF5OfjkE/Lg8HB6s6VTutKbMCSrNGI5UcZSRQcjcp4JHOD5H31N+Ne1p/2wJ/VLIP8AR6bsPQZ5o5b0E99oo1ijNy1JJsReFQZbhQOAPA6qaJp9F4zSqpXSLJjiiG2NWIwX2jy2ONxyccdf/8QAHxEAAgIBBAMAAAAAAAAAAAAAAQIAAxEQITFBEhMg/9oACAECAQE/APlRgxxvvpWnmYamXqCtj1GrKDJgYjie54bnMLluZ//EACgRAAEEAQICCwAAAAAAAAAAAAECAwQRACExBUEQEhUgIlFhgZGhwf/aAAgBAwEBPwDuvLK26o1f0OeR12klOuv5v0SpYjpsCzdY1OYcTqqj66YqUwgWVjI8tD6ilPLFsocvrDfOzY/kfnE8NjjcE++Nx22z4BWf/9k=) | adorable | [Adorable Avatars](http://avatars.adorable.io/)
![](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAQCAwMDAgQDAwMEBAQEBQkGBQUFBQsICAYJDQsNDQ0LDAwOEBQRDg8TDwwMEhgSExUWFxcXDhEZGxkWGhQWFxb/2wBDAQQEBAUFBQoGBgoWDwwPFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhb/wgARCAAgACADAREAAhEBAxEB/8QAGgAAAgIDAAAAAAAAAAAAAAAAAAcBBAIGCP/EABQBAQAAAAAAAAAAAAAAAAAAAAD/2gAMAwEAAhADEAAAAOii6BSAb5InzIaoCqNqGQAtz//EACcQAAIBAwMCBgMAAAAAAAAAAAECAwQFEQAGQRKRBxAhMTJxE1HB/9oACAEBAAE/ANWe03G6OVoKV5un5N6BR9k4GrvaLlayBX0jxBvichlP0Rkeey4IYNrUKQABXgV2I5Zhlj3Ot4wQVG165JwCqwM4J4ZRkHuPKFHllWONCzuQqhRkkn2A1sS2XG12YQV06vn1SIDP4s+46udb4ttwudmanoKgJy8RGDLj1A6uP7+9So8UrxyIVdCVYMMEEe4OvCOgSpvc1ZIARSRjoB4ZsgHsG8/FqgSmvcVZGABVxnrA5ZcAnsV1/8QAFBEBAAAAAAAAAAAAAAAAAAAAQP/aAAgBAgEBPwAH/8QAFBEBAAAAAAAAAAAAAAAAAAAAQP/aAAgBAwEBPwAH/9k=) | mp | simple, cartoon-style silhouetted outline of a person (does not vary by user)
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgBAMAAACBVGfHAAAAGFBMVEVPMTn///+hkZWsnqKWhInz8fG3q67o5OVjymXqAAAAoElEQVQoz82OwQ3CMBAEV8ENXCzxdjowHeBHCnBQ/jRB/2TWwjVwq5H2tXOK3HPkLYAoaq9RlwCirNeFNnCqyoUWcM7jcxQpwX7upzdWqcHciJIC5kasLcAb+DVudPwaNzp+pOBO5S1wx6/HXeCOX7e3wN3+caPbP879b/4oetoPSt447Ac1b/SCFFJ4o6/4ocXYsB9+G/bD3MAPcwM/kC/KhCQv+Oa0WgAAAABJRU5ErkJggg==) | identicon | a geometric pattern based on an email hash
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAB2lBMVEXw3/Q3t350dHTn1+uwo7LAssOnp6dVVVWhoaGamprs3PDp2e3j0+ZxcXHZyt2UlJQ1sXlwcHBcW1zTxNapnauMjIyHfol3b3lvb29qampoZ2jh0eTez+K5ubmmm6iakJyYj5qTiZV+mJOSkpKIh4h8fHx4eHg0p3RsbGxiYGJQUFAgbUvQwdPOwNLNzc3Hucq/vcC5rbu4q7u2qrmVjJeWlpaTk5ORh5OPiZGPj4+LhoxylouJgYuAd4JzioB+dYB+fH96eHs0rXcwoW9uZ29Chmg7hWVkY2VgW2I4c1lOTU9MTEzJu8y9r8C0p7e1tbWyqbWiqa+rn66ro62qqqqkmKahl6Ock56MnJyFgYWEhIR1hn98c35lf3ZzbnRJhmsvmGlUdmg4jGctkmVkXWVRaV9fX180eltEa1kmf1dFZVdVUVZHR0f////o2OzVytvY2NjT0tPKvs3AvMjCtMXCu8Sqsbeor7WxsbGtobCurq6mqqicn6ajo6Oenp6OjZWJiYlymohwj4dxioVDt4Nil4N4i4OAgIAzqXQ6onRcfm85mW5LgWw6kWtkbGhgaGdAgWRUbGMwimJNZF5KZFxZWVlLVFBJRUo9UEg5UEgfZ0c8PDw7OTsgQzTXmnPvAAACSUlEQVQ4y42ShXPiQBSH325ISBqCe4sWKFJ3B4pD3d2u3p67u7v7/3pLgB5Q5ua+yWQy+X37due9hf9CXl/1z/zC+XPjZyBHK4BGVi6Mn+64EV0Wi1BWoCahnJrmxmaZLKinAKrpKykeQDIDwE9ZLoNItWGgiQe+YWCZgpaJOvT47OSwPGhINjY3ips1qf0Zv3qErx81bMHVCEJoUxvVO7p+9VxrgSyrWIqPjF59FdADH+tIXhcIPOxP4CO11waEUR8RjH6887VL/mo/gFDkxxBCKfxZKsXeWSJsYSwVH+Hta4TW9yMBRFDuZXAGY5MWIGne8Ru9RNgm5QlkuWgcYJMaq3xWANA4ZrRp6fYzVMK6GadxkpZDHvoUKmNX9TOhKRpH34Nve8fShy+/+zbUvn4oYc6UKghx2/Vsh6lSoSp6QLLYS/Lqg4rUfFduLlluPkJovuKlGLF+ejc9uHSfVLgrOxE3HAq17O7gEyXK8ibca6OLT0C1uxnF01Dn2BoS2WAZhgvrG46b4GLYWmFsZS2uzAkxXQfHkn+5ccoWdIxCZ5oeJGmBF5yC5Wo7JWL5MMfc4ViVJY7+MvS+e5HrIVeAUN/TybDu7pAlhop4fpE3L87lDqgyGiSUJuRxrzid8xKRW07nBCzcloBIt8IB0Mq4OC0UI8O6vDB7D1MAU71WvkSQuIz5TjTpFG1wkvYOoTCkVXclwaXozec2qVmtLY81/WnhsEb8NJhUgkdwlObVCZXZ4/ENA+ESTbfa7V1lAk23tdvtQQr+AEpRWa/mX8zUAAAAAElFTkSuQmCC) | monsterid | a generated "monster" with different colors, faces, etc.
![](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAQDAwMDAgQDAwMEBAQFBgoGBgUFBgwICQcKDgwPDg4MDQ0PERYTDxAVEQ0NExoTFRcYGRkZDxIbHRsYHRYYGRj/2wBDAQQEBAYFBgsGBgsYEA0QGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBgYGBj/wgARCAAgACADAREAAhEBAxEB/8QAGwAAAQQDAAAAAAAAAAAAAAAABAMFBgcBAgj/xAAbAQACAwEBAQAAAAAAAAAAAAACAwAEBgcBBf/aAAwDAQACEAMQAAAA7bDwNf1URYFK7aFah061OMmdYZHaxjHR6yMLmEsbVQ8o1RuMQhGZD//EAC4QAAEDAwMBBwIHAAAAAAAAAAECAwQFESEABhIHEyIxUVKR0kGiFSMkNGFiof/aAAgBAQABPwD8Vlvy0R4pbF0laluXISBbFhbxv5/TTm4JLTpQZcXH9VfLTm55KGlLEqKbD0K+WqDvw1Sqv054Nh1CO0Spu4BSDYggk+ac3zc4Fs06euQ6+Uryhk/6U63HRRL620eGjY8KpUidBck1iryePNiV3vygmwNgUoAJKuQXcHGOn9I/QVmpVzaEbblbiVYx6ezG4FMmJ61FKbpAGQoqss4462nNVG3u6ortyiuj729bOqTbzs/tFjDIt76mVVbFUkJehurY5XQ+xZfdsLhSb8r8uXgCLWzpdWXI4oiwng0T33n7NpCfrZJPMny7oH86jTRG3chSVYVHeH3tapPV52lKfLRbd7ZHCy74ze+DpXWCSpfK8T2V8tHq7IN/2nsr5af6lokPNPHsm1tIUm7dxfkQT4k+lOv/xAAiEQACAgECBwEAAAAAAAAAAAABAgARAwQSEyExQWGBwfD/2gAIAQIBAT8A3Q5wIdQBMOoGW67QtamZCoQFW5xypw3u5/u00Brf6+wMNpuEi+sYius0Zrf6+zjCiDKTzKTzEdUFLP/EADARAAECBAIGCQUAAAAAAAAAAAIBEQADBSEEBgciMUFhkRITVGKSwcLS4UJRcoGh/9oACAEDAQE/AJA9Y99kDSTJHRV5fMDRTJWf+fMValzKb0FNXQnbdsZ7ftIoKocwkXh5xgJc6ZiSGfL1b/TZtyou/nGFHEDUEFJbBd9WyJ+W/nGkRhDCt3vTGVnmTDbh5xLA0HZaJYH0ktGkzVDCP3/TGX81FSJxTEBDQkuiq2zjeE0vn2UfEvthNMB9lHxL7YzPnebXylqYIAi7IivtZ72+0f/Z) | wavatar | generated faces with varying features and backgrounds
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgAQMAAABJtOi3AAAABlBMVEVLAmn9LdWXmTS+AAAAMUlEQVQI12N4wMDAj0wUyCATDAUyDMgE/wMEARbDIOQbmD8gEx/kkQmZApkCJIIwAAAZjxw4Pi/EJgAAAABJRU5ErkJggg==) | retro | awesome generated, 8-bit arcade-style pixelated faces
![](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDAwMEAwMEBQgFBQQEBQoHBwYIDAoMDAsKCwsNDhIQDQ4RDgsLEBYQERMUFRUVDA8XGBYUGBIUFRT/2wBDAQMEBAUEBQkFBQkUDQsNFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBQUFBT/wgARCAAgACADAREAAhEBAxEB/8QAGgAAAQUBAAAAAAAAAAAAAAAACQABBgcIBP/EABkBAAIDAQAAAAAAAAAAAAAAAAAFAwQGAf/aAAwDAQACEAMQAAAAKmFTQT2dNB19GAcj3fTwWbgRZRgG/Z38htKyALMogqCxfyBdakdVZv8A/8QAKBAAAQMDBAEEAgMAAAAAAAAAAgEDBAUGEQAHCBIhEBMiMRQkMkJS/9oACAEBAAE/ANbv71SdsatRILFtzqutSkjH98U6MopKiIiH5yXlVxj+uqe6+9BYclMDGkmCE4yLnuIBY8j2wmcfWcevNTlQtyXJKsq3ak/T4dEnKD8qKRNGclvIkvuf5RVIRQcYUVJV1wb5PXJet1zbBvGpFWjKN+ZSqm8Qm9gfJsmafz+OSQl+SYJF9d+OJNfi7n3XV27br9xU2rVBZ8OTQBjGgA453eB4XF7IY5JBwnVdcCuOVXS8I+69RzTKE2zJYosJ0wKU+hEbSuPIHxFBHI4+1L15N7k1javbF2r0IYS1A5Tcb94FMUAhMjUQQh7lgPrKa4b7/wC4q3jaVty3YMbbFme9RTMWA7rLfZekMNqXZXEVTEkFcIOkXOv/xAAlEQABAwEIAgMAAAAAAAAAAAABAgMEEQAFEBITITFBMlFCccH/2gAIAQIBAT8Ast0INKWHG+MJiMkZ5XfA/bXjDbaGqz4+sZN43olDTd2aSQkHNqBRJPxpl6913s/eDsiO227TOAMxGwJ7oPVeK4xmkvOpbUaV2tNitQyW6kq6+sP/xAAkEQABAwQBAwUAAAAAAAAAAAABAgMRAAQFIRASMXETFEFRof/aAAgBAwEBPwCm2usEzXjnCYfqb9w62VSNa1FZjGt249dgQmYI5x+Xtk26G3DBSIOu+jG/MTWWyiLlsMt7+z2/ObFlFw+lpwwDWSsbeyBbBJX8eOP/2Q==) | robohash | a generated robot with different colors, faces, etc.
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgAQMAAABJtOi3AAAAA1BMVEUAAACnej3aAAAAAXRSTlMAQObYZgAAAAtJREFUCNdjGOQAAACgAAH4BzM6AAAAAElFTkSuQmCC) | blank | a transparent PNG image
  | notfound | return an HTTP 404 (File Not Found) response
  | noavatar | the user will not have a `picture` property

##### Client logo flags

The following flags modify the generated logo.

Logo | Flag | Description
--- | --- | ---
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgBAMAAACBVGfHAAAAJFBMVEX/VyL76ef+dkz71s774t39noL8uqf9kXD+glz/Zjb8xrf9qZHgm7oqAAAAlElEQVQoz6XNwQ0CMQwEwPUhIZ5rgcQXRAOUcCUcJVACHVACdEAJlMh5E5Dlzz1YR4k0iWN4yQ9WFWALQPgSWAYgALh1wBxa7E/BC5jAIyICAHbmbhNgM7Dd6GTAA5HTXa5KuVSwsQL/Bx8rqCowfbG1Agzw3HENmNAzODwWU4fA04wG7A/eJviKHeCCJsMea29Q8gH9RxXZMd8OgAAAAABJRU5ErkJggg==) | icon | [Game-icons.net](https://game-icons.net/) icon as a logo (default)
![](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAYEBAUEBAYFBQUGBgYHCQ4JCQgICRINDQoOFRIWFhUSFBQXGiEcFxgfGRQUHScdHyIjJSUlFhwpLCgkKyEkJST/2wBDAQYGBgkICREJCREkGBQYJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCQkJCT/wgARCAAgACADAREAAhEBAxEB/8QAGQAAAwADAAAAAAAAAAAAAAAAAwQGAgUH/8QAGAEBAQEBAQAAAAAAAAAAAAAABgUEAwL/2gAMAwEAAhADEAAAAASHNXa056c8HP8ANkeusPyLOLuuNvc5byaaDbHQy6XH2GuA1ZxYPrmmEZP/xAAuEAABAwIFAwIEBwAAAAAAAAABAgMEBREAITFBUQYScQciFGGBoRMyM4KRksH/2gAIAQEAAT8A9HPT1mndMtPSWEKkPgPvFY3Oif2jFIpIlTZbIUoMpUlBUDmfbfI83++KlCXSHwxEJSJC9ASeVKt87ZeABtj1YoEiu0B2LNYR8THBehu6kLAuW720UBa17XANztSOokwaOSMwoFSlk2CTve+nP1x03W2GWnXJDqWUuO5FZ7ArPM57knTxpiqVVpVUgFVz2lRBPix+x+xx1xKjSobamFBStAUkHOxIz8gHBpyZcj8U+1squv3WCc/GoJH8njOJGbkLKVuraQpAUhIV+Ygg9pO4NsxwPGKhAkxgiK4opfjICw4q/cogDjQk2H1POH5lReaWmSsPFA7UWCQCom225sc+LnI3t05UY/UNFiVRkBRdQEvI07XAlQWP7km3BBxGmOxYJi/DtusKIUF6qQf9Gmp2xUJTD6OyO4p1Q/UWSVdxyyGW1uecdTTo9Ao8uovaMBYabXY9zujQA+V0g22F8f/EACwRAAECBQICCgMAAAAAAAAAAAECBAADESExEkEFYRMUMlFxkcHh8PEigdH/2gAIAQIBAT8A4k5UFdCnAz4+0NXC1MES0mn5H+w0dFpImrVemK3vT6MNn6nZKJhqoYhwhap9KXMM2iGzWWiYoAm+dztztHHmpS11p2Vf9j2hlMMtwlQ2IhHCZ8qdrVhO+ceQMO19aWrWvSUdkd45czmGM2aUKaTb6sD09YZcJWp2lGkgA38AeflCp5nNqitabZsKYia0UhJHbBNlYp31r8pCGhTN6RJ1KF1KJsOX0IW4UJSp69sV54PzIBMf/8QAKxEAAgECBAQFBQEAAAAAAAAAAQIRAAMEBSExE0FRYRIicYHBMlKRodHw/9oACAEDAQE/AMutjA4dfvfU9ulYu4i3uKwBaNPzRspi2Qt3n0msyyyy+HLWOWtXcKtxg5MAVnPFu32aypIUAbToOf73rIvExdWO66ex1rBWHCOj9Kv51hnAVWktsJ117bilThongSZPm7aTPxWIawFGKtkQDqff+0+Y20wzXZBkae9ZeFW8HYjXrMT0nl27GKwuJ494XSeGyyGT6vFGxEH4NHHlbbC6ptqfKiBRJjn6eugoJwXKqYG8Dr0P+MSB1j//2Q==) | fractal | [Electric Sheep](https://electricsheep.org/) fractal as a logo

##### `Group` size flags

The following flag modify the sizes of the generated team (group of users) and fleet (group of clients).

Flag | Size
--- | ---
tiny | 5 (default)
small | 10
medium | 25
large | 50
huge | 100

#### Name

In most cases, the generated objects have a full name, which is generated from the identifier. Instead of being generated, the full name can be produced from the identifier, if the identifier contains at least one period (`.`) or space (` `) character. In such cases, these characters play the role of separator between the parts of the full name (e.g. family name, given name). That is, the full name isn't randomly generated from the identifier but, by taking the separator characters into account,  it is produced from the single parts of the full name (with capitalised initial letters). For this purpose, it is advised to use a period character, rather than a space character.

```
joe.black;sketch
```

In the above example: The full name of the user generated by the user generator is *Joe Black* (and his avatar is a skecthed profile avatar). The [profile page](https://phantauth.net/%7Ejoe.black%3bsketch) of this example can be found [here](https://phantauth.net/%7Ejoe.black%3bsketch).

#### Picture

In most cases, the generated objects have an image (avatar for a user, logo for a client), which is generated from the identifier. The *flags* determine which pre-defined inventory the image comes from (see [flags](#flags)). It can be further customized by the use of [Gravatar](https://gravatar.com).

Each object has a generated unique email address (`email` for a user, `logo_email` for any other objects). To customize the image of a given object, you need to assign the gravatar image to this email address. By default, an object has a gravatar image, and the generated image is the default value of the gravatar URL only. In other words, as soon as you create a gravatar image to a given email address, that image will appear as the image associated with the given object.

#### Email

A disposable, operational email address suitable for receiving incoming emails is generated to each object. You can use your own email address (e.g. a previously set test email address) instead of a generated email address, if you prefer. In this case, the identifier contains an email address. Consequently, the image associated with the given object is the gravatar image assigned to the email address contained in the identifier.

```
ivan.test.szkiba@spam4.me
```

In the above example: The email address of the user generated by the user generator is *ivan.test.szkiba@spam4.me* (and his name is *Ivan Test Szkiba*). The [profile page](https://phantauth.net/%7Eivan.test.szkiba%40spam4.me) of this example can be found [here](https://phantauth.net/%7Eivan.test.szkiba%40spam4.me).

### Custom Generators

PhantAuth can use external data sources and generators as well. The only restriction is that the external generator has to be deterministic. This means that even if called several times, it has to generate the same object to the same identifier.

A special case of external generators is if an external data source is used. In such cases, the properties of a given object can be provided in a comma separated value (CSV) file or a Google Sheets document.

The external data sources and generators can be defined by the use of so-called [tenants](https://doc.phantauth.net/#/tenant). To learn more, please go to chapter [Tenant](https://doc.phantauth.net/#/tenant).


# Group User

The *user* resource contains the [Standard Claims](https://openid.net/specs/openid-connect-core-1_0.html#StandardClaims) defined in the [OpenID Connect Core](https://openid.net/specs/openid-connect-core-1_0.html) specifications. It also includes some PhantAuth-specific property.

To use PhantAuth as an OpenID Connect provider, you don't need to carry out the user-related operations described here.
You don't need to generate users in advance. If PhantAuth requires a piece of data that belongs to a specific user, it will be generated in runtime.
The deterministic nature of the generators guarantee that the same user object will be generated to the same user name.
The only exception is selfie token generation, when the provided user data are used to create a so-called selfie token, which can later be used as a login name.

## User [/user]

### Get a User [GET /user/{username}]

Use this endpoint to generate a random user. The user is generated in a deterministic way, on the bases of the user name given as a path parameter.
In the case of identical user names, the endpoint will generate the same user object. The properties of the generated user object are randomly generated on the basis of the user name.
In lack of a user name, all calls generate a different user object to the randomly generated user name.

By providing an email address as the `username` parameter, you can customize the user picture by the use of the gravatar associated with the email address.

If the `username` parameter contains at least one dot (`.`) or space (` `) character, the whole name is produced from the parameter, rather than being generated.
In this case, these cahracters play the role of separator between the units of the full name (family name, given name).`

The result is always a user object. If you want to generate multiple users in one single step, you can do it by the use of *Team* generation.
The members of a team are users randomly generated from the team name.

+ Parameters
   + username (optional, string) ... The username or email used for generation purposes.

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

To create a selfie token from the user data, you need an opaqe string token, which contains the encoded user properties sent in the request.
Later, the selfie token can be used as a login name. In this case, the user data is included in the selfie token, that is, the user properties are taken from the token.
By the use of a selfie token, you can use your own user objects during the authentication process.

Its use, however, is limited by its relatively large size (more than 100 characters), which exceeds the maximum size of the user name in several systems.

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

It is used to generate OpenID Connect tokens as path parameters to a user of a given name.

This method is mainly used in the testing process, when, for example, the token received from the normal authenticaton flow is not available to the test code.
Generating an access token, for example, will let you avoid authentication, and immediately call an operation requiring the access token.

+ Parameters

    + username (required, string) ... A username or email.
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

# Group Client

The client object contains standard OAuth2/OpenID Connect client properties. To use an OpenID Connect flow, you need a client_id. Certain flows also require a client_secret. The client object contains the client_id and client_secret values, as well as some properties to be displayed to the user (e.g. logo, client name, version).

## Client [/client]

### Get a Client [GET /client/{client_id}]

Use this endpoint to generate a random client. The client is generated in a deterministic way, on the bases of the client ID given as a path parameter.
In the case of identical client IDs, the endpoint will generate the same client object. The properties of the generated client object are randomly generated on the basis of the client ID.
In lack of a client ID, all calls generate a different client object to the randomly generated client ID.

By providing an email address as the `client_id` parameter, you can customize the client logo by the use of the gravatar associated with the email address.

If the `client_id` parameter contains minimum one dot (`.`) or space (` `) character, the client_name is produced from the parameter, rather than being generated.`

The result is always a client object. If you want to generate multiple clients in one single step, you can do it by the use of *Fleet* generation.
The members of a fleet are clients randomly generated from the fleet name.

+ Parameters
   + client_id (optional, string) ... A client ID or email.

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

To create a selfie token from the client data, you need an opaqe string token, which contains the encoded client properties sent in the request.
Later, the selfie token can be used as a client ID. In this case, the client data is included in the selfie token, that is, the client properties are taken from the token.
By the use of a selfie token, you can use your own client objects in the authentication process.

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

It is used to generate a OpenID Connect token as a path parameter to a client of a given client ID.

It is primarily used for testing purposes, when, for example, the token from the standard authentication flow is not available to the test code.

+ Parameters

    + client_id (required, string) ... A client ID or email.
      
    + kind (required, enum[string]) ... A token kind.
      
    
      Token type
    
      + Members
          + 'registration'
          + 'selfie'
          + 'plain'

+ Response 200 (text/plain)

    + Body

            eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJtYWdpYy50b29sYm94IiwidG9rZW5fa2luZCI6IlJFR0lTVFJBVElPTiIsInNjb3BlIjoib3BlbmlkIHByb2ZpbGUgZW1haWwgYWRkcmVzcyBwaG9uZSBpbmRpZWF1dGggdWlkIiwiZXhwIjoxNTg4NDI4NDM4LCJpYXQiOjE1NTY4OTI0Mzh9.TGilMHuWIDYiBAjzXyMuBvMiRlnKFLDX7FJJW_flldg


# Group Team

Team is a group of users under a given name. For the purposes of identification and visualisation, the team object has its own properties (e.g. logo), the most important of which is the `members`, which contains the user objects of the team.

## Team [/team]

### Get a Team [GET /team/{teamname}]

Use this endpoint to generate a random group of users. The team is generated in a deterministic way, on the basis of the team name given as the path parameter.
In the case of identical team names, the endpoint will generate the same team object. The properties of the generated team object are randomly generated on the basis of the team name.
In lack of a team name, all calls generate a different team object to the randomly generated team name.

+ Parameters
   + teamname (optional, string)
     The identifier or email address of the team; it is integrated in the `sub` property and is the basis of the other generated properties.

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

# Group Fleet

Fleet is a group of clients under a given a name. For the purposes of identification and visualisation, the Fleet object has its own properties (e.g. logo), the most important of which is the `members`, which contains the user objects of the fleet.

## Fleet [/fleet]

### Get a Fleet [GET /fleet/{fleetname}]

Use this endpoint to generate a random group of clients. The feleet is generated in a deterministic way, on the basis of a fleet name given as a path parameter.
In the case of identical fleet names, the endpoint will generate the same fleet object. The properties of the generated fleet object are randomly generated on the basis of the fleet name.
In lack of a fleet name, all calls generate a different fleet object to the randomly generated fleet name.

+ Parameters
   + fleetname (optional, string)
     The identifier or email address of the fleet; it is integrated in the `sub` property and is the basis of the other generated properties.

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

# Group Tenant

To customize the application, you need to use one or more so-called tenants. A tenant can be consiered as an independent PhantAuth service. A tenant has its own random user generator endpoints and OpenID Connect endpoints.

The tenants can be organised into so-called domains. Practically, a domain is a DNS zone, which contains the settings of the given tenant(s). The tenants as well as the domain can be configured by the use of DNS TXT records.

The URL of the tenant issuer is in `https://phantauth.net/_{tenant}` format, where `tenant` is the fully qualified DNS name associated with the tenant. When using a PhantAuth official tenant, you can omit `phantauth.net` from the end of the name. When using a community-created, shared tenant, `phantauth.cf` can be omitted from the end of the name.
When using a default tenant (default.phantauth.net), the issuer URL is identical with the PhantAuth base URL, that is, [https://phantauth.net](https://phantauth.net).

The resource URL is relative to the URL of the tenant issuer URL, that is, the endpoint address of the random user generator for the tenant named `faker` is: [https://phantauth.net/_faker/user](https://phantauth.net/_faker/user).

## Tenant [/tenant]

### Get a Tenant [GET /tenant/{tenantname}]

This endpoint allows you to get the data of a given PhantAuth tenant. To use the PhantAuth services, you don't need this endpoint.
It is, therefore, mainly used for debug/diagnostic purposes in tenant customization.

Tenantname is the name of the full DNS domain of the tenant you get.
In the case of an official and shared tenant (phantauth.net and phantauth.cf DNS domains), the DNS domain can be omitted (e.g. *default* or *faker*).

+ Parameters
   + tenantname (required, string) ... The tenant ID integrated in the `sub` property.

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


# Group Domain

A domain object contains several tenants; it can be considered a group of tenants. The PhantAuth official tenants are collected in a domain identified by `phantauth.net`.
In the `phantauth.cf` domain, you can share and register your own tenants as well.

A domain can also be used as a tenant, that is, it has an issuer endpoint and some resource endpoints. The issuer URL of the domain is in `https://phantauth.net/_{domain}` format, where `domain` is the fully qualified DNS name associated with the domain, that is, for example [https://phantauth.net/_phantauth.net](https://phantauth.net/_phantauth.net) or
[https://phantauth.net/_phantauth.cf](https://phantauth.net/_phantauth.cf). When using a default domain (phantauth.net), the domain name, that is, the URL of the default domain issuer, [https://phantauth.net/_](https://phantauth.net/_) can be omitted.

## Domain [/domain]

### Get a Domain [GET /domain/{domainname}]

This endpoint allows you to get the data of a given PhantAuth domain. To use the PhantAuth services, you don't need this endpoint.
It is, therefore, mainly used for debug/diagnostic purposes in tenant customization.

Domainname is the fully qualified DNS name of the domain you get (e.g. *phantauth.net* or *phantauth.cf*).

+ Parameters
   + domainname (required, string) ... The domain ID integrated in the `sub` property.

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
  Subject - User identifier at the issuer.
  
+ name (optional, string)
  The user's full name in displayable form, including all name parts, possibly including titles and suffixes, ordered according to the enduser's locale and preferences.

+ address (optional, Address)
  The user's preferred postal address.

+ given_name (optional, string)
  The user's given name(s) or first name(s).

+ family_name (optional, string)
  The user's surname(s) or last name(s).

+ middle_name (optional, string)
  The user's middle name(s).

+ nickname (optional, string)
  A casual name of the User that may or may not be the same as the given_name.

+ preferred_username (optional, string)
  A shorthand name by which the user wishes to be referred to at the Relying Party.

+ profile (optional, string)
  The URL of the user's profile page.

+ picture (optional, string)
  The URL of the user's profile picture.
  
+ website (optional, string)
  The URL of the user's webpage or blog.

+ email (optional, string)
  The user's preferred email address.

+ email_verified (optional, boolean)
  True if the user's e-mail address has been verified; otherwise false.

+ gender (optional, string)
  The enduser's gender. Possible values are: female, male, and unknown.

+ birthdate (optional, string)
  The user's birthday, represented as an ISO 8601:2004 [ISO8601‑2004] YYYY-MM-DD format.

+ zoneinfo (optional, string)
  A string from the zoneinfo time zone database representing the user's time zone. For example, Europe/Paris or America/Los_Angeles.

+ locale (optional, string)
  The user's locale, represented as a BCP47 [RFC5646] language tag. It is an ISO 639-1 Alpha-2 language code in lowercase and an ISO 3166-1 Alpha-2 country code in uppercase letters, separated by a dash.

+ phone_number (optional, string)
  The user's preferred telephone number.

+ phone_number_verified (optional, boolean)
  True if the enduser's phone number has been verified; otherwise false.

+ updated_at (optional, number)
  The time when the User's information was last updated. Its value is a JSON number representing the number of seconds from 1970-01-01T0:0:0Z as measured in UTC until the date/time.

+ me (optional, string)
  The simplified URL of the user's profile page.
  
+ password (optional, string)
  The user's generated password.

+ uid (optional, string)
  The user's simplified, shortened identifier at the Issuer.
  
+ webmail (optional, string)
  The URL of user's mailbox in a webmail application.

+ @id (optional, string)
  The URL of the user's JSON representation.

## Address (object)

+ formatted (optional, string)
  Full mailing address, formatted for display or use on a mailing label. This field MAY contain multiple lines, separated by newlines. Newlines can be represented either as a carriage return/line feed pair or as a single line feed character.

+ street_address (optional, string)
  Full street address component, which MAY include house number, street name, post office box, and multi-line extended street address information. This field MAY contain multiple lines, separated by newlines. Newlines can be represented either as a carriage return/line feed pair or as a single line feed character.

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
  An email address used to generate a gravatar.com logo_uri.

## Team (object)

+ sub (required, string)
  The name or email address of a given team. The team properties and team members are generated from this name. If you provide an email address, you can customize the team logo by the use of the gravatar associated with the email address.

+ name (optional, string)
  The displayed team name.

+ logo (optional, string)
  The URL of the team logo, which can be customized by the gravatar associated with the email address in the `logo_email` property.

+ logo_email (optional, string)
  The email address of the team, either generated or provided in the `sub` property. The team logo can be customized by the use of the gravater associated with this email address.

+ @id (optional, string)
  URL of the Teams's JSON representation.

+ profile (optional, string)
  The URL of the Team profile.

+ members (optional, array[User])
  The user objects that generate a team member.


## Fleet (object)

+ sub (required, string)
  The name or email address of a given fleet. The fleet properties and fleet members are generated from this name. If provide an email address, you can customize the fleet logo by the use of the gravatar associated with the email address.

+ name (optional, string)
  The displayed fleet name.

+ logo (optional, string)
  The URL of the fleet logo, which can be customized by the gravatar associated with the email address in the `logo_email` property.

+ logo_email (optional, string)
  The email address of the fleet, either generated or provided in the `sub` property. The fleet logo can be customized by the use of the gravater associated with this email address.

+ @id (optional, string)
  URL of the Fleet's JSON representation.

+ profile (optional, string)
  The URL of the Fleet profile.

+ members (optional, array[Client])
  The client objects included in a fleet.

## Tenant (object)

+ sub (required, string)
  The fully qualified DNS domain name of the tenant. In the case of official and shared tenants (phantauth.net and phantauth.cf DNS domain), the DNS domain can be omitted (e.g. *default* or *faker*).

+ issuer (required, string)
  The URL of the tenant OpenID Connect issuer. This value allows you to get, for example, the [OpenID Provider Metadata](https://openid.net/specs/openid-connect-discovery-1_0.html#ProviderMetadata).
  As a webpage, it contains information on the use if the given tenant.

+ website (optional, string)
  The website address associated with the tenant. If a tenant doesn't have a website, its value is identical with that of the `issuer` property.

+ template (optional, string)
  It defines the place of the templates of the HTML pages of the tenant in [RFC 6570 - URI temaplate](https://tools.ietf.org/html/rfc6570) format.
  The URI template receives the page name in a `resource` parameter. By default, it takes the following value: `https://default.phantauth.net{/resource}`.

+ factory (optional, string)
  The address of the custom random resource generator (user, team) in [RFC 6570 - URI temaplate](https://tools.ietf.org/html/rfc6570) format.
  The URI template receives the type of the object to be generated (user, team) in the `kind` parameter, and the identifier of the object to be generated in the `name` parameter.

+ factories (optional, array[string])
  A list of resource types supported by the external generator set in `factory`.

+ depot (optional, string)
  It defines the place of the CSV file containing the resource data in [RFC 6570 - URI temaplate](https://tools.ietf.org/html/rfc6570) format.
  The URI template receives the type of the object to be generated (user, team) in the `kind` parameter.

  The first line of the CSV file contains the resource property names, the following lines, on the other hand, contain the relevant data.
  In the case of nested properties, a '.' character separates the elements of the property name (e.g. address.formatted).

+ depots (optional, array[string])
  A list of resource types supported by the external CSV set in `depot`.

+ userinfo (optional, string)

+ @id (optional, string)
  The URL of the tenant's JSON representation.

+ name (optional, string)
  The displayed tenant name. In lack of such name, the DNS name of the tenant is displayed in the address bar of the tenant's webpages.

+ logo (optional, string)
  The URL of the tenant logo. The image from this address appears in the address bar of the tenant's webpages and the pages that contain the list of available tenants.

+ favicon (optional, string)
  The URL of the tenant favicon. The image from this address appears as a shortcut icon in the browser when a user visits the tenant's webpages.

+ theme (optional, string)
  The URL of the CSS style sheet used for the tenant's webpages.
  The default webpage templates were created by the use of the Bootstrap library, therefore, the Bootstrap CSS URL has to be provided when such a webpage is used.

+ script (optional, string)
  The URL of a custom JavaScript file can be automatically inserted in the login.html, consent.html, és test.html pages.

+ sheet (optional, string)
  It is used to give the identifyer of a public Google Sheet document. The first line of the table contains the user property names, the following lines, on the other hand, contain the relevant data.
  In the case of nested properties, a '.' character separates the elements of the property name (e.g. address.formatted).

+ summary (optional, string)
  A one-line description, the watchword of the tenant. It appears on the tenant's startup page and the pages that contain the list of available tenants. It takes the valua of an unformatted text.

+ attribution (optional, string)
  The attribution of the external data source or random user generator. Its value can have markdown formatting, that is, the external source can contain highlights and links.

+ about (optional, string)
  A detailed description of the tenant. If it takes the value of an URL, the description is downloaded from the given URL, otherwise the value it takes is the description itself. Markdown formatting can be used in the description.

+ domain (optional, boolean)
  True in the case of a domain tenant collecting several tenants, otherwise false.

+ subtenant (optional, boolean)
  True in the case of a tenant referred to in a domain tenant, otherwise false.

## Domain (object)

+ sub (string)
  The fully qualified DNS name of the domain (e.g. phantauth.net).

+ name (optional, string)
  The displayed domain name.

+ logo (optional, string)
  The URL of the domain logo. The image from this address is displayed on the webpage of the domain.

+ @id (optional, string)
  The URL of the domain's JSON representation.
  
+ profile (optional, string)
  The URL of the domain's webpage.

+ members (optional, array[Tenant])
  The tenants included in a domain.
