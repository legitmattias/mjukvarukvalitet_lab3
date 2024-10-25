# Reflektioner kring Clean Code och utveckling av RepoDocster-appen och uppdateringar i mddoc-toolkit

## Introduktion

Utvecklingen av **RepoDocster** har varit en intressant och lärorik, om än bitvis lite väl stressig, resa där jag fått tillämpa och reflektera över principer inom objektorienterad programmering (OOP), och  *Clean Code* av Robert C. Martin. Syftet har varit att skapa en skalbar, underhållbar och funktionell applikation för att hantera GitHub-dokumentation på ett effektivt sätt. Under projektets gång har jag fått en djupare förståelse för vikten av att skriva tydlig och bra kod, och inte bara "fungerande" kod, och i allmänhet hur designprinciper kan underlätta framtida vidareutveckling. Jag valde även för App-delen att använda TypeScript för att få en bättre struktur och typning i koden, och för att lära mig mer om språket. Stark typning har varit en stor fördel för att undvika buggar och för att göra koden mer lättförståelig, men det har också varit utmanande då jag använde en linter som var väldigt strikt.

---

### Huvuddelar av implementationen

#### 1. **Inkapsling och Serviceklasser**

För att följa principen om inkapsling (encapsulation) har jag arbetat med att isolera ansvarsområden i klasser och servicekomponenter. Ett exempel är skapandet av `GithubService` som hanterar interaktionen med GitHub API och avlägsnar denna logik från kontrollernivån. Detta gör koden mindre beroende av varandra och minskar risken för att ändringar i en del påverkar andra delar av applikationen. På samma sätt har jag i den mån det har varit praktiskt görbart och tidsmässigt möjligt försökt att isolera olika delar av applikationen i separata klasser för att underlätta underhåll och vidareutveckling.

#### 2. **Centraliserad konfiguration**

Ett stort fokus har legat på att undvika hårdkodade värden och magiska strängar. Genom att använda både en `BackendConfig`-klass och en `BackendConfig`-klass centraliserade jag konfigurationselement som API-URL:er och GitHub-tokens odyl, vilket förutom att minska beroendet från flera moduler till en .env-fil eller liknande, även delvis minskar kodupprepning och gör systemet lättare att uppdatera. Detta steg blev tydligt en fördel för läsbarheten och enkelheten, men också ett sätt att följa DRY-principen och göra koden mer flexibel.

#### 3. **Error Handling och HttpError-klassen**

För att säkerställa robust felhantering skapade jag `HttpError`-klassen som möjliggör specifika HTTP-fel i både backend och frontend. Istället för att överbelasta controller-logiken med try-catch-block kunde jag delegera hantering av fel till den här klassen och en centraliserad felhanteringsmiddleware. Resultatet blev en mer konsekvent och överskådlig lösning för felhantering, särskilt användbart vid API-kommunikation.

#### 4. **Integrering och uppdatering av mddoc-toolkit**

Projektets kärnfunktionalitet bygger på biblioteket `mddoc-toolkit`, som jag också vidareutvecklade parallellt. Jag har främst lagt tid på att vidareutveckla dess grundfunktionalitet i form av en mer användbar och flexibel markdown-parser, och att integrera den i RepoDocster. Jag vet att fokus skulle bara att följa Clean code i så stor utsträckning som möjligt, och jag är fullt medveten om att det finns mycket mer att göra för att förbättra koden när det kommer till att bryta ut ytterligare delar i separata klasser och metoder, men jag har försökt att hålla en balans mellan att följa principerna och att inte överkomplifiera koden. Dessutom känner jag att jag la mer tid än vad som egentligen fanns tillgängligt under L2 och därför redan hade en bra grund att stå på. I övrigt har jag försökt lägga lite tid på att förbättra dokumentationen och utveckla enhetstester för att säkerställa att koden är robust och att den fungerar som den ska.

---

### Reflektioner över Clean Code, kapitel 2–11

#### Kapitel 2: Meningsfulla namn
Under utvecklingen har jag lagt vikt vid att använda namn som tydligt beskriver funktionaliteten. Exempelvis valde jag att namnge metoderna `getGithubDocument`, `getProcessorInstance`, och `LoadingErrorDisplay` för att tydligt visa vad de ansvarar för. Tydliga namn minskar behovet av kommentarer och gör koden mer självdokumenterande. 

