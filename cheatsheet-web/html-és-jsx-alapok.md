# HTML és JSX alapok

_A ```HTML``` egy olyan programnyelv mellyel meghatározhatjuk a weboldalunk működő részeit._

<br>

## _HTML definíciók_

A ```HTML``` elemekből áll amelyeket így fogalmazunk meg:

```
<{elem}> {tartalom} </{elem}>
```

Példa: Egy paragrafus elem

```
<p> Hello World </p>
```

Weboldal:

---

## <p> Hello World </p>

---

---

<br>

Az elemeknek lehetnek argumentumai is:

```
<{elem} {argumentum}={adat}>{tartalom}</{elem}>
```

Példa: Egy paragrafus elem piros szín stílus argumentummal

```
<p style="color:red;"> Hello World </p>
```

Weboldal:

---

## <p style="color:red;"> Hello World </p>

---

---

<br>

Ha egy elemnek nincs tartalma, akkor használhatjuk a ```rövid elem definíció```-t is:

```
<{elem} {argumentum}={adat} />
```

Példa: Egy kép elem a src avagy forrás argumentummal

```
<img src="https://post.healthline.com/wp-content/uploads/2020/08/Alternative_Treatments_for_Alcoholism-732x549-thumbnail-1-732x549.jpg"/>
```

Weboldal:

---

<img src="https://post.healthline.com/wp-content/uploads/2020/08/Alternative_Treatments_for_Alcoholism-732x549-thumbnail-1-732x549.jpg"/>

---

---

## _Elemek típusai_

- div - divider - elválasztó
- p - paragrafus
- br - break - üres sor
- a - hyperlink
- h{szam} - header - fejléc - a szám meghatározza a méretét 1 a legynagyobb 6 a legkissebb
- input - betáplált információ - felhaszáló átal hozzáférhető eszköz, mellyel bevihet információt
- button - gomb
- img - kép

---

## _Mi az a JSX?_

Mivel mi nem fogunk tiszta ```HTML```-t használni ezért sokminden ami itt van, nem fog működni React nélkül. A ```JSX``` az ennek a React ```HTML``` kombinációnak az elnevezése.

```
JSX = HTML + React + JavaScript
```