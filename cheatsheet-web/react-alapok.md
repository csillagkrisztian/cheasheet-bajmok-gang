# React Alapok

## React Komponensek

_A React komponensek JavaScript segítségével létrehozott funkciók, amiket személyreszabott HTML szerű elemekként tudunk felhasználni._

Komponens definíciója:

```
             1
function Komponens() {
    2
  [...]
  return (
      3
    <div>
      [...]
    </div>
  )
}
```

1. A komponens neve
2. A kód amit a komponensen belül előkészíti a látható adatot
3. A ```HTML``` kód amit a weboldalunkon látható

## A React Parancsolatai

1. A komponensek neve **_MINDIG NAGY BETŰVEL KEZDŐDIK_**!

2. React esetén minden komponensben a ```JSX``` a **_return_** funkcióval küldhető a weboldalunknak.

3. A return funkcióban felhasználhatunk bármilyen ```HTML``` elemet.

4. A return funkcióban felhasználhatunk ```JavaScript```-et a {} jelek segítségével.

5. A ```return``` funkcióban bármelyik más komponenseinket is felhasználhatjuk

4-es Példa:

```
function Komponens() {
  const text = "Bazdmeg magad köcsög";
  const blue = { color: "blue" };
  return (
    <p style={blue}>{ text }</p>
  )
}
```

Weboldal:

---

## <p style="color:blue;">Bazdmeg magad köcsög</p>

---

<br>

Példa:

```
function Title() {
  return (
    <h1> Valami </h1>
  )
}

function Description() {
  return (
    <p> Valami más </p>
  )
}

function App() {
  return (
      <div>
        <Title/>
        <Description/>
        <Description/>
      </div>
  )
}
```

Weboldal:

---

<h2> Valami </h2>
<p> Valami más </p>
<p> Valami más </p>

---

<br>

## A Komponensek argumentumai

A komponensek legnagyobb ereje abban rejlik, hogy újrahasznosíthatóak. A részletesebb újrahasznosítást az ```argumentum```-ok teszik lehetővé. Ahhoz, hogy egy ```argumentum```-ot tartalmazzon a komponens, hozzá kell adni a komponenshez, a következő módon.

```
function Title({text}) {
  return (
    <h1>{text}</h1>
  )
}

function App() {
  return (
      <div>
        <Title text={"Főcím"}/>
        <Title text={"Bármi más"}/>
      </div>
  )
}
```
Weboldal:

---

<h2> Főcím </h2>
<h2> Bármi más </h2>

---

Az ```argumentum``` szerepe, hogy egy adatod megváltozhatóvá tehetünk, és ezátal könnyen tudunk komponenseket újrahasznosítani. Ha egy komponens definíciójában, felhasználunk kötelezően egy argumentumot:

```
function Title({text}) {
  return (
    <h1>{text}</h1>
  )
}
```

De nem adunk meg text ```argumentum```-ot a komponens előhívásakor:

```
function App() {
  return (
      <div>
        <Title/>
      </div>
  )
}
```

Ebben az esetben nem fogunk látni semmit, hiszen a ```text``` argumentum, mely meg kéne, hogy adja a komponens szövegét, hiányzik avagy ```undefined``` értéke lesz. Egy ```<h1>``` elem esetén nem okoz nagy fejfájást, de ha az ```argumentum``` lista, objektum, vagy adat melyet más funkciókban felhasználunk, akkor ```ERROR```-t fog okozni.

Ha esetleg több ```argumentum```-ot adunk meg, mint amennyit elvárunk:

```
function App() {
  return (
      <div>
        <Title text="Nena" age={21} color="red"/>
      </div>
  )
}
```
Ebben az esetben semmi probléma nem alakul ki, hiszen ha nem használjuk fel az extra ```argumentum```-okat, ez nem okoz problémát, csak felesleges.

---

# Hook funkciók


Egy ```hook``` egy olyan funckió mely képes az applikáció pillanatnyi helyzetével és memóriával dolgozni.


## Importálás

```
import React, { useState, useEffect } from "react";
```

---

## useState

A ```useState``` egy ```hook``` ami képes adatot tárolni a weboldalon és számon tartani a komponens pillanatnyi állapotát. 

```
function App() {
      1      2        3                4
    const [state, setState] = useState({});
}
```

1. a két variáns definíciója
2. a vödörben lévő adat
3. a vödört megváltoztató funkció
4. a kezdőadat

Példa: 
```
import React, { useState } from 'react';

function Example() {
  const [number, setNumber] = useState(0);

  return (
    <div>
      <p>A gombra klikkeltél ennyi alkalommal: {number} </p>
      <button onClick={() => setNumber(number + 1)}>
        Klikk ide!
      </button>
    </div>
  );
}
```

- Amint a komponens a weboldalra kerül, a ```number``` változó értéke ```0```, mert a kezdőadat ami a ```useState()``` ```hook``` funkcióban lévő argumentum ```0```.
- Ezután a gombban lévő ```onClick``` - ```eventListener``` azaz eseményt váró funkció, tartalmazza a ```setNumber``` nevű funkciót, mely argumentuma, az új ```number``` változó lesz.
- Mivel ennek az argumentuma ```number+1``` ezért a pillanatnyi ```number``` értékéhez, ami ```0```, hozzáad egyet.
- A ```number``` változó ez a funkció után frissíti a weboldalat és ettől kezdve ```1```-es számot tartalmazza.

