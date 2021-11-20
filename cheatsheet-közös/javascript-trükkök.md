# Javascript trükkök

## Objektum dekonstrukció

Minden ```objektum ``` ```entry```-k ből áll, és mindegyik ```entry```-nek van egy kulcsa és egy értéke.

```
const country = {
    name:'Israel',
    population: 13054812,
    flag: 'https://www.flags.com/israel'
}
```

Ezekhez az adatokhoz a kulcsok segítségével tudunk hozzáférni, ezzel a két módszerrel.

```
const countryName = country.name;
const countryPopulation = country['population'];

console.log(countryName);
// "Israel"
console.log(countryPopulation);
// 1305481
```

Viszont, ha az össze kulcsot ki szeretnénk venni, ez sok kóddal járhat, pláne ```objektum```-okban, amiben van több mint 5 ```entry```.

```
const country = {
    name:"Israel",
    population: 13054812,
    flag: "https://www.flags.com/israel",
    geoLocation: "52S 41E",
    languages: ["hebrew", "english", "pakistani"],
    capital: "Jerusalem"
};

const countryName = country.name;
const countryPopulation = country.population;
const countryFlag = country.flag;
const countryCapital = country.capital;
const countrylanguages = country.languages;
const countryGeoLocation = country.geoLocation;
```

És persze ez még egy kisebb ```objektum```-nak is számítható.
Ahhoz hogy ezt meggátoljuk, ```dekonstruktáljuk az objektum kulcsait``` és saját változókká alakítjuk őket.

```
const country = {
    name:"Israel",
    population: 13054812,
    flag: "https://www.flags.com/israel",
    geoLocation: "52S 41E",
    languages: ["hebrew", "english", "pakistani"],
    capital: "Jerusalem"
};

const { name, population, flag, capital, languages, geoLocation } = country;
```

## Objektum dekonstrukció - érdekességek

Mi van ha az ```objektum```-nak van egy ```objektum``` adata, azt ki tudom ```dekonstruktálni```?

```
const country = {
    name: "Israel",
    languages:{
        mainLanguage: "hebrew",
        secondaryLanguage: "english",
        minorityLanguages:[ "pakistani", "old hebrew" ],
    }
};

const { name, languages } = country;
const { mainLanguage, secondaryLanguage, minorityLanguages } = languages;

```

Ha a ```map``` listafunkcióban tudom, hogy az egyik elem ```objektum```, akkor tudok ott is ```dekonstruktálni```?

```
const countries = [
    {
        name: "Israel",
        languages:{
            mainLanguage: "hebrew",
            secondaryLanguage: "english",
            minorityLanguages: [ "pakistani", "old hebrew" ],
    }, 
    {
        name: "Hungary",
        languages:{
            mainLanguage: "hungarian",
            secondaryLanguage: "german",
            minorityLanguages: [ "serbian", "slovakian" ],
    }
];

const countryLanguages = countries.map((country)=> {
    return country.languages;
});

const countryLanguagesDestructured = countries.map(({languages})=> {
    return languages;
});

const countryLanguagesDestructuredAutoReturn = countries.map(({ languages }) => languages);


// Mind a három lista adata megegyezik.
console.log(countryLanguages);
console.log(countryLanguagesDestructured);
console.log(countryLanguagesDestructuredAutoReturn);

```

---

## ... vagy Spread Operator- avagy adat szórás listában és objektumban

Ha össze szeretnénk ```listákat``` kombinálni, erre van egy egyszerű megoldás. A ```...``` operátor.
Ez a beépített funckió lehetővé teszi, hogy kiszedjuk listáknak és objektumoknak az ```entry``` adatait és átszórjuk másik ```listába``` vagy ```objektum```-ba.

Példa: Lista

```
const patients = ["Jani", "Mari"];
const nurses = ["Sladjana", "Andrea"];
const doctor = "Dr. Marko";

const hospitalResidents = [...patients, ...nurses, doctor];
console.log(hospitalResidents);
// ["Jani", "Mari", "Sladjana", "Andrea", "Dr. Marko"]
```

Példa: Objektum
```
const person = {
    id:578911,
    name:"Milos",
    age:'29',
}

const diagnosys = {
    disease: "Megfázás",
    cameToHospital: "2021-11-09",
    medicine: null,
}

const patient = {
    ...person,
    ...diagnosys
}
console.log(patient);
// 
{
    id:578911
    name:"Milos",
    age:'29',
    disease: "Megfázás",
    cameToHospital: "2021-11-09",
    medicine: null,
}
```

## Spread édekességek    

Egy ```objektum``` elemeit, nem tudjuk egy ```listába``` beleszórni.

```
const user = {
    name:"Daniel",
    age:21,
}

const patients = [
    {
        name:"Sandra",
        age:48,
    },
    {
        name:"Alex",
        age:16,
    }
];

const newPatients = [...patients,...user];
console.log(newPatients);
// ERROR

```

A problémát képzeljük el másképp. És rájövünk, hogy mi az ```error```.

```
const newPatients = [...patients,...user];
```
A ```...``` operátor megváltoztatja és így fog kinézni

```
const newPatients = [ { name:"Sandra", age:48 }, { name:"Alex", age:16 }, name:"Daniel", age:21 ];
console.log(newPatients);
// ERROR
```
Mivel nem tartalmazhat ```kulcs:adat``` párokat a ```lista```, ezért összetörik a kód.




