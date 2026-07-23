---
name: recipe-generator
description: Gebruik wanneer iemand recepten op maat wil laten genereren en eerst de dieetwensen, keukenapparatuur, ingrediëntenvoorkeuren en receptformat moet vastleggen. Van toepassing bij het opzetten van een nieuw receptenproject, het aanpassen van bestaande dieetregels, of het toevoegen van nieuwe recepten aan een bestaande verzameling.
---

# Recepten-generator

## Overzicht

Deze skill begeleidt het volledige traject van "ik wil recepten op maat" naar een opgeslagen, kwaliteitsgecontroleerd recept: eerst de vereisten uitvragen, dan een ingrediëntenlijst opstellen en laten aanpassen, en pas daarna recepten genereren volgens een vast format.

**Kernprincipe:** genereer nooit recepten zonder eerst de dieetregels, apparatuur en ingrediëntenlijst te kennen — anders is de kans groot dat het recept niet passend, niet haalbaar of niet lekker is.

## Wanneer gebruiken

- De gebruiker vraagt om een recept, weekmenu of receptenverzameling te genereren.
- Er is nog geen profielbestand (`recept-profiel.md`) in de projectmap — dit is dan een nieuw project.
- De gebruiker wil dieetregels, apparatuur of ingrediëntenlijst wijzigen.
- De gebruiker wil recepten toevoegen aan een bestaande verzameling die al via deze skill is opgezet.

## Werkwijze

### Fase 0 — Bestaand profiel controleren

Zoek naar `recept-profiel.md` in de projectroot.

- **Bestaat het?** Vat de bestaande antwoorden kort samen en vraag of dit nog klopt of moet worden aangepast. Sla Fase 1 over voor de onderdelen die ongewijzigd blijven.
- **Bestaat het niet?** Ga naar Fase 1.

### Fase 1 — Vereisten uitvragen

Stel de gebruiker onderstaande vragen (bijvoorbeeld via de AskUserQuestion-tool, met concrete keuzeopties waar mogelijk). Vraag niet alles in één keer als dat de gebruiker overweldigt — groepeer logisch.

**Verplichte vragen:**

1. **Gezondheids-/dieetdoel** — bv. diabetes type 2, cholesterolverlaging, afvallen, spieropbouw, geen specifiek doel. Dit bepaalt de niet-onderhandelbare voedingsregels (koolhydraten, vet, eiwit, vezels).
2. **Allergieën en intoleranties** — gluten, lactose, noten, schaaldieren, ei, soja, etc.
3. **Dieetstijl** — omnivoor, vegetarisch, veganistisch, flexitarisch, pescotarisch.
4. **Verboden of te vermijden ingrediënten** — expliciet uitvragen, ook als dit al uit doel/allergieën volgt (bv. "geen toegevoegde suiker", "geen witte pasta in grote porties").
5. **Aantal personen** per standaardportie (recepten worden voor dit aantal geschreven; vermenigvuldigen wordt aan de gebruiker overgelaten).
6. **Maaltijdtype(s)** — ontbijt, lunch, diner, tussendoortje. Elk maaltijdtype krijgt een eigen ingrediëntenlijst en eigen receptenmap.
7. **Beschikbare keukenapparatuur** — vraag expliciet naar wat er WEL is (bv. inductie, oven, air fryer, wok) en wat NIET beschikbaar is (bv. magnetron, grillpan, snelkookpan). Neem alleen apparatuur op die de gebruiker bevestigt.
8. **Smaakvoorkeuren** — hartig/zoet/neutraal, favoriete keukens (mediterraan, Aziatisch, Midden-Oosters, etc.), ingrediënten die men juist graag terugziet.
9. **Waar wordt boodschappen gedaan** — welk land/type supermarkt, zodat ingrediënten daadwerkelijk verkrijgbaar zijn.

**Nuttige aanvullende vragen (stel als relevant):**

- Budget: mag een recept een duur ingrediënt bevatten (bv. entrecote, garnalen) of moet het budgetvriendelijk blijven?
- Gewenste bereidingstijd (bv. altijd < 30 min, of geen restrictie)
- Kooknervaring/niveau (beginner vs. gevorderd) — beïnvloedt complexiteit van instructies
- Variatie: recepten mogen niet te vaak dezelfde hoofdingrediënten gebruiken
- Uitvoerformaat: losse markdown-bestanden, één bestand per recept, en/of PDF-export
- Bestandsnaamgeving en mapstructuur, als de gebruiker een voorkeur heeft die afwijkt van het standaardvoorstel hieronder

### Fase 2 — Profiel vastleggen

Leg alle antwoorden vast in `recept-profiel.md` in de projectroot, met secties: Doel/dieetregels, Allergieën, Verboden ingrediënten, Portiegrootte, Maaltijdtypen, Apparatuur, Smaakvoorkeuren, Supermarkt/regio, Overige voorkeuren.

Dit bestand is de bron van waarheid voor alle volgende stappen en toekomstige sessies — lees het altijd opnieuw in plaats van aannames te doen.

