# Rendering: kennis en voorkeuren

Samenvatting van wat besproken en beslist is over snelle visualisatierenders vanuit 3D-views.
Bedoeld als achtergrond voor elke AI-assistent of renderingtool die hiermee verder werkt.

## Profiel en voorkeuren

- Achtergrond in VFX. Kent renderen, maar wil **geen eindeloos tweaken of geprutst** meer.
- Zoekt **snelle oplossingen**: binnen ongeveer **5 minuten** een semi-realistisch beeld of een
  sfeerbenadering die de klant helpt kiezen.
- Het resultaat moet **trouw blijven aan de viewport**: geometrie, camerastandpunt, verhoudingen,
  ramen en openingen mogen niet veranderen.
- **Bijsturen** moet kunnen wanneer iets verkeerd geïnterpreteerd wordt, liefst lokaal (één onderdeel
  aanpassen zonder de rest opnieuw te genereren).
- **Geen texturen aanbrengen** in het CAD-programma. Materialen worden **in woorden beschreven** per
  onderdeel van de scène.
- Antwoorden graag in het Nederlands, kort en praktisch.

## Huidige situatie (november 2026)

- Bron van de 3D-views: **Vectorworks** (gebruikt door een naaste medewerker). Die kan DWG's en
  **screenshots van de 3D-view** aanleveren. De screenshots volstaan voor deze workflow; DWG's zijn
  alleen nodig om zelf het model aan te passen.
- Eerder bekeken: SketchUp (met Diffusion of Veras) en 3ds Max. 3ds Max is afgevallen omdat het
  te veel opzet- en tweakwerk vraagt.
- Volgende stap: **Grok testen** op screenshots, en hetzelfde vergelijken met Gemini en ChatGPT.

## Werkwijze: ID-kleuren in plaats van texturen

1. Elk onderdeel (in Vectorworks: per **klasse**) krijgt een **effen kleur** (vloer rood, muren
   blauw, kasten groen, ...), zoals een ID-pass in VFX.
2. Screenshot van de 3D-view maken.
3. In de prompt per kleur het gewenste materiaal beschrijven.
4. Eén correctie per keer om bij te sturen.

## Promptsjabloon (Engels werkt meestal het best)

```
Turn this 3D CAD screenshot into a photorealistic architectural visualization.
Keep the geometry, camera angle, proportions, windows and openings EXACTLY as they are.
Do not add, remove or move any walls, windows or furniture.

Materials (by color in the image):
- Red surfaces: [wide oak floorboards, light oiled, matte]
- Blue surfaces: [warm off-white lime plaster walls]
- Green surfaces: [dark green lacquered cabinets with brass handles]
- Grey surfaces: [concrete-look countertop]

Mood and light: [soft late afternoon sunlight through the windows, warm and calm].
Style: [Scandinavian interior, natural and minimal].
```

Voorbeelden van correcties:

- `Keep everything the same, only make the floor a lighter oak.`
- `The window on the left was removed — put it back exactly as in the original.`
- `Add a few large plants in the right corner, change nothing else.`
- `Make the lighting more overcast and soft.`

## Testcriteria bij het vergelijken van tools

1. Geometrie klopt (ramen, deuren, verhoudingen op hun plaats).
2. Materialen komen op de juiste plek (kleuren correct vertaald).
3. Bijsturen werkt (een correctie verandert alleen wat gevraagd is).
4. Snelheid: haalbaar binnen ongeveer 5 minuten.
5. Resolutie volstaat om aan een klant te tonen.

## Overzicht van de bekeken opties

| Optie | Trouw aan het model | Snelheid | Bijsturen | Opmerking |
|---|---|---|---|---|
| Grok / Gemini / ChatGPT (screenshot + prompt) | Matig tot goed | Zeer snel | In gewone taal | Los van het CAD-programma; wordt getest |
| Vectorworks AI Visualizer | Goed | Snel | Via prompt | Ingebouwd sinds ongeveer 2024; beschikbaarheid hangt af van versie en licentie |
| Webtools (mnml.ai, LookX) | Goed (regelbaar) | Snel | Via prompt | Werken op een geüpload beeld |
| SketchUp Diffusion / AI Render | Matig | Snel | Beperkt | Lage resolutie, materialen wijken soms af |
| Veras (Chaos) | Goed (regelbaar) | Snel | Lokaal per zone | Ongeveer $29/maand; voor SketchUp, Revit en Rhino, niet voor Vectorworks |
| Enscape / D5 / Twinmotion | 100% | Realtime | Via het model | Vraagt materialen in het model; Enscape en Twinmotion koppelen met Vectorworks |
| 3ds Max (Arnold, V-Ray, Corona) | 100% | Traag | Volledig | Afgevallen: te veel tweakwerk |

## Mogelijke vervolgstappen

- Python-script voor Vectorworks dat elke klasse automatisch een effen kleur geeft en een
  legende (kleur naar onderdeel) maakt als basis voor de prompt. Moet eerst samen getest worden.
- Uitbreiding van het promptsjabloon met stijlvarianten (gevel, tuin, interieur).

## Context om te plakken in een AI-renderingtool

> Ik maak snelle sfeerrenders voor klanten op basis van screenshots van een 3D-view uit
> Vectorworks. Behoud altijd exact de geometrie, het camerastandpunt, de verhoudingen, ramen en
> openingen. Effen kleuren in het beeld zijn materiaalzones; ik beschrijf per kleur welk materiaal
> het moet worden. Bij een correctie pas je alleen aan wat ik vraag en laat je de rest ongewijzigd.
> Doel: binnen enkele minuten een semi-realistisch beeld dat de gewenste sfeer toont.