```typescript
const LoadingErrorDisplay: React.FC<LoadingErrorDisplayProps> = ({ loading, error }) => (
  <div className="loading-error-display">
    {loading && <p>Loading...</p>}
    {error && <p style={{ color: 'red' }}>{error}</p>}
  </div>
)
```

Detta kapitel har varit avgörande för att undvika tvetydiga namn och minimera behovet av kommentarer, vilket resulterar i mer läsbar och intuitiv kod.

#### Kapitel 3: Funktioner
Kapitel 3 uppmuntrar till korta, fokuserade funktioner. Jag har följt denna princip genom att bryta ner stora funktioner i små, fokuserade metoder. Ett exempel är `asyncHandler`-metoden som hanterar asynkrona route handlers och fångar fel för att skicka dem vidare till `next()`. Genom att bryta ut den logiken och skapa en wrapper blir koden mer lättförståelig och underlättar felhanteringen.

```typescript
  private asyncHandler(handler: (req: Request, res: Response, next: NextFunction) => Promise<void>) {
    return (req: Request, res: Response, next: NextFunction) => {
      handler(req, res, next).catch(next)
    }
  }
```

Att skriva korta funktioner minskar komplexiteten och gör att koden blir mer lättförståelig, vilket överensstämmer väl med principen om "Single Responsibility".

#### Kapitel 4: Kommentarer
Jag har bara delvis följt rådet i kapitel 4 att minimera kommentarer. Istället för kommentarer har jag använt meningsfulla namn och tydliga metoder för att göra koden självdokumenterande. Men jag har genomgående använt jsdocs, för att på så vis kunna enkelt söka i kodbasen, nyttja anpassade verktyg kopplade till dokumentation och framförallt kunna generera bra och korrekt dokumentation utifrån jsdocs:en. Däremot har jag försökt minska ner antalet inline-kommentarer och låta koden, dvs namn och formattering, tala för sig. Genom att strukturera kod med tydliga metoder och klasser blev behovet av kommentarer mycket mindre, vilket resulterar i renare kod.

Det här exemplet illustrerar hur jag använder inline-kommentarer för att förklara de delar av koden som inte är uppenbara, men annars låter koden tala för sig själv.

```typescript
protected getSectionsWithTemplate(
    sectionType: string,
    errorMessage: string
  ): { title: string; body: string }[] {
    const sections = this.getSectionsByKeywordsInDictionary(sectionType)

    // If no sections match, return an error message as a single array item.
    if (sections.length === 0) {
      return [
        {
          title: `${sectionType.charAt(0).toUpperCase() + sectionType.slice(1)} Not Found`,
          body: errorMessage,
        },
      ]
    }

    // Format each matching section.
    return sections.map((section) => ({
      title: section.heading,
      body: this.formatText(section.body),
    }))
  }
  ```

#### Kapitel 5: Formatering
Att hålla konsekvent formatering är avgörande för att göra koden mer lättläst. Jag har försökt dela upp metoder och skapa avdelningar på naturliga plater mellan kodblock. Formatmässigt har jag följt ett strukturerat mönster i varje fil, vilket tydligt skiljer olika funktionaliteter åt. Jag har däremot inte haft en generell formatteringsguide, vilket kan vara en förbättringsområde för att ytterligare förbättra konsistensen i koden. Jag har istället försökt fokusera på att koden ska vara sammanhängande och lätt att läsa.
Som exempel har jag delat upp MarkdownParser i olika avsnitt för vilken logik de hanterar, vilket gör det enklare att navigera i koden.

```typescript
// MAIN PARSING LOGIC
Olika metoder för klassens grundläggande funktionalitet.
// CONTEXT RELATED HELPER METHODS
Metoder för att hantera kontextberoende logik.
// DICTIONARY PUBLIC METHODS
Metoder för att hämta och manipulera ordlistan.
// GENERAL PUBLIC METHODS
Metoder för att hantera generell funktionalitet, inlusive de metoder som ärvs av kontext-klasserna.
```

#### Kapitel 6: Objekt och Datastrukturer
I projektet har jag aktivt använt objekt för att representera olika typer av markdown-dokument och deras specifika sektioner. Exempelvis används `Section`-objekt för att representera varje del av markdown-filerna, vilket gör det lätt att arbeta med och utöka dokumentens struktur. Detta tillvägagångssätt säkerställer en mer flexibel och tydlig struktur, även om det ibland komplicerar kodningen något.
  
  ```typescript
  export interface Section {
    heading: string;
    body: string;
  }
  ```

