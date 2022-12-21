# JavaScript - Memento Design Pattern

Patern Memento omogućuje privremeno skladištenje kao i rekonstrukciju nekog objketa.

## Upotreba Mementa

Mogli biste posmatrati bazu podataka kao implementaciju Memento dizajn paterna u kojem se objekti čuvaju i obnavljaju. Međutim, najčešći razlog za korištenje ovog paterna je snimanje snapshot-a odnosno stanja objekta tako da se sve naknadne promene mogu lako poništiti ako je potrebno.

U suštini, Memento je mali repozitorijum koji skladišti stanje objekta. Scenariji u kojima možda želite vratiti objekat u stanje koje je prethodno postojalo: čuvanje i vraćanje stanja igrača u video igrama ili implementaciju poništavanja operacije u bazi podataka.

U JavaScriptu Memento se jednostavno implementira serijalizacijom i deserializacijom objekata pomoću JSON-a.

## Diagram

<img width="400" alt="memento_pattern" src="https://user-images.githubusercontent.com/21141150/208949214-8f4916c8-81db-4ef6-a1ba-2387e6cc0fa7.png">

## Učesnici

Objekti koji učestvuju u ovom paternu su:

