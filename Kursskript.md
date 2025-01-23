# Konzepte
- Utility-First: Man verwendet vordefinierte Klassen statt CSS selbst zu schreiben 
- Tailwind: Durchsucht Dateien nach Tailwindklassen und erstellt daraus eine CSS Datei 
- Minimal: Es werden nur die vordefinierten Klassen eingebunden, die auch verwendet werden
- Direktiven: Css Datei von Tailwind erweitern 
- Anpassbar: Die vordefinierten Klasen lassen sich ändern und erweitern
- Responsive: Breakpoints für Klassen setzen, sodass sie nur für bestimmte Bildschirmgrößen gelten 
- Mobile-First: Mobile Bildschirme sind den Standard und größere Bildschirme werden durch Breakpoints angepasst 
- Interaktivität: Alle Klassen lassen sich mit Pseudoklassen wie hover kominieren 
# Einfaches Setup 
VSCode installieren
	- https://code.visualstudio.com/
VSCode Extensions installieren
	- Live Server
	- Tailwind CSS IntelliSense 
	- Auto Rename Tag
	- Prettier
VSCode Json anpassen
```json
"editor.defaultFormatter": "esbenp.prettier-vscode",
"editor.formatOnSave": true,
"prettier.printWidth": 180
```
Tailwind CDN einbinden
```html
<script src="https://cdn.tailwindcss.com"></script>
```
# Erweitertes Setup
Nodejs installieren
- https://nodejs.org
Version prüfen
```bash
node --version
```
Tailwind mit nodejs installieren 
```bash
npm install -D tailwindcss
```
Tailwind initialisieren
```bash
npx tailwindcss init
```
Konfigurationsdatei anpassen
```js
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["index.html"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
Inputdatei erstellen
```css
/* input.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```
Html Datei erstellen und output von Tailwind hinzufügen  
```html
<!-- index.html -->
<link href="output.css" rel="stylesheet">
```
Tailwind kompilieren 
```bash
npx tailwindcss -i input.css -o output.css
```
Tailwind durchgehend kompilieren 
```bash
npx tailwindcss -i input.css -o output.css --watch
```
Shortcut für Skript hinzufügen
```json
// package.json
{
  "scripts": {
    "watch": "tailwindcss -i input.css -o output.css --watch"
  },
}
```
Tailwind kompilieren mit dem Shortcut
```bash
npm run watch
```
Prettier für Tailwind installieren
```bash
npm install -D prettier prettier-plugin-tailwindcss
```
Prettier config hinzufügen
```json
//.prettierrc
{
  "plugins": ["prettier-plugin-tailwindcss"],
  "printWidth": 180
}
```
Editor neuladen
- Ctrl+Shif+P, dann "Developer: Reload window"
## CDN und Node unterschied
Es gibt eine Alternative für die Konfig, Input und tailwind Plugins mit CDN. 

Tailwind config mit CDN 
```html
<script>
    tailwind.config = {
        theme: {
            extend: {
                colors: {
                    primary: '#aa5733',
                    secondary: '#aa5733'
                }
            }
        }
    }
</script>
```
Tailwind CSS mit CDN
```html
<style type="text/tailwindcss">
@layer base {
	@apply bg-black;
}
</style>
```
Tailwind Plugins mit CDN 
```html
<script src="https://cdn.tailwindcss.com?plugins=forms,typography"></script>
```
Damit ist alles möglich, außer, dass man kein Autocomplete hat und Prettier keine Klassen sortiert
# Klassen
## Basis Klassen
Die häufigsten und einfachsten Elemente von Tailwind. 
### Color
Vordefinierte Farben für Tailwind. 
```html
<!-- schwarz und weiß -->
<div class="bg-{black|white}/{0|5|..|95|100}">

<!-- farben -->
<div class="bg-{slate|gray|zinc|netural|stone|red|orange|amber|yellow|lime|green|emerald|teal|cyan|sky|blue|indigo|violet|fuchsia|pink|rose}-{50|100|200|..|900|950}/{0|5|..|95|100}">

<!-- abkürzung -->
<div class="bg-{color}">
```
### Background color
Hintergrundfarbe für ein Element. 
```html
<!-- Hintergrundfarbe -->
<div class="bg-{color}">

<!-- Benutzerdefiniert -->
<div class="bg-[#fff]">
```
### Text color 
Textfarbe für ein Element.
```html
<!-- Textfarbe -->
<div class="text-{color}">

<!-- Benutzerdefiniert -->
<div class="text-[#fff]">
```
### Hover
Klasse anwenden, wenn Maus über dem Element ist. 
```html
<div class="hover:{class}"></div>
```
### Spacing
Vordefinierte Abstände für Tailwind. 
```html
<div class="p-{0|px|1|1.5|2|2.5|3|3.5|4|5|6|7|8|9|10|11|12|14|16|20|24|28|32|36|40|44|48|52|56|60|64|72|80|96}">

<!-- abkürzung -->
<div class="p-{spacing}">
```
### Padding
Innenabstand für ein Element. 
```html
<!-- Innerer Abstand auf jeder Seite -->
<div class="p-{spacing}">

<!-- Innerer Abstand auf bestimmter Achse -->
<div class="p{x|y}-{spacing}">

<!-- Innerer Abstand auf bestimmter Seite -->
<div class="p{t|r|b|l}-{spacing}">

<!-- Benutzerdefiniert -->
<div class="p-[3px]">
```
### Margin
Außenabstand für ein Element. 
```html
<!-- Äußerer Abstand auf jeder Seite -->
<div class="m-{spacing}">

<!-- Äußerer Abstand auf bestimmter Achse -->
<div class="m{x|y}-{spacing}">

<!-- Äußerer Abstand auf bestimmter Seite -->
<div class="m{t|r|b|l}-{spacing}">

<!-- Automatischer äußerer Abstand -->
<div class="mx-auto">

<!-- Negativ -->
<div class="-m-{spacing}">

<!-- Benutzerdefiniert -->
<div class="m-[3px]">
```
### Space between
Außenabstand zwischen Elementen auf einer Achse. 
```html
<!-- Fester Wert -->
<div class="space-{x|y}-{spacing}">

<!-- Negativ -->
<div class="-space-{x|y}-{spacing}">

<!-- Benutzerdefiniert -->
<div class="space-{x|y}-[3px]">
```
## Width & Hight
Die Breite und Höhe für ein Element anpassen. 
### Width
Breite für ein Element. 
```html
<!-- feste breite -->
<div class="w-{spacing}">

<!-- teil der verfügbaren breite -->
<div class="w-{1..11/{2..6|12}}">

<!-- ganze verfügbare breite  -->
<div class="w-full">

<!-- viewport breite  -->
<div class="w-screen">

<!-- Benutzerdefiniert -->
<div class="w-[2000px]">
```
### Height
Höhe für ein Element. 
```html
<!-- feste höhe -->
<div class="h-{spacing}">

<!-- teil der verfügbaren höhe -->
<div class="h-{1..5/2..6}">

<!-- ganze verfügbare höhe  -->
<div class="h-full">

<!-- viewport höhe -->
<div class="h-screen">

<!-- dynamische viewport höhe -->
<div class="h-dvh">

<!-- Benutzerdefiniert -->
<div class="h-[2000px]">
```
### Size
Breite und Höhe für ein Element. 
```html
<!-- feste breite und höhe -->
<div class="size-{spacing}">

<!-- teil der verfügbaren breite und höhe -->
<div class="size-{1..11/{2..6|12}}">

<!-- ganze verfügbare breite und höhe  -->
<div class="size-full">

<!-- Benutzerdefiniert -->
<div class="size-[2000px]">
```
### Min-Width
Minimale Breite für ein Element. 
```html
<!-- fester wert -->
<div class="min-w-{spacing}">

<!-- Benutzerdefiniert -->
<div class="min-w-[2000px]">
```
### Max-Width
Maximale Breite für ein Element. 
```html
<!-- fester wert -->
<div class="max-w-{spacing}">
<div class="max-w-{xs|sm|lg|xl|{2..7}xl}">

<!-- breite der breakpoins -->
<div class="max-w-screen-{sm|md|lg|xl|2xl}">

<!-- ganze verfügbare breite  -->
<div class="max-w-full">

<!-- Benutzerdefiniert -->
<div class="max-w-[2000px]">
```
### Min-Height
Minimale Höhe für ein Element. 
```html
<!-- fester wert -->
<div class="min-h-{spacing}">

<!-- ganze verfügbare höhe  -->
<div class="min-h-full">

<!-- gesamter viewport -->
<div class="min-h-screen">

<!-- gesamter dynamischer viewport -->
<div class="min-h-dvh">

<!-- Benutzerdefiniert -->
<div class="min-h-[2000px]">
```
### Max-Height
Maximale Höhe für ein Element. 
```html
<!-- fester wert -->
<div class="max-h-{spacing}">

<!-- ganze verfügbare höhe  -->
<div class="max-h-full">

<!-- gesamter viewport -->
<div class="max-h-screen">

<!-- gesamter dynamischer viewport -->
<div class="max-h-dvh">

<!-- Benutzerdefiniert -->
<div class="max-h-[2000px]">
```
## Flex
Elemente flexibel darstellen und anordnen. 
### Flex display
Element als Flex Container definieren.
```html
<!-- flex block -->
<div class="flex">

<!-- flex inline -->
<div class="inline-flex">
```
### Gap
Abstand zwischen flex und grid elementen. 
```html
<!-- fester wert -->
<div class="flex gap-{spacing}">

<!-- fester wert achse -->
<div class="flex gap-{x|y}-{spacing}">

<!-- Benutzerdefiniert -->
<div class="gap-[3px]">
```
### Flex direction 
Anordnung der Elemente im Flex Container.
```html
<!-- standard, nebeneinander anordnen -->
<div class="flex flex-row">

<!-- untereinander anordnen -->
<div class="flex flex-col">
```
### Flex wrap 
Umbruchverhalten im Flex Container.
```html
<!-- standard, element umbruch nicht erlauben -->
<div class="flex flex-nowrap">

<!-- element umbruch erlauben -->
<div class="flex flex-wrap">
```
### Flex basis
Initiale größe für ein Flexelement. 
```html
<!-- fester wert -->
<div class="basis-{spacing}">

<!-- prozentualler wert -->
<div class="basis-{1..11/{2..6|12}}">

<!-- gesamte breite -->
<div class="basis-full">

<!-- Benutzerdefiniert -->
<div class="basis-[13%]">
```
### Grow & Shrink
Definiert wie das Flexelement größer und kleiner werden darf.
```html
<!-- standard, grow nein und shrink ja, abhängig von der Initialgröße -->
<div class="flex-initial">

<!-- grow und shrink ja, unabhängig von der Initialgröße -->
<div class="flex-1">

<!-- grow und shrink ja, abhängig von der Initialgröße -->
<div class="flex-auto">

<!-- grow ja, abhängig von der Initialgröße -->
<div class="grow">

<!-- grow nein -->
<div class="grow-0">

<!-- grow und shrink nein -->
<div class="flex-none">

<!-- shrink ja, abhängig von der Initialgröße -->
<div class="shrink">

<!-- schrink nein -->
<div class="shrink-0">
```
### Order
Reihenfolge vom Flex oder Grid Element.   
```html
<!-- standard = 0 -->
<div class="order-none">

<!-- fester wert -->
<div class="order-{1..12}">
<div class="order-{first|last}">

<!-- Negativ -->
<div class="-order-{1..12}">

<!-- Benutzerdefiniert -->
<div class="order-[42]">
```
## Grid
Elemente in einer Kachelform anordnen. 
### Grid display
Element als Gridelement definieren. 
```html
<!-- grid block -->
<div class="grid">

<!-- grid inline -->
<div class="inline-grid">
```
### Grid cols und rows
Anzahl den Spalten und Reihen definieren. 
```html
<!-- keine spalten -->
<div class="grid grid-cols-none">

<!-- anzahl der spalten -->
<div class="grid grid-cols-{1..12}">

<!-- keine reihen -->
<div class="grid grid-rows-none">

<!-- anzahl der reihen -->
<div class="grid grid-rows-{1..12}">
```
### Grid span
Die Spalten- und Reihenbreite definieren. 
```html
<!-- standard -->
<div class="col-auto row-auto">

<!-- spaltenbreite -->
<div class="col-span-{1..12|full}">

<!-- reihenbreite -->
<div class="row-span-{1..12|full}">
```
### Grid start und end
Die Start- und Endposition für Reihen und Spalen definieren. 
```html
<!-- standard -->
<div class="col-start-auto col-end-auto row-start-auto row-end-auto">

<!-- die start und end position der spalte -->
<div class="col-start-{1..13} col-end-{1..13}">

<!-- die start und end position der reihe -->
<div class="row-start-{1..13} row-end-{1..13}">
```
## Box Positionierung
Positionierung der Flex und Grid Elemente. 
### Justify content
Flex: Positionierung der Elemente entlang der x Achse. 
Grid: Keine Anwendung. 
```html
<div class="flex justify-{center|start|end|around|between|evenly}">
```
### Align content
Flex: Positionierung der Reihen der Elemente entlang der y Achse. 
Grid: Keine Anwendung. 
```html
<div class="flex content-{center|start|end|around|between|evenly|stretch}">
```
### Justify items
Flex: Keine Anwendung. 
Grid: Positionierung der Grid-items innerhalb ihrer Zellen entlang der x Achse. 
```html
<div class="grid justify-items-{center|start|end|stretch}">
```
### Align items
Flex: Positionierung der Elemente entlang der y Achse. 
Grid: Positionierung der Gridelemente innerhalb ihrer Zellen entlang der y Achse. 
```html
<div class="grid items-{center|start|end|stretch}">
```
### Justify self
Flex: Keine Anwendung. 
Grid: Positionierung eines Gridelemente innerhalb der Zelle entlang der x Achse. 
```html
<div class="justify-self-{center|start|end|stretch}">
```
### Align self
Flex: Positionierung eines Elementes im Flexcontainer auf der Kreuzachse. 
Grid: Positionierung eines Gridelementes innerhalb der Zelle entlang der y Achse. 
```html
<div class="self-{center|start|end|stretch}">
```
## Ränder
### Radius
Rundung für ein Element definieren. 
```html
<!-- Standard -->
<div class="rounded-none">

<!-- radius für alle seiten -->
<div class="rounded-{sm|_|md|lg|xl|2xl|3xl|full}">

<!-- radius für eine bestimmte seite -->
<div class="rounded-{t|r|b|l}-{sm|_|md|lg|xl|2xl|3xl|full}">

<!-- radius für eine bestimmte ecke -->
<div class="rounded-{tr|br|bl|tl}-{sm|_|md|lg|xl|2xl|3xl|full}">

<!-- Benutzerdefiniert -->
<div class="rounded-[50px]">
```
### Border 
Rand für ein Element definieren. 
```html
<!-- standard -->
<div class="border-none">

<!-- breite für alle seiten -->
<div class="border-{0|_|2|4|8}">
<!-- breite für eine bestimmte seite -->
<div class="border-{t|r|b|l}-{0|_|2|4|8}">
<!-- breite für eine bestimmte achse -->
<div class="border-{x|y}-{0|_|2|4|8}">

<!-- farbe für alle seiten -->
<div class="border border-{color}">
<!-- farbe für eine bestimmte seite -->
<div class="border border-{t|r|b|l}-{color}">
<!-- farbe für eine bestimmte achse -->
<div class="border border-{x|y}-{color}">

<!-- stil für den rand -->
<div class="border-{solid|dashed|dotted|double}">
```
### Divider
Rand zwischen den Elementen definieren. 
```html
<!-- standard -->
<div class="divide-{x|y} divide-none">

<!-- divider breite -->
<div class="divide-{x|y}-{0|_|2|4|8}">

<!-- divider farbe -->
<div class="divide-{x|y} divide-{color}">

<!-- divider stil -->
<div class="divide-{x|y} divide-{solid|dashed|dotted|double}">
```
### Shadow
Schatten für ein Element definieren. 
```html
<!-- standard -->
<div class="shadow-none">

<!-- schattenbreite -->
<div class="shadow-{sm|_|md|lg|xl|2xl}">

<!-- inner schatten -->
<div class="shadow-inner">

<!-- schattenfarbe -->
<div class="shadow shadow-{color}">

<!-- benutzerdefiniert -->
<div class="shadow shadow-[x_y_verwaschung_breite]">
<div class="shadow shadow-[inset_x_y_verwaschung_breite]">
```
### Ring
Schattenrand für ein Element definieren. 
```html
<!-- ring breite -->
<div class="ring-{0|1|2|_|4|8}">

<!-- ring farbe -->
<div class="ring ring-{color}">

<!-- ring offset breite -->
<div class="ring ring-offset-{0|1|2|4|8}">

<!-- ring offset farbe -->
<div class="ring ring-offset-{color}">
```
### Outline
Äußerer Rand für ein Element. 
```html
<!-- outline stil -->
<div class="outline-{dashed|dotte|double}">

<!-- outline solid -->
<div class="outline">

<!-- kein outline -->
<div class="outline-none">

<!-- outline breite -->
<div class="outline outline-{0|1|2|4|8}">

<!-- outline farbe -->
<div class="outline outline-{color}">

<!-- outline offset -->
<div class="outline outline-offset-{0|1|2|4|8}">
```
## Pseudo Klassen
Klassen an bestimmte Zustände binden. 
### Focus
Element wird fokussiert
```html
<input class="focus:{class}">
```
### Focus-within
Element oder eines der Kinder wird fokussiert
```html
<div class="focus-within:{class}">
```
### Active
Element wird gedrückt
```html
<button class="active:{class}">
```
### Group 
Kinder vom Element abhängig machen
```html
<div class="group:{class}">

<!-- Gruppe gruppieren -->
<div class="group/subgroup:{class}">
```
### Peer
Nachkommen vom Element abhängig machen
```html
<div class="peer:{class}">

<!-- Peer gruppieren -->
<div class="peer/subpeer:{class}">
```
## Typography
### Decoration
Dekoration für ein Element definieren. 
```html
<!-- standard -->
<p class="no-underline">

<!-- decorationen -->
<p class="underline">
<p class="line-through">
<p class="overline">

<!-- decoration farbe -->
<div class="underline decoration-{color}">

<!-- decoration breite -->
<p class="underline decoration-{0|1|2|4|8}">

<!-- decoration stil -->
<p class="underline decoration-{solid|dashed|dotted|double|wavy}">

<!-- decoration offset -->
<p class="underline underline-offset-{0|1|2|4|8}">
```
### Font size 
Textgröße für ein Element. 
```html
<!-- fester wert -->
<div class="text-{xs|sm|base|lg|xl|{2..7}xl}">

<!-- benutzerdefiniert -->
<div class="text-[13px]">
```
### Font weight
Schriftdicke für ein Element. 
```html
<div class="font-{light|normal|semibold|bold|extrabold}">
```
### Text align 
Text Positionierung für ein Element definieren.
```html
<div class="text-{left|right|center|justify}">
```
### Font family
Textstil für ein Element. 
```html
<div class="font-{sans|serif|mono}">
```
### Letter spacing
Abstand zwischen den Buchstaben. 
```html
<div class="tracking-{tighter|tight|normal|wide|wider|widest}">
```
### Text transform
Groß- und Kleinschreibung für ein Element. 
```html
<!-- alles groß -->
<div class="uppercase">
<!-- alles klein -->
<div class="lowercase">
<!-- anfangsbuchstaben groß -->
<div class="capitalize">
```
### Text overflow
Verhalten bei zu langem text. 
```html
<p class="truncate">
```
### Line clamp
Verhalten bei zu vielen Textzeilen. 
```html
<!-- fester wert -->
<p class="line-clamp-{1..6}">

<!-- benutzerdefiniert -->
<p class="line-clamp-[7]">
```
## Anzeige & Positionierung
### Breakpoints
Klassen am bestimmte Breakpoints binden. 
```html
<div class="{sm|md|lg|xl|2xl}:...">
```
### Container
Element mit vordefinierten Breakpoints. 
```html
<div class="container">
```
### Display
Darstellung für ein Element definieren. 
```html
<!-- breite auf inhalt begrenzt, keine breite und höhe, padding und margin nur auf der x-achse -->
<div class="inline">

<!-- breite auf inhalt begrenzt, breite und höhe setzbar, padding und margin alle richtungen -->
<div class="inline-block">

<!-- volle breite, breite und höhe setzbar, padding und margin alle richtungen -->
<div class="block">

<!-- wird nicht angezeigt -->
<div class="hidden">
```
### Position
Positionierung für ein Element. 
```html
<!-- default, im seitenfluss -->
<div class="static">

<!-- im seitenfluss, bezugspunkt für elemente, nicht staisch -->
<div class="relative">

<!-- wechsel zwischen relative und fixed, je nach scrollposition -->
<div class="sticky">

<!-- nicht im seitenfluss, wird zum viewport positioniert -->
<div class="fixed">

<!-- nicht im seitenfluss, wird zum nächsten element positioniert, das nicht static ist oder dem viewport -->
<div class="absolute">
```
### Abstand
Abstand zum Rand. 
```html
<!-- abstand zu allen seiten -->
<div class="inset-{spacing}">

<!-- abstand zu einer bestimmten achse -->
<div class="inset-{x|y}-{spacing}">

<!-- abstand zu einer bestimmten seite -->
<div class="{top|right|bottom|left}-{spacing}">

<!-- negative werte -->
<div class="-inset-{spacing}">

<!-- benutzerdefiniert -->
<div class="inset-[30px]">
```
### Z-index
Positionierung auf der z-Achse für ein Element. 
```html
<!-- element vorziehen -->
<div class="z-{0|10|20|30|40|50}">

<!-- element hinterziehen -->
<div class="-z-{0|10|20|30|40|50}">

<!-- benutzerdefiniert -->
<div class="z-[3]">
```
### Overflow
Verhalten bei zu großen Inhalt für ein Element. 
```html
<!-- overflow scroll elemente anzeigen, falls benötigt -->
<div class="overflow-auto">
<div class="overflow-{x|y}-auto">

<!-- overflow abschneiden -->
<div class="overflow-hidden">
<div class="overflow-{x|y}-hidden">

<!-- scroll elemente immer anzeigen  -->
<div class="overflow-scroll">
<div class="overflow-{x|y}-scroll">

<!-- overflow anzeigen -->
<div class="overflow-visible">
<div class="overflow-{x|y}-visible">
```
### Overscroll
Verhalten beim scrollen für ein Element. 
```html
<!-- standard -->
<div class="overscroll-auto">

<!-- nur der aktuelle container darf scrollen -->
<div class="overscroll-contain">
```

### Object fit
Positionierung eines Objektes in einem Element. 
```html
<!-- skaliert bis ein rand erreicht wurde -->
<img class="object-contain">

<!-- skaliert bis alle ränder erreicht wurden -->
<img class="object-cover">

<!-- passt objekt dem container an -->
<img class="object-fill">

<!-- orginalgröße -->
<img class="object-scale-down">
```
### Object position
Focuspunkt eines Objektes. 
```html
<img class="object-{center|top|top-right|right|bottom-right|bottom|bottom-left|left|top-left}">
```
## Background
Hintergrund für ein Element defininieren. 
### Gradient
Farbüberläuft für den Hintergrund für ein Element. 
```html
<!-- gardient richtung -->
<div class="bg-gradient-to-{t|tr|r|br|b|bl|l|tl}">

<!-- gardient mit 2 farben -->
<div class="bg-gradient-to-r from-{color} to-{color}">

<!-- gardient mit 3 farben -->
<div class="bg-gradient-to-r from-{color} via-{color} to-{color}">

<!-- gardient mit 3 farben und eigenen positionen -->
<div class="bg-gradient-to-r from-{color} from-{0,5..100}% via-{color} via-{0,5..100}% to-{color} to-{0,5..100}%">
```
## Svg
### Svg
Breite und Farben für ein Svg Element.  
```html
<!-- svg flächenfarbe -->
<svg class="fill-{color}">

<!-- svg linienfarbe -->
<svg class="stroke-{color}">

<!-- sve linienbreite -->
<svg class="stroke-{0|1|2}">
<svg class="stroke-[3px]">
```
## Transform
Element transformieren. 
### Translate
Element verschieben
```html
<!-- fester wert -->
<div class="translate-{x|y}-{spacing}">

<!-- prozentualler wert -->
<div class="translate-{x|y}-{1..3/{2..4}|full}">

<!-- negativ -->
<div class="-translate-{x|y}-{spacing}">

<!-- benutzerdefiniert -->
<div class="translate-{x|y}-[30px]">
```
### Rotate
Element rotieren
```html
<!-- fester wert -->
<div class="rotate-{0|1|2|3|6|12|45|90|180}">

<!-- benutzerdefiniert -->
<div class="rotate-[17deg]">
```
### Scale
Element skalieren
```html
<!-- beide seiten -->
<div class="scale-{0|50|75|90|95|100|105|110|125|150}">

<!-- eine achse -->
<div class="scale-{x|y}-{0|50|75|90|95|100|105|110|125|150}">
```
### Origin
Fixpunkt für Element setzen
```html
<div class="origin-{center|top|top-right|right|bottom-right|bottom|bottom-left|left|top-left}">
```
## Transition
Animation manipulieren
### Property
Elemente für animation bestimmen 
```html
<!-- standard, no transition -->
<div class="transition-none">

<!-- transition auf bestimmte elemente anwenden -->
<div class="transition-{colors|opacity|shadow|transform}">

<!-- transition auf alle der einzelnen elemente anwenden -->
<div class="transition">

<!-- transition auf alles anwenden -->
<div class="transition-all">

<!-- benutzerdefiniert -->
<div class="transition-[width]">
```
### Duration
Dauer der animation
```html
<!-- fester wert -->
<div class="transition duration-{0|75|100|150|200|300|500|700|1000}">

<!-- benutzerdefiniert -->
<div class="transition duration-[2000ms]">
```
### Function
Verlauf der animation
```html
<!-- gleiche geschwindigkeit -->
<div class="transition ease-linear">

<!-- langsamer start -->
<div class="transition ease-in">

<!-- langsames ende -->
<div class="transition ease-out">

<!-- langsamer start und end -->
<div class="transition ease-in-out">
```
### Delay
Verzögerung der animation
```html
<!-- fester wert -->
<div class="transition delay-{0|75|100|150|200|300|500|700|1000}">

<!-- benutzerdefiniert -->
<div class="transition delay-[2000ms]">
```
## Animation
Animation anwenden. 
```html
<!-- element drehen -->
<div class="animate-spin">

<!-- element pingen -->
<div class="animate-ping">

<!-- element pulsieren -->
<div class="animate-pulse">

<!-- element springen -->
<div class="animate-bounce">
```
## Interaktion

### Cursor
Stil vom Mauszeiger für ein Element. 
```html
<!-- zeigerstil -->
<div class="cursor-{auto|pointer|wait|text|help|progress|move|none|crosshair}">
```
### Select
Definieren wie Text ausgewählt wird. 
```html
<!-- standard -->
<div class="select-auto">

<!-- ganzer text -->
<div class="select-all">

<!-- nicht auswählbar -->
<div class="select-none"> 
```
## Filter
Filtereffekt für ein Element definieren. 
#### Blur
Unschärfe filter
```html
<!-- standard -->
<div class="blur-none">

<!-- fester wert -->
<div class="blur-{sm|_|md|lg|xs|2xl|3xl}">

<!-- benutzerdefiniert -->
<div class="blur-[10px]">
```
#### Hue filter
Farben rotieren
```html
<!-- fester wert -->
<div class="hue-rotate-{0|15|30|60|90|180}">

<!-- benutzerdefiniert -->
<div class="hue-rotate-[70deg]">
```
#### Grayscale
Graufilter
```html
<!-- standard, filter entfernen -->
<div class="grayscale-0">

<!-- filter setzen -->
<div class="grayscale">
```
# Fortgeschritten
## Dirketiven
### Base
Voreinstellungen und Resets zu den HTML Elementen. 
```css
@tailwind base; 

@layer base {
  body {
    /* eigenes css */
    color: white;
    /* tailwind klassen */
    @apply bg-black;
  }
  h1 {
    @apply mb-4 text-center text-4xl;
  }
}
```
### Components
Zusammenstellungen aus Tailwind Klassen und CSS. 
```css
@tailwind components;