#### Kapitel 7: Felhantering
Felhantering har haft hög prioritet och jag har använt custom errors och centrala try-catch-block för att hantera olika fel på ett konsekvent sätt. `HttpError`-klassen möjliggjorde en enhetlig hantering av fel i controller-logiken. Denna strategi gör att kodstrukturen blir renare och att all felhantering sker konsekvent.

```typescript
throw new HttpError("Installation instructions not found", 404);
```

#### Kapitel 8: Gränssnitt
Att skapa tydliga gränssnitt för interaktion med API:et var en central del i designen. Genom att skapa metoder som `fetchGithubDocument` kunde jag hantera API-anrop utan att avslöja interna detaljer. Detta gör att gränssnitten är enkla att förstå och hantera och följer Dependency Inversion Principle (DIP).

```typescript
async fetchGithubDocument(repo: string, path: string): Promise<string> {
  const url = `${this.baseUrl}/${repo}/contents/${path}`;
  const response = await fetch(url, {
    headers: {
      Authorization: `token ${this.token}`,
    },
  });
  const data = await response.json();
  return atob(data.content);
}
```

#### Kapitel 9: Enhetstester
Jag har lagt stor vikt vid att skapa enhetstester för samtliga klasser i mddoc-toolkit. Jag har försökt se till att testa olika användningsfall och edge cases för att säkerställa att att modulen fungerar bra även vid refaktoreringar. Enhetstesterna bidrar till att upprätthålla kodens kvalitet och stabilitet. Det är också mycket enklare att göra förändringar i koden när man vet att man snabbt kan verifiera att inget har gått sönder. När det kommer till applikationen har jag istället valt att fokusera på att skapa integrationstester för att testa hela flödet från användarens perspektiv.

```typescript
test("should extract installation instructions", () => {
  const processor = new RepoReadmeProcessor(mockMarkdown);
  const result = processor.installationInstructions();
  expect(result).toContain("Installation instructions content");
});
```

#### Kapitel 10: Klasser
En av de viktigaste lärdomarna från kapitlet om klasser var att undvika klasser som gör för mycket. Genom att dela upp funktioner i `GithubService`, `GithubController`, `RepoReadmeProcessor`, och andra, kunde jag säkerställa att varje klass hade ett enda ansvar. Detta minskar komplexiteten och gör koden mer modulär. Men här hade jag gjort mer om jag känt att tiden funnits för det, men jag tycker att jag lyckats ganska bra i de flesta fall.
  
  ```typescript
  class GithubService {
    async fetchGithubDocument(repo: string, path: string): Promise<string> {
      // Implementation
    }
  }
  ```

#### Kapitel 11: System
Designen har utformats så att processorklasserna kan utökas med nya funktioner utan att påverka huvudkoden. Det har gjort att systemet är öppet för framtida utvidgningar och visar vikten av flexibel systemdesign. Jag lärde mig att utforma systemet på ett sätt som minimerar påverkan av nya funktioner på befintlig kod, vilket överensstämmer med Open/Closed-principen.

```typescript
class ChangelogProcessor extends MarkdownParser {
  // Implementation
}
```

---

## Slutsats

Sammanfattningsvis har arbetet med RepoDocster och uppdateringarna i mddoc-toolkit varit en process där jag tagit till mig mycket om objektorienterad design och framförallt vikten av tydlig och genomtänkt kod. Genom att konsekvent tillämpa SOLID-principerna och följa riktlinjer från *Clean Code* har jag skapat en applikation som förhoppningsvis fungerar (bra), men också är robust och hyfsat lätt att underhålla. Jag inser också att det alltid finns förbättringsmöjligheter, och att balansen mellan enkelhet och komplexitet är en konstant utmaning. Jag har inte haft brist på ideér på hur jag skulle kunna vidareutveckla både RepoDocster och mddoc-toolkit, och det har varit svårt att begränsa mig till det som var nödvändigt för att uppfylla kraven för kursen och det fokus som var tänkt. Jag har i det här projektet för första gången publicerat ett npm-paket, vilket var kul och lärorikt. Det är tydligt att det är först när man gör saker själv som man förstår hur sker hänger ihop och fungerar.