# Webfilter
Ett tillägg för Google Chrome webbläsare
Av
Simon Vernberg
IT-samordnare Hedda Wisingskolan


Beskrivning.
Webfilter är ett Chrome-tillägg utvecklat för användning i skolor och utbildningsverksamheter. Det skapades för att ge IT-administratörer ett pålitligt, transparent och integritetsvänligt verktyg för att begränsa åtkomst till webbplatser som inte är lämpliga eller produktiva under skoltid.
Tillägget är avsett att driftsättas och hanteras av skolans IT-administratör via Google Workspace for Education, med hjälp av Chrome Browser Cloud Management eller liknande MDM/EMM-lösningar.

Vad gör tillägget.
Webfilter blockerar åtkomst till webbplatser som anses olämpliga eller oproduktiva i skolmiljö. När en användare försöker besöka en blockerad webbplats omdirigeras webbläsarfliken till en inbyggd sida (blocked.html) som medföljer tillägget. Denna sida informerar användaren om att sajten är blockerad av administratören. Ingen extern server kontaktas under denna process, den blockerade sidan levereras helt och hållet från tillägget.
Vad gör inte tillägget.
Tillägget kan inte fjärrstyras eller om konfigureras efter installation. Den använder inga dynamiska regellistor. Det läser inte, ändrar inte och avlyssnar inte webbsidors innehåll. Användaren kan inte konfigurera, inaktivera eller kringgå tillägget. Ingen kan ansluta till eller interagera med tillägget över ett nätverk. Tillägget utför ingen SSL/TLS-inspektion och installerar inga certifikat.
Hur Fungerar tillägget.
Webfilter bygger på Chromes inbyggda declarativeNetRequest API. Alla blockeringsregler lagras som statiska JSON-filer som paketeras direkt i tillägget och används lokalt på enheten. Det sker inga anrop till externa servrar, API:er eller molntjänster. 
Regellistan kan bara uppdateras genom att publicera en ny version av tillägget via Chrome Web Store och distribuera den via Google Workspace for Education, med hjälp av Chrome Browser Cloud Management eller liknande MDM/EMM-lösningar. Det finns ingen mekanism för fjärruppdatering, inget push-system och inget sätt att ändra tilläggets beteende utan att installera ett nytt paket eller ny version av tillägget.





Data och integritet.
Webfilter lagrar, överför eller analyserar inte några uppgifter om användare eller deras surfaktivitet. Tillägget innehåller inga spårningsfunktioner, analysverktyg, telemetri eller rapporteringsfunktioner av något slag. Det finns inga tredjepartstjänster, annonsbibliotek eller externa SDK:er inbäddade i tillägget. All regelhantering sker lokalt i webbläsaren.
Webfilter är fullt kompatibelt med dataskyddsregler och integritetslagar:
•	EU:s dataskyddsförordning (GDPR, förordning 2016/679)
o	Art. 4 - Definitioner
o	Art. 5 – Principer för behandling
o	Art. 6 – Laglig grund för behandling
o	Art. 9 – Känsliga personuppgifter
o	Art. 25 – Inbyggt dataskydd och dataskydd som standard
o	Art. 30 – Register över behandlingar
o	Art. 32 – Säkerhet vid behandling
o	Art. 35 - konsekvensbedömning
o	Art. 44-49 – Överföring av uppgifter till tredjeland
•	ePrivacy-direktivet (2002/58/EG)
o	Art. 4 – Säkerhet vid behandling
o	Art. 5 – Konfidentialitet vid kommunikation
o	Art. 9 – Lokaliseringsuppgifter
o	Art. 13 – Otillbörlig kommunikation
o	Art. 14 – Tekniska egenskaper och standard
o	Art. 15 – Undantag och begränsningar
•	NIS2-direktivet (EU 2022/2555)
o	Art. 2 – Tillämpningsområde
o	Art. 6 – Definitioner
o	Art. 20 – Styrning
o	Art. 21 – Riskhanteringsåtgärder
o	Art. 24 – Användning av produkt och tjänster
o	Art. 32-33 – Tillsyn och kontroll
•	Skollagen (2010:800)
o	5kap. 5-7 §§
o	6kap.1-6 §§
o	26a kap.2-6 §§
Licenser och behörigheter
Webfilter är byggt uteslutande på webbplattformsstandarder och öppna API:er. Det innehåller ingen tredjepartskod. Nedan specificeras de öppna licenser vars krav tillägget uppfyller, de exakta Chrome-behörigheter det begär, samt vad Manifest V3 är.
•	MIT License: Den primära licensen för tilläggets egna källkod. 
•	Apache License 2.0: Används i Chromium-projektet och Chrome Extensions-plattformen som tillägget bygger på.
•	W3C Software and Document License: Webbstandarder (HTML, JSON, URL-syntax) som definieras av W3C.
•	Chromes Extensions API (Google LLC): Tillägget använder Chrome publikta dokumenterade Extensions API, som distribueras under Googles egna användarvillkor för Chrome Web Store och Chrome Browser.
Tillägget är inte beroende av externa bibliotek, npm-paket eller CDN-resurser.
Chrome-behörigheter
Tillägget begär exakt tre behörigheter i Manifest V3
•	declarativeNetRequest: Krävs för att registrera statiska blockeringsregler och låta Chromes inbyggda regelmotor omdirigera eller blockera matchade nätverksbegärningar.
•	Storage: Krävs för att läsa administratörskonfigurerad policy från chrome.storage.managed. Används enbart för att hämta listan allowedDomains som en IT-administratör valfritt kan definiera via Google Workspace.
•	host_permissions: <all_urls>: Krävs av declarativeNetRequest API:et för att utvärdera blockeringsregler.


Manifest V3
Webfilter är byggt på Chrome Extensions Manifest V3, det nuvarande manifestformatet för Chrome-tillägg. 
Manifest v3 innebär:
•	Nätverksfiltrering sker via API:et declarativeNetRequest i stället för det äldre webRequest-API:et, vilket innebär att tillägget aldrig läser eller modifierar nätverkstrafik.
•	Bakgrundsprocesser körs som service workers, vilket minskar resursanvändning.
•	Fjärrkod är förbjudet i MV3.
Driftsättning
Webfilter är avsett för driftsättning via verktyg så som Google Workspace for Education (Chrome Browser Cloud Management) samt andra MDM/EMM-lösningar som stöder Chrome-tilläggspolicy.
Administratörer kan valfritt konfigurera en godkänd lista med ytterligare godkända domäner via den hanterade lagringspolicyn allowedDomains. Detta gör det möjligt för enskilda skolor att vitlista specifika utbildningsverktyg eller tjänster utan att en ny tilläggsversion behöver byggas.
