---
Title: About
Description: Documentation about methods used in creating this website.
---

Om
==========================

## Grundstruktur

Innehållet på denna sida är uppbyggt med hjälp av Pico ramverk.
Stylingen är skapad via CSS preprocessor SASS där bla variabler och mixins har använts för att skapa CSS strukturer. SASS koden är uppdelad över moduler efter syfte.

## Typografi

Det är tre olika fonts som används på denna sida, en serif-font för h1 elementet i title "Palyfair Display SC 400", en serif font för rubrik-element i main "Playfair Display 400" samt en sans serif font för p, respektive a element "Montserrat". P elementet har vikt 300 på skärmvidd laptop och lägre och vikt 400 på skärm 1600px bredd och högre. Länkar har vikt 400. För att hitta fonter som matchar har jag använt mig av online-verktyget https://fontjoy.com .  


Font-size är satt i den relativa enheten rem med 'scale faktor' 1.414 (Augmented Fourth) mellan p, h2 och h1 i main-elementet; lineheight är 1.5. Vid större skärm än laptop har även p elementet font-weight 400. På mindre skärm (tex mobiltelefon) är scale factor för p, h2 och h1 i main istället 1.333 (Perfect Fourth). Det är rekommenderat att ha 1-2 viktklasser mellan p element och rubrik element, men fonten Playfair Display ser i sig fetare ut även i normalvikt, och därför har jag valt att ha även den i 400.

Fonten Montserrat är nerladdad i ttf format från google fonts och hämtas in lokalt, men importeras även via fonts.googleapis.com i woff format. De övriga fonterna är än så länge endast importerade från google eftersom jag ännu inte beslutat om jag ska behålla dessa eller ändra. För fontloading används FOUT metoden - att en fallback font visas tills den "riktiga" fonten är laddad.  

Text-alignment för p-elementet i main är justify ner till skärmvidd motsvarande skärmstorlek av mobiltelefon i liggande läge, där det ändras till left för att undvika stora mellanrum som kan bildas med justify vid smal kolumnbredd.  

## Responsivitet

Eftersom jag främst arbetar på laptop är webbsidan skapad i utgångspunkt i laptop och därefter anpassad till såväl större (min-width 1600px) som mindre skärmstorlekar (mobiltelefon/surfplatta). På mindre skärmar (motsvarande mobiltelefon i liggande läge och mindre) tar headern upp hela skärmhöjden och det finns en länk/pil som man kan klicka på för att scrolla förbi headern ner till main elementet (jag har lagt till ett id till main-elementet som länken går till).

## Layout

Index-sidan och Technologies sidorna är skapade med CSS grid. På me sidan överlappar bild-element med text-element inom samma grid-celler för att ge intryck av bild-bakgrund. Jag har använt mig av denna teknik istället för att lägga bakgrundsbild för att kunna lägga till bildbeskrivning 'alt'.  

Text-innehållet på index-sidan ligger uppdelad i tre separata divar. På skärmar större än 767px ligger divarna i en tre kolumn-layout och bilden är inlagd separat i repsektive del men med olika positionering gentemot föräldra-diven för att ge intryck av olika bilder i samma bildserie. Det är en mörk bild men med ganska låg opacitetsfaktor som ändå gör så att texten syns tydligt.  

På skärmar mindre än 767px används istället en annan bild som har genomskinliga ytor för att låta den vita bakgrunden synas igenom för att ge ett luftigare intryck. Bilden läggs här in endast en gång och täcker samtliga celler i griden.

Sidan för respektive Teknologi använder flex-box layout där artikelelementet blir mindre när skärmbredden minskar medan sidebar elementet behåller sin skärmbredd fram tills skärmbredden blir mindre än 767px. Efter det får sidebaren 'display-none' och artikel-elementet får bredden 100%.

