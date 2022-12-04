---
Title: Load
Description: Load
Template: analysis-single
---


Load
=======================

I denna rapport analyseras tre webbplatsers laddningstid och användbarhet, samt potentiella förbättringsområden.

Urval
-----------------------

Jag har valt att fortsätta analysera samma tre webbplatser som förra veckan:  

- https://www.scandinavianexecutive.se erbjuder interimschefer inom HR, ekonomi/finans, marknad/försäljning, industri/produktion, sourcing/supply chain, offentlig sektor, IT. Förutom "huvudsidan" har jag genomfört mätningar på https://www.scandinavianexecutive.se/om-oss/ och https://www.scandinavianexecutive.se/utbud/ .
- https://www.gazella.se är specialiserade på interimlösningar och rekrytering inom ekonomi, allt från ekonomichef till ekonomiassistent. Förutom huvudsidan har jag även genomfört mätningar på https://www.gazella.se/om-gazella/ och https://www.gazella.se/anlita-oss/rekrytering/.
- https://meshab.se/ erbjuder såväl interimschefer som konsulter inom HR, ekonomi, marknad, försäljning, IT, inköp. Förutom huvudsidan har jag även genomfört mätningar på https://meshab.se/om-mesh/ och https://meshab.se/anlita-interimskonsult/ .

Det är tre webbplatser som är lagom bildtunga och där primärsyftet med bilderna är att förmedla en känsla snarare än att sälja innehållet i bilderna (till skillnad mot exempelvis en webshop).


*Tips! Hovra över rutan för respektive webbplats för att zooma eller klicka för att öppna bilden i originalstorlek*

<div class="foto-container">
<div class="image-cell scandinavian">
<div class="title-cell"><h3>Scandinavian Executive</h3></div>
<div class="screen1">
<a href="../image/Scand-Exec-1.jpg"><img src="../image/Scand-Exec-1.jpg?q=40" alt="website screenshot"></a>
</div>
</div>
<div class="image-cell gazella">
<div class="title-cell"><h3>Gazella</h3></div>
<div class="screen1">
<a href="../image/gazella-1.jpg"><img src="../image/gazella-1.jpg?q=40" alt="website screenshot"></a>
</div>
</div>
<div class="image-cell mesh">
<div class="title-cell"><h3>Mesh</h3></div>
<div class="screen1">
<a href="../image/mesh-1.jpg"><img src="../image/mesh-1.jpg?q=40" alt="website screenshot"></a>
</div>
</div>
</div>


Metod
-----------------------

Jag började med att testa var och en av de tre utvalda sidorna per webbplats (dvs totalt 9 sidor) i https://pagespeed.web.dev/ .
Jag utförde testet 3 ggr för såväl mobil som desktop och antecknade prestanda poängen samt vilka tips på förbättringar som verktyget genererade.

Därefter undersökte jag respektive sida i Firefox Developer edition devtools. Jag började med att titta på totalt antal begäran, total storlek för sidan och sidans laddningstid. Mellan varje kontroll laddade jag om sidan Ctrl + Shift + R. Jag valde att också göra motsvarande kontroller för enbart bilder och därefter enbart javascript för att analysera deras storlek och laddningstid i förhållande till den totala (dvs totalt antal sidomladdningar 9 x 3 för respektive webbplats). Under mätningen såg jag till att scrolla igenom hela webbsidan för att i beräkningarna även få med filer som laddar in med lazyload (dvs att dessa laddar först när man scrollat fram till de).

Resultat
-----------------------

Studien ledde till följande observationer:

<div class="scroll-container">
<iframe width=100% height=600px src="https://docs.google.com/spreadsheets/d/e/2PACX-1vTx1MK-g1zmT6pprXEb60PCej7BKveJ7PysDbg9POtk-DRWpfji2vUg66Jb2hDZI04nzDtj8t_ok8Qg/pubhtml?gid=0&amp;single=true&amp;widget=true&amp;headers=false"></iframe>
</div>




Analys
-----------------------

Från början hade jag tänkt utföra testet för respektive sida genom att endast ladda om sidan och skriva ner värdena, men upptäckte snart att samtliga webbplatserna använde sig av lazyload vilket innebär att innehåll laddas in först när den blir nödvändig och att den initiella laddningstiden då ändrades i efterhand som man scrollade ner på sidan, vilket innebar att jag fick anpassa min metod något för att få med laddningstiden för hela sidan och inte enbart det som är "above the fold" (dvs den delen som man ser först när man besöker webbplatsen).  

I början utgick jag ifrån att mätningen var totaltiden för respektive förfrågan till att resursen laddats in (eftersom det var så jag tolkade devtools dokumentationen), men det kändes inte som att så var fallet eftersom det kunde bli en rejäl skillnad i laddningstid beroende på om jag scrollade ner direkt eller avvaktade en liten stund innan jag började scrolla. Det kan ha varit en tillfällighet, men för att minimera den person-beroende effekten på mätningen försökte jag att scrolla hela vägen ner så snabbt som möjligt för att eventuella förfrågningar skulle gå iväg på en gång. 

### Prestanda i PageSpeed Insights

När det kommer till prestanda mätningen i PageSpeed Insights verktyget så vann Scandinavian Executives som fick ett genomsnittligt poäng av 88 på mobil och 98 på desktop. Tvåa kom Gazella med genomsnittligt poäng 50 på mobil och 84 på desktop. Och sist kom Mesh med ett genomsnitt av 28 poäng på mobil och 68 på desktop.  

De mest återkommande rekommendationerna i PageSpeed Insights (gemensamma för samtliga tre webbplatser) relaterade till laddningstid och användbarhet var:  

- Skicka bilder i modernare format (WebP och AVIF)
- Ta bort resurser som blockerar renderingen (infoga js/CSS kod inline och skjut upp inläsning av mindre viktig javascript/css)
- Reducera javascript som inte används och skjut upp inläsningen av script tills den är nödvändig 
- Reducera CSS som inte används från formatmallar samt skjut upp CSS som inte används för innehåll som är above the fold (dvs syns först)
- Minska arbetsbelastningen i huvudtråden (dvs minska tiden det tar att kompilera/tolka och köra javascript)
- Undvik att kedjekoppla kritiska förfrågningar, minska storleken på resurser som laddas ner eller skjut upp nedladdning av onödiga resurser
- Begränsa antal begäran och storleken på överföringar (med hjälp av en budget.json-fil som innehåller budget för kvantitet och storlek på sidresurser)
- Undvik uppgifter som körs i huvudtråden under lång tid
- Undvik större layout-förskjutningar
- Sätt width och height på bilder för att undvika störra layout förskjutningar  
  
    

Några av de mindre vanliga rekommendationerna (föreslagits för en eller två av de undersökta webbplatserna):

- Koda bilder effektivt (optimerade bilder läses in snabbare och förbrukar mindre mobildata)
- Använd bilder med rätt storlek
- Möjliggör textkompression (med gzip, delate eller brotli)
- Skjut upp inläsningen av bilder som är utanför skärmen eller dolda (lazy-loading) 
- Minska serverns första svarstid (påverkans av teman, plugins och serverns prestanda)
- Undvik att skicka äldre Javascript-koder till moderna webbläsare
- Skicka med en effektiv cachelagringspolicy - om filerna cashlagras under längre tid kan upprepade besök på sidan gå snabbare
- Undvik hög nätverksbelastning genom att exempelvis dela upp innehåll på flera sidor
- Undvik document.write() eftersom det kan fördröja sidinläsningen rejält för användare med långsam anslutning
- Använd passiva eventlyssnare för tryck och hjul för att förbättra sidans scroll-funktion



### Mätningar hel sida i dev tools

Intressant nog så visade devtools mätningarna kortast laddningstid för just Mesh (genomsnitt 2.6s för hel sida, jämfört med Gazella som hade 12.1s och Scandianvian Exectuive som hade 5.7s). Storleksmässigt låg Scandinavian Executive och Mesh på ca 5.5 MB i genomsnitt för hel sida, medan Gazella visade ett genomsnittligt innehåll på 12.1 MB. 

### Mätningar bilder i dev tools

