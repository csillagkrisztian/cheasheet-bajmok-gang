# Javascript trükkök

## Objektum dekonstrukció

Minden objektum "entry"-k ből áll, és mindegyik "entry"-nek van egy kulcsa és egy értéke.

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

Viszont, ha az össze kulcsot ki szeretnénk venni, ez sok kóddal járhat, pláne objektumokban, amiben van több mint 5 "entry".

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

És persze ez még egy kisebb objektumnak is számítható.
Ahhoz hogy ezt meggátoljuk, dekonstruktáljuk az objektum kulcsait és saját változókká alakítjuk őket.

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

Mi van ha az objektumnak van egy objektum adata, azt ki tudom dekonstruktálni?

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

Ha a map listafunkcióban tudom, hogy az egyik elem objektum, akkor tudok ott is dekonstruktálni?

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

const coutnryLanguagesDestructuredAutoReturn = countries.map(({ languages }) => languages);

// Mind a három lista adata megegyezik.

```