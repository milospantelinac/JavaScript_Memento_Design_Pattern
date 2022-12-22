# JavaScript - Memento Design Pattern

Patern Memento omogućava privremeno skladištenje kao i rekonstrukciju nekog objketa.

## Upotreba Mementa

Mogli biste posmatrati bazu podataka kao implementaciju Memento dizajn paterna u kojem se objekti čuvaju i obnavljaju. Međutim, najčešći razlog za korištenje ovog paterna je čuvanje snapshot-a odnosno stanja objekta tako da se sve naknadne promene mogu lako poništiti ako je potrebno.

U suštini, Memento je mali repozitorijum koji skladišti stanje objekta. Scenariji u kojima možda želite vratiti objekat u stanje koje je prethodno postojalo: čuvanje i vraćanje stanja igrača u video igrama ili implementaciju poništavanja operacije u bazi podataka.

U JavaScriptu Memento se jednostavno implementira serijalizacijom i deserializacijom objekata pomoću JSON-a.

## Diagram

<img width="400" alt="memento_pattern" src="https://user-images.githubusercontent.com/21141150/208949214-8f4916c8-81db-4ef6-a1ba-2387e6cc0fa7.png">

## Učesnici

Objekti koji učestvuju u ovom paternu su:

**Originator** -- U primeru: **Person**
1. Implementira interfejs za kreiranje i vraćanje mementosa. U primeru koda: **hydrate** i **dehydrate**
2. Objekat čije se stanje privremeno čuva i obnavlja

**Memento** -- U primeru: JSON reprezentacija **Person**
1. Interno stanje objekta Originator u nekom formatu

**CareTaker** -- U primeru: **CareTaker**
1. Odgovoran za čuvanje Mementos
2. Ovo je samo skladište; ne menja Mementos

## Primer

U primeru kreiramo dve osobe pod imenom Jovana i Milica koje se stvaraju pomoću funkcijskog konstruktora **Person**. Zatim se kreiraju njihov Mementos koji održava **CareTaker** objekat.

Jovani i Milici dodeljujemo druga imena pre nego što ih vratimo iz njihovog Mementos-a. Nakon vraćanja potvrđujemo da je **Person** obejkati vraćeni u svoje izvorno stanje s prvobitnim imenima.

Sam **Memento** patern sa **CareTaker** itd. retko se koristi u JavaScriptu. Međutim, JSON je vrlo efikasan format koji je izuzetno koristan u mnogim različitim scenarijima prilikom razmene podataka.

```
var Person = function (name, street, city, state) {
    this.name = name;
    this.street = street;
    this.city = city;
    this.state = state;
}

Person.prototype = {

    hydrate: function () {
        var memento = JSON.stringify(this);
        return memento;
    },

    dehydrate: function (memento) {
        var m = JSON.parse(memento);
        this.name = m.name;
        this.street = m.street;
        this.city = m.city;
        this.state = m.state;
    }
}

var CareTaker = function () {
    this.mementos = {};

    this.add = function (key, memento) {
        this.mementos[key] = memento;
    },

        this.get = function (key) {
            return this.mementos[key];
        }
}

function run() {

    var jovana = new Person("Jovana Maric", "Janka Veselinovica 25", "Novi Sad", "Active");
    var milica = new Person("Milica Jankovic", "Janka Cmelika 60", "Novi Sad", "Inactive");
    var caretaker = new CareTaker();

    // save state

    caretaker.add(1, jovana.hydrate());
    caretaker.add(2, milica.hydrate());

    // mess up their names

    jovana.name = "Kristina Petrovic";
    milica.name = "Ana Markovic";

    // restore original state

    jovana.dehydrate(caretaker.get(1));
    milica.dehydrate(caretaker.get(2));

    console.log(jovana.name);
    console.log(milica.name);
}
// → Jovana Maric
// → Milica Jankovic
```

