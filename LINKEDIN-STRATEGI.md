# LinkedIn-strategi för A/B-test på Shoreline

En organisk och en betald post. Båda pekar mot splittersidan `test.shorelinetechstudio.se`. Ingen vet vilken variant de landar på.

## Deploya splittersidan i Coolify

Samma flöde som variant A och B. Domän: `test.shorelinetechstudio.se`. Lägg A-record i Cloudflare mot Coolify-IP.

När den är live: klistra in i webbläsare. Du ska tvingas till a.shorelinetechstudio.se eller b.shorelinetechstudio.se slumpmässigt.

## UTM-taggade länkar (använd dessa, inte bara domänen)

Splittersidan läser av query-parametrarna i länken du delar och skickar dem vidare automatiskt till a- eller b-sidan (`params.set` bevarar det som redan finns i URL:en). Så GA4 fångar källan på slutsidan utan att du behöver ändra i koden. Använd dessa exakta länkar istället för `test.shorelinetechstudio.se` rakt av, så kan du i GA4 → Reports → Acquisition separera organiskt inlägg från betald annons:

**Organiska inlägget:**

```
https://test.shorelinetechstudio.se/?utm_source=linkedin&utm_medium=organic&utm_campaign=abtest
```

**LinkedIn Ads Destination URL:**

```
https://test.shorelinetechstudio.se/?utm_source=linkedin&utm_medium=paid&utm_campaign=abtest
```

## Det organiska inlägget

Postas från både din personliga LinkedIn och Shoreline TechStudio-sidan för maximal räckvidd. Neutralt formulerat så det inte avslöjar att det är ett test.

### Kortare version (rekommenderas, hög läsbarhet)

```
Vi har testat olika sätt att prata om vad vi faktiskt gör på Shoreline.

Är det en teknisk byrå som "bygger tillväxtmotorer"? 
Eller en studio som gör så att du kan "anställa en digital medarbetare"?

Samma verksamhet, två helt olika sätt att förklara den.

Om du driver ett litet företag: kika in en 30 sekunder och säg vilken känsla du får. Vi läser varje kommentar.

→ test.shorelinetechstudio.se/?utm_source=linkedin&utm_medium=organic&utm_campaign=abtest

#småföretagare #digitalisering #AI
```

### Längre version (mer engagerande, men riskerar att avslöja upplägget)

```
En liten uppdatering från Shoreline.

Vi bygger hemsidor och AI-lösningar åt småföretagare i Sverige. Men vi har märkt en sak: hur vi PRATAR om det vi gör verkar betyda mer än hur bra vi är på det.

Vissa besökare bounces direkt när vi säger "AI-agent".
Andra stannar när vi säger "digital medarbetare".

Samma tjänst. Olika reaktion.

Så vi bygger om vår startsida. Innan vi rullar ut: vad tycker du?

→ test.shorelinetechstudio.se/?utm_source=linkedin&utm_medium=organic&utm_campaign=abtest

Läser varenda kommentar. Tack.

#småföretagare #tech #startup #AI
```

### Timing

Publicera mellan 07:30 och 09:00 svensk tid för högsta räckvidd bland svenska småföretagare. Måndag till torsdag är bäst, undvik fredag eftermiddag och helg.

## Betald LinkedIn Ads-kampanj

Detta ger dig kall trafik som inte känner dig personligen. Guldstandard för A/B-testet.

### Steg för steg

**1. Öppna LinkedIn Campaign Manager**

Gå till https://www.linkedin.com/campaignmanager. Välj Shoreline TechStudios företagskonto (om du inte har det: skapa ett).

**2. Skapa ny kampanj**

Klicka "Create campaign". Välj campaign group "A/B-test Uppgift 2" (eller något du känner igen).

**3. Objective**

Välj "Website visits" som mål. Det är det billigaste och matchar vad vi mäter.

**4. Målgrupp**

Välj följande:
- Location: Sweden
- Language: Swedish
- Company size: 1-10 employees, 11-50 employees
- Job seniority: Owner, Founder, CEO, Partner
- Job function: Business Development, Entrepreneurship, Marketing (bocka i alla tre)

Detta ger dig cirka 50 000 till 100 000 målpersoner. Kall målgrupp, riktade småföretagare.

**5. Ad format**

Välj "Single image ad" (enklast och billigast).

**6. Budget och schema**

- Daily budget: 100 kr
- Schedule: Start now, end 24 hours later
- Total spend cap: 200 kr (så du inte råkar spendera mer)
- Bid strategy: "Maximum delivery" (LinkedIn optimerar automatiskt)

**7. Skapa annonsen**

- Introductory text (huvudtexten):

```
Vad är enklare att förstå på en företagswebbplats?

"Vi bygger tillväxtmotorn" eller "Anställ en digital medarbetare"?

Vi testar och behöver din input.
```

- Bild: Använd en enkel Shoreline-branded bild. Om du inte har en, ta en screenshot av hero-sektionen på Shoreline och redigera lite. Behöver vara 1200×627 px.

- Destination URL: `https://test.shorelinetechstudio.se/?utm_source=linkedin&utm_medium=paid&utm_campaign=abtest`

- Call-to-action button: "Learn More"

**8. Launch**

Klicka Launch. Godkännande av LinkedIn tar 30 minuter till 4 timmar. Sedan börjar den visas.

### Förväntad avkastning

- 100 till 200 kr budget under 24 timmar
- CPM (kostnad per 1000 visningar) i Sverige: cirka 60 till 120 kr
- Impressions: 1 000 till 3 000
- CTR (klickfrekvens på ads): 0,5 till 1 procent
- Klick till splittern: 10 till 30
- Fördelas 50/50 mellan A och B: 5 till 15 per variant

Kombinerat med det organiska inlägget (som kan ge ytterligare 30 till 100 klick): totalt 40 till 150 besökare fördelade på båda varianterna. Tillräckligt för uppgiften.

## Att kommunicera i redovisningen

Detta är styrkan i ditt setup:
- Splitter-URL: besökaren visste inte vilken variant hen skulle se
- Betald cold traffic från LinkedIn Ads: målgruppen är helt främmande för dig personligen
- Organisk trafik som secondary datapunkt: mätning från ditt egna nätverk

I talarnoterna nämner du att paid-siffrorna är mest tillförlitliga, organic-siffrorna kan ha selection bias, men båda pekar (förhoppningsvis) åt samma håll.

Det är MVG-nivå på metod-medvetenhet.
