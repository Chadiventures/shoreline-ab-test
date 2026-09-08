# A/B-test setup för Uppgift 2

Två landningssidor plus deploy-instruktioner för Coolify plus mätning i Google Analytics 4.

## Filerna

```
shoreline-ab-test/
  variant-a/
    index.html   ← Kontroll: "Vi bygger tillväxtmotorn..."
    Dockerfile
  variant-b/
    index.html   ← Test: "Anställ din digitala medarbetare"
    Dockerfile
```

## Steg 1: Sätt in din GA4 measurement ID

Öppna båda index.html-filerna och byt ut `G-XXXXXXXXXX` (finns på tre ställen per fil) mot din riktiga GA4 measurement ID från shorelinetechstudio.se. Du hittar den i Google Analytics under Admin → Data Streams → Web.

Sedan i GA4: gå in i Admin → Custom definitions → Create custom dimension. Skapa en dimension som heter "variant" med scope "Event". Detta gör att du kan filtrera trafik och klick per variant senare.

## Steg 2: Deploya till Coolify som två subdomains

Här är det enklaste flödet:

**I Coolify:**

1. Skapa en ny resurs för varje variant (två stycken totalt). Välj "New Resource" → "Docker Image" eller "Dockerfile".

2. Peka den mot ditt Git-repo där du pushat variant-a/ respektive variant-b/. Eller om du inte vill använda Git: välj "Deploy Docker Compose" och klistra in Dockerfilen som byggkontext.

3. För variant A: sätt domain till `a.shorelinetechstudio.se`. För variant B: `b.shorelinetechstudio.se`.

4. Sätt exposed port till 80 i båda.

5. Coolify sätter upp SSL automatiskt via Let's Encrypt.

**I din DNS (Cloudflare troligen):**

Lägg till två A-records som pekar på Coolify-serverns IP:
- `a` → din Coolify-servers IP
- `b` → din Coolify-servers IP

Vänta 2 till 5 minuter för DNS-propagering, sedan är sidorna live på:
- `https://a.shorelinetechstudio.se`
- `https://b.shorelinetechstudio.se`

## Steg 3: Splitta trafik och samla klasstrafiken

För uppgift 2 räcker det med manuell 50/50-split. Här är två sätt:

**Metod 1: Två separata inlägg**

Posta variant A-länken i klass-Slack, LinkedIn eller kursens forum. Posta variant B-länken på ett annat ställe (till exempel din Instagram Stories eller mail till halva klasslistan). Håll trafiken separerad så metoden är ärlig.

**Metod 2: Random splitter**

Om du vill bara dela en länk och slumpmässigt splitta: skapa en enkel splitter-sida på `test.shorelinetechstudio.se` som redirectar 50/50:

```html
<!doctype html>
<script>
  const variant = Math.random() < 0.5 ? 'a' : 'b';
  location.replace(`https://${variant}.shorelinetechstudio.se/?src=split`);
</script>
```

Dela bara den länken till alla, så delas de slumpmässigt.

## Steg 4: Mätning i Google Analytics 4

Efter 24 till 48 timmars trafik, öppna GA4 → Reports → Engagement → Events.

**Vad du tittar på:**

1. **Sidvisningar per variant.** Reports → Pages and screens. Se hur många som besökt varje sida (variant A vs variant B).

2. **CTA-klick per variant.** Filter på event "cta_click". Skapa en jämförelse med "variant" som dimension. Du får två siffror, en per variant.

3. **CTR (Click-Through-Rate).** Räkna själv: `cta_click / sidvisningar` per variant. Det är din huvudsiffra.

4. **Statistisk signifikans.** Använd en gratis A/B-signifikans-kalkylator som `abtestguide.com/calc/`. Mata in:
   - Variant A: antal besökare, antal klick
   - Variant B: antal besökare, antal klick
   
   Den räknar ut om skillnaden är signifikant (över 95 procent är gyllene, över 90 procent räknas för uppgiften).

## Steg 5: Uppdatera slide 8 med riktiga siffror

När du har data:

Öppna Canva-designen: https://www.canva.com/d/4lIUl_t5fy3NbQM
Klicka in på slide 8 (Resultat & Slutsats).

Uppdatera texten under "SIFFRORNA" med de riktiga siffrorna:
```
Variant A (kontroll):   CTR X,X procent   ·   XXX besökare
Variant B (test):          CTR X,X procent   ·   XXX besökare
Relativ lyft:                   ±XX procent
Statistisk signifikans:  XX procent
```

Uppdatera också rubriken högst upp beroende på utfall:
- Om B vinner: "Variant B vann med +XX procent CTR"
- Om A vinner: "Kontrollen vann. Hypotesen förkastad."
- Om lika: "Ingen signifikant skillnad efter 14 dagar"

Ärlighet i redovisningen är faktiskt bra: läraren ser att du utvärderat metodiskt och inte bara hittat på resultat.

## Bonus: Alternativ snabbare-än-Coolify-metod

Om du vill spara tid: pusha `variant-a/index.html` som en enda fil till Netlify Drop (https://app.netlify.com/drop), sedan `variant-b/index.html` samma sätt. Får två unika URL:er på under 2 minuter, utan Coolify. Sämre för branding (netlify-URL) men snabbare.

Mätning fungerar identiskt, GA4 spårar oavsett var sidan ligger.