När jag sedan tittar på bilder så utgör dessa hos Scandinavian Executives i genomsnitt ca 24% av totalt antal begäran men endast 9% av total storlek. Om vi tittar på genomsnittlig storlek per bild blir det 0.02 MB per bild, vilket är riktigt bra. Bilderna är främst i format webp, svg och gif, men även några png. Om vi tittar på bilderna rent visuellt så upplever jag att (på desktop) ser bilderna på Scandinavian Executives sida rätt så pixliga ut, även utan inzoomning. Jag hade gärna sett bilder i bättre kvalité på desktop eftersom det inte är lika stort behov av att spara data som på mobil enhet (de flesta har bredband). Besparingen har i detta fall synbart påverkat kvalitén. 

 Hos Gazella utgör bilder i genomsnitt ca 35% av total antal begäran och 42% av total storlek, per bild blir den genomsnittliga storleken 0.12 MB, vilket är sex gånger så mycket jämfört med storleken hos Scandiavian Executives. Gazella använder sig av några svg bilder till ikoner, men i övrigt är det många jpeg, png samt några gif. När jag tittar på bilderna upplever jag kvalitén som ok (bilderna blir pixliga först när man börjar zooma in).
 
 För Mesh är motsvarande siffror 31% av totalt antal och 46% av total storlek, respektive 0.07 MB/bild. Sett till genomsnitt på storlek placerar sig alltså Mesh tvåa. Merparten av bilderna på Meshs webbplats är webp och gif format, men även några svg, png och jpeg syns till. På Meshs sida upplever jag bilderna som bra kvalité - vissa av de mindre bilderna är något pixliga, men de de flesta upplever jag som tydliga, även vid inzoomning. Mesh har i mitt tycke hittat en bra balans här mellan besparing och presenation.

### Mätningar javascript i dev tools

I genomsnitt utgjorde Javascript på Scandinavian Exectuives sidan ca 51% av totala antalet begäran och 58% av sidans totala storlek. Per begäran var storleken i genomsnitt 0.07MB.

Hos Gazella utgjorde Javascript ca 35% av totalt antal begäran från sidan samt ca 45% av sidans totala storlek. Per begäran av storleken 0.12MB.

För Mesh var motsvarande siffror 50.45% av sidans totala antal begäran och 21.86% av sidans totala storlek, motsvarande 0.02 MB/begäran. 

### Sammanfattningsvis

Det är svårt att säga en exakt laddningstid som jag tycker är rimlig. Helst vill jag såklart att när jag kommer in på en webbsida så ska jag kunna se allt direkt på den delen som syns i viewport, med undantag för eventuella annonser. Jag skulle dock inte tycka att det var jobbigt om det dröjer att ladda in bilder som inte har något primärt syfte. Är det däremot primärt innehåll som knappar och menyer (eller bilder på vara i webshop) så ska det helst inte dröja mer än 1-2 sekunder. 

Jag tycker att samtliga tre sidorna har en bra strategi med att använda lazyload som gör så att resurser laddas in allteftersom de behövs. Då allokeras nätverksresurser dit de behövs i första hand och på så sätt ge intryck av att sidan laddar snabbare (för mig som användare spelar det ju ingen roll om något jag inte direkt ser har laddats in eller inte). 

Baserat på de mätningar jag gjorde i dev tools kommer Mesh 1a när det kommer till genomsnittlig laddningstid per sida, följt av Scandianvian Executive och sist Gazella. Detta är inte i linje med PageSpeed Insights mätningen där Scnadianvian Exectuives kom etta, följt av Gazella och Mesh kom sist. Dock tittar verktyget på fler mått och inte enbart totaltid tills samtliga resurser laddats - exempelvis tittar vektyget på tid till när första innehållet blir synligt, tid till när merparten av innehållet upplevs som synligt, cumulative layout shift (när layout plötsligt ändras, tex när en bild utan bestämda mått/placeholder laddas in och flyttar om annat innehåll), tiden till interaktivt tillstånd mm. 

Om man tittar specifikt på bilder så har Scandianvian Executives lyckats spara in mest data men jag tycker nog ändå att Mesh ska få första platsen eftersom de varit mest effektiva, de har sparat in en del data åt användarna men inte mer än att de ändå behåller bra kvalité på bilderna.  

När det kommer till javascript utgör antal begäran lite mer än hälften av sidans totala antal hos både Scandianvian Executives och hos Mesh, medan hos Gazella är motsvarande siffra 35%. Per begäran ligger dock Mesh bäst med 0.02MB/begäran (jämfört med 0.07MB/begäran för Scandinavian Exectuives och 0.12MB/begäran för Gazella) vilket tyder på att de skickar många små filer. Det är dock svårt att bedöma en vinnare i denna kategori utan att veta exakt vad javascripten gör på respektive sida/hur pass avancerad den är och om koden hade kunnat skrivas om kortare eller inte.













### Mesh 




Referenser
-----------------------




Övrigt
-----------------------

Mitt namn är Julia Lind, och jag har gjort denna undersökning/skrivit rapporten ensam.