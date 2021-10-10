# React Router

## ...avagy több oldal használata

### Link: https://reactrouter.com/web/guides/quick-start

---

## Telepités

```
npm install react-router-dom
```

---

## Használat

### Importálás

```
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link
} from "react-router-dom";
```

---

### Router

A Router komponensnek az a szerepe, hogy lehetővé tegye az oldalak váltogatását a Reactben. Mindig legyen benne az egész App.js-nek a html-je

```
function App() {
    [...]
return (
    <Router>
      <div>
        [...]
      </div>
    </Router>
}
```

---

### Switch

A Switch komponens teszi lehetővé, hogy tudjunk komponenseket válogatni egy bizonyos térben. A Switch nem kötelező, hogy az egész oldalat elfoglalja, tehát fent hagyhatunk vagy lent valamit minden oldalon.

Példa: A facebook fenti sora, sosem változik.
![](../images/fb.png)

```
function Facebook() {
    [...]
return (
    <Router>
        <Navigation/>
        <Switch>
          [...]
        </Switch>
    </Router>
}
```

### Route

A Route komponens jelképezi az egyik lapot amit változtathatunk.
<br>
<br>
Fontos argumentumok:

- path - "/" - string - a link amellyel a felhasználó a bizonyos oldalat eléri
- mi megy bele? - < Home /> - komponens amelyet az oldal mutatni fog

```
function App() {
    [...]
return (
    <Router>
        <Switch>
          <Route path="/fehalsználók">
            <Users/>
          </Route>
          <Route path="/sajátprofil">
            <MyProfile/>
          </Route>
          <Route path="/">
            <Home/>
          </Route>
        </Switch>
    </Router>
}
```

---

### Link

A Link komponens egy linket készit amellyel a weboldalon belül tudunk másik oldalakra ugrándozni.
<br>
<br>
Fontos argumentumok:

- to - "/" - string - a link ahova szeretnénk menni

Példa: Egy lista ahol a linkek találhatók.

<div>
    <nav>
      <ul>
        <li>
          <a to="/">Home</a>
        </li>
        <li>
          <a to="/about">About</a>
        </li>
        <li>
          <a to="/users">Users</a>
        </li>
      </ul>
    </nav>
</div>

```
<div>
    <nav>
      <ul>
        <li>
          <Link to="/">Home</Link>
        </li>
        <li>
          <Link to="/about">About</Link>
        </li>
        <li>
          <Link to="/users">Users</Link>
        </li>
      </ul>
    </nav>
</div>
```