@layer components {
  .btn {
    @apply rounded-lg bg-blue-500 px-4 py-2 text-blue-100 hover:bg-blue-700;
  }
}
```
### Utilities
Bestimmte Eigenschaften aus Tailwind Klassen und CSS. 
```css
@tailwind utilities;

@layer utilities {
  .text-error {
    @apply text-red-400;
  }
}
```
### Fonts
Font finden auf https://fonts.google.com/
#### Per link einbinden 
Head links einfügen
```html
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="output.css" />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link href="https://fonts.googleapis.com/css2?family=Jersey+25+Charted&family=Poetsen+One&display=swap" rel="stylesheet" />
  </head>
```
Css einbinden
```css
@layer base {
  body {
    font-family: "Poetsen One", sans-serif;
    font-weight: 400;
    font-style: normal;
  }
}
```
#### Herunterladen und einbinden 
Font herunterladen und die .ttf in das Projekt kopieren

CSS anpassen
```css
@layer base {
  body {
    font-family: "Poetsen One";
  }
}
@font-face {
  src: url(PoetsenOne-Regular.ttf) format("truetype");
  font-family: "Poetsen One";
  font-style: normal;
  font-weight: 400;
}
```
## Konfiguration 
### Content
Dateien für die Klassensuche einbinden 
```js
module.exports = {
  // alles in dummy
  content: ["index.html", "dummy/*"],
  // alles in dummy rekursiv mit einer bestimmten endung
  content: ["index.html", "dummy/**/*.{html,php}"]
}
```
### Safelist 
Klassen für die Css Datei whitelisten
```js
module.exports = {
  safelist: [
    "bg-red-500",
    "lg:text-4xl",
    {
      // reg expressions verwenden
      pattern: /bg-(red|green|blue)-(100|200|300)/,
    },
    {
      // varianten hinzufügen
      pattern: /bg-red-(100|200|300)/,
      variants: ["lg", "hover", "focus", "lg:hover"],
    },
	{
      // transparenzgrade weglassen
      pattern: /bg-blue-(100|200|300)$/,
    },
	{
      // alle helligkeitsgrade kurzschreibweise
      pattern: /bg-red-\d{3}$/,
    },
  ],
}
```
### Blocklist 
Klassen für die Css Datei blockieren
```js
module.exports = {
  blocklist: ["container", "collapse"],
}
```
### Theme
Tailwindklassen überschreiben oder erweitern
```js
module.exports = {
  theme: {
    container: {
      center: true,
      padding: '2rem'
    },
    extend: {
      colors: {
        primary: {
          500: "#1B4F72",
          DEFAULT: "#2E86C1",
        },
      },
      spacing: {
        100: "20rem",
      },
	}
  },
}
```
Tailwind Farben verwenden
```js
const colors = require("tailwindcss/colors");

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["index.html"],
  theme: {
    extend: {
      colors: {
        primary: {
          500: colors.blue["500"],
          DEFAULT: colors.blue["700"],
          900: colors.blue["900"],
        },
      },
    },
  },
};
```
Volle Config erstellen
```bash
npx tailwindcss init -f full-tailwind.js
```
Eigene Animation
```js
module.exports = {
  theme: {
    extend: {
      keyframes: {
        superanimation: {
          "0%": { transform: "rotate(0deg)" },
          "25%": { transform: "rotate(10deg)" },
          "50%": { transform: "rotate(0deg)" },
          "75%": { transform: "rotate(-10deg)" },
          "100%": { transform: "rotate(0deg)" },
        },
      },
      animation: {
        superanimation: "superanimation 2s linear infinite",
      },
    },
  },
};
```
### Plugins
Plugins für Tailwind einbinden
#### Forms Plugin einbinden
Plugin installieren
```bash
npm install -D @tailwindcss/forms
```
Plugin hinzufügen
```js
module.exports = {
  plugins: [require("@tailwindcss/forms")],
}
```