---

## useEffect

A ```useEffect hook``` lehetővé teszi, hogy kövessük a komponenssel történő eseményeket.
A ```useEffect``` lefut akárhányszor egy komponens frissül, megszületik, vagy meghal, függően, hogy hogyan építsük fel.
<br>

### _useEffect születéskor_

A ```useEffect```-et ha csak születéskor szeretnénk használni, azaz amikor a komponens először jön létre a weboldalon, akkor:
```
                  1        2
 useEffect( () => {[...]}, [] );
```
1. A funkció mely lefut amint a komponens megszületik.
2. Az argumentum ami lehetővé teszi az egyszeri lefutást

Példa:
```
const [database, setDatabase] = useState();
useEffect(() => {
    const fetchData = async () => {
    const result = await axios.get(
            "https://codaisseur-pokemon-api.herokuapp.com/"
        );
        setDatabase(result.data);
    };
    fetchData();
}, []);
```

A legsűrűbben használt példa erre a server-ekről való adatok letöltése. 
- Először megalakítunk egy vödröt, ahol tároljuk az adatot, amit le fogunk tölteni.
- Azután az ```Axios-library``` segítségével letöltünk egy link segítségével adatot egy ```server```-ről
- A ```setDatabase``` funkcióval a letöltött adatot a ```database``` változóba helyezzük.

<br>

### _useEffect halálkor_

A komponens halála, azt jelenti, hogy vagy egy más komponens veszi át a helyét. Vagy a weboldal becsukódik a böngészőben.

```
useEffect(() => {
    return () => {[...]}
});
```

Ezt legtöbbször az ```online```/```offline``` funkcionalitás esetén használjuk. Példa erre a Facebook chat funkciója.

Példa:

![](../képek/react-alapok-1.png)

Mint ahogy látjátok, ```Csillag Ottó``` chat komponens online és ```Nina Peckelsen``` chat komponens offline állapotot tartalmaz. Ez azt jelenti, hogy valahol ```Csillag Ottó``` weboldala valamilyen applikációban meg van nyitva.

Nyilván gőzöm sincs mi mindent csinál a facebook, de így le tudjuk ellenőrizni a működését egy ```Switch``` segítségével. 

```
 const Practice = () => {
    useEffect(()=>{
      console.log("Pillanatnyi státusz: Online");
      return () => {
        console.log("Pillanatnyi státusz: Offline");
      }
    });

    return <p>Gyakorlat</p>
 };

 return (
    <Router>
      <Navigation />
      <Switch>
        <Route path="/practice">
          <Practice />
        </Route>
        <Route path="/">
          <Home />
        </Route>
      </Switch>
    </Router>
 );
```
- Nyissuk meg az ```inspector```-t a Google Chromeban.
- Írjuk be a szükséges linket, hogy elérjük a ```Practice``` komponenst:```localhost:3000/practice```
- Lássuk, hogy a ```Pillanatnyi státusz``` - ```console.log``` legutolsó nyomtatásánál, hogy ```Online```.
- A navigáció segítségével menjünk egy másik oldalra (ne frissítsd az oldalat, mert úgy nem lesz időd meglátni)
- Az ```inspector```-ban láthatjuk komponensünk utolsó szavát, amivel azt jelzi, hogy ```Offline```.

<br>

### _useEffect frissítéskor_

Ebben az esetben, akárhányszor valami megváltozik a komponens memóriájában, futtatunk egy bizonyos funkciót.

```              1
useEffect( () => {[...]} );
```
Példa:
```

import React, { useState } from 'react';

function Example() {
  const [number, setNumber] = useState(0);

  useEffect(()=> {
    console.log("Valami történt")
  })

  return (
    <div>
      <p>A gombra klikkeltél ennyi alkalommal: {number} </p>
      <button onClick={() => setNumber(number + 1)}>
        Klikk ide!
      </button>
    </div>
  );
}
```

Itt lássuk, hogy akárhányszor ráklikkelünk a gombra, mindig kidobja, hogy megváltozott valami. Viszont azt is meg tudjuk oldani, hogy ne akkor fusson, ha a memória változik, hanem csak egy bizonyos adat.

Példa:

```
function Example() {
  const [number, setNumber] = useState(0);
  const [word, setWord] = useState("");

  useEffect(()=> {
    console.log("Valami történt")
  })

  useEffect(()=> {
    console.log("Változott a szöveg")
  },[word])

  return (
    <div>
      <p>A gombra klikkeltél ennyi alkalommal: {number} </p>
      <button onClick={() => setNumber(number + 1)}>
        Klikk ide!
      </button>

      <p>Ezt a szöveget írtad be: {word} </p>
      <input type="text" onChange={(event)=>{setWord(event.target.value)}}/>
    </div>
  );
}
```
- Nyissuk meg az inspectort.
- Klikkeljünk a gombra. // Valami történt
- Írjuk át a szöveget. // Valami történt, Változott a szöveg

Szóval ```[word]``` segítségével, sikerült a funkció futtatását egy adat változtatásához kötni, ha a ```word``` megváltozik, akkor futunk újra. Ha ezt üresen hagyjuk, ```[]``` csak egyszer fog lefutni, mert függni fog a semmitől és persze az első lefutás után a semmi nem fog változni.