### Fase 3 — Ingrediëntenlijst genereren en laten aanpassen

Voor elk maaltijdtype:

1. Stel op basis van het profiel een voorstel-ingrediëntenlijst op, gegroepeerd per categorie (bv. Vlees, Vis, Groenten, Fruit, Granen, Peulvruchten, Zuivel, Noten/Zaden, Kruiden, Oliën/Sauzen). Neem alleen ingrediënten op die passen bij de dieetregels en verkrijgbaar zijn bij de opgegeven supermarkt. Maak de lijst zo compleet mogelijk.
2. Sla de lijst op als `ingredienten-<maaltijdtype>.md` (bv. `ingredienten-diner.md`, `ingredienten-ontbijt.md`) in de projectroot.
2. Vraag de gebruiker expliciet om aanpassingen: items toevoegen, verwijderen of vervangen - of geef de gebruiker de optie om de lijst met hand aan te passen in een teksteditor.
3. Als de gebruiker de lijst niet zelf heeft aangepast, verwerk dan de aanpassingen en sla de definitieve lijst op.
4. Herhaal dit pas bij een expliciet verzoek van de gebruiker om de lijst te herzien — niet bij elk nieuw recept.

### Fase 4 — Recepten genereren

Vraag, tenzij al duidelijk: voor welk maaltijdtype, hoeveel recepten, en of er specifieke wensen zijn (bv. "iets met vis", "gebruik de aardappelen op").

Genereer elk recept volgens dit vaste format:

```markdown
# [Naam van het gerecht]

**[Label 1] | [Label 2] | [Dieetlabel]**

> [Eén of twee zinnen: waarom dit gerecht lekker én passend is bij het dieetdoel.]

---

## Hoeveelheden (voor **N persoon/personen**)

> Vermenigvuldig alle hoeveelheden met het aantal personen.

| Ingrediënt | Hoeveelheid |
|---|---|
| ... | ... |

---

## Kook-instructies

### Voorbereiding (X min)
1. ...

### [Fase 2 naam] (X min)
2. ...

### Serveren
N. ...

---

## Diabetes-tips / Dieet-tips
- [Tip over koolhydraten, vet of glycemische belasting, indien relevant voor het dieetdoel]
- [Tip over portiegrootte of slimme vervanging]
```

Sla elk recept op als `XX-kebab-case-naam.md` in `recepten-<maaltijdtype>/` (oplopend volgnummer, aansluitend op het hoogste bestaande nummer), en voeg het toe aan `recepten-<maaltijdtype>/00-overzicht.md` in de vorm:

```
| XX | [Naam](bestandsnaam.md) | [Hoofdeiwit] | [Dieet info (waarom past het in het dieet)] | [Labels]
```

### Fase 5 — Kwaliteitscheck per recept

Controleer voor het opslaan van elk recept:

- [ ] Alle ingrediënten staan op de vastgestelde ingrediëntenlijst voor dit maaltijdtype
- [ ] Geen verboden ingrediënten (uit het profiel) gebruikt, of alleen binnen de toegestane uitzondering
- [ ] Koolhydraat-/vet-/suikerregels uit het profiel worden gerespecteerd
- [ ] Bereiding past binnen de bevestigde keukenapparatuur — geen apparaat gebruikt dat niet beschikbaar is
- [ ] Ingrediënten zijn verkrijgbaar bij de opgegeven supermarkt/regio
- [ ] Portiegrootte klopt met het profiel
- [ ] Dieet-tips sectie aanwezig en inhoudelijk nuttig
- [ ] Recept toegevoegd aan het juiste `00-overzicht.md`

Als een gewenste smaakcombinatie een ingrediënt vereist dat niet op de lijst staat: vraag de gebruiker of dit ingrediënt mag worden toegevoegd, of kies anders een alternatief van de bestaande lijst.

## Snel overzicht

| Fase | Doel | Output |
|---|---|---|
| 0 | Bestaand profiel checken | — |
| 1 | Vereisten uitvragen | Antwoorden van gebruiker |
| 2 | Profiel vastleggen | `recept-profiel.md` |
| 3 | Ingrediëntenlijst opstellen + laten aanpassen | `ingredienten-<type>.md` |
| 4 | Recepten genereren | `recepten-<type>/XX-naam.md` + overzicht |
| 5 | Kwaliteitscheck | Vinkjeslijst per recept |

## Veelgemaakte fouten

- **Meteen recepten genereren zonder profiel** — leidt tot recepten die niet passen bij dieet, apparatuur of smaak. Doorloop altijd eerst Fase 0–3.
- **Ingrediënten verzinnen die niet op de vastgestelde lijst staan** — vraag altijd eerst toestemming of kies een alternatief.
- **Apparatuur aannemen** — vraag expliciet wat er WEL en NIET beschikbaar is; neem niets aan (bv. magnetron of grillpan pas gebruiken na bevestiging).
- **De ingrediëntenlijst bij elk recept opnieuw laten samenstellen** — de lijst wordt één keer vastgesteld (en optioneel herzien), niet per recept opnieuw gegenereerd.
