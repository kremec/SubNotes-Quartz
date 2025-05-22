### Zgodovina
- Swagger 2.0
- OpenAPI Specification (OAS) 3.0ž
Format: ==json== / ==yaml== - nadmnožica json
### Sklopi OAS
![[OpenAPI 3-Image-1.png]]
- ==info==: opis - title, description, contact, licence, version
- ==servers==: URL predloge dostopov - subdomain, version, ...
- ==security==: avtorizacijska shema - scheme (npr. basic / bearer / OAuth / ...), bearerFormat
- ==paths==: URL poti do posameznih virov
- ==tags, externalDocs==: označbe in dokumentacija
- ==components==:
    - requestBodies: description, required, content/schema - uporaba referenc na tipe objektov
    - responses: code, description
    - links: uporaba rezultatov ene operacije kot vhod za drugo operacijo
    - parameters, examples, headers, callbacks
### Orodja Swagger
- Swagger Editor: urejevalnik OAS specifikacije
- Swagger UI: vizualni prikaz specifikacije
- Swagger Core: generacija OAS na podlagi anotacij v kodi
### Java anotacije
#### Operations
- `@Operation`: opis
- `@RequestBody`: vsebina zahtevka
- `@ApiResponse`: vsebina odgovora
- `@Callbacks`: množica zahevkov
- `@Parameter`: parameter
- `@Link`: design-time povezava odgovora
- `@LinkParameters`: povezava
- `@Content`: shema in primeri odgovora
- `@Schema`: vhodni izhodni podatki
#### Info
- `@Info`: splošni metapodatki
- `@Contact`: kontaktni podatki (npr. mail)
- `@Licence`: licenca API
- `@Extension`: razširitev
- `@ExtensionProperty`: lastnosti razširitve
#### Security
- `@SecurityRequirement`: seznam zahtevanih varnostnih shem za operacijo
- `@SecurityScheme`: definicija varnostne sheme
- `@OAuthFlow`: definicija varnostne sheme
- `@OAuthFlows`: konfiguracija OAuth tokov