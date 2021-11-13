# Listafunkciók

## Map

A map listafunkció, átfut mindegyik elemen és opcionálissan meg is változtatja

```
const map = [1,2,3].map( x=>{
if(x===1) {
    return x-1;
}
return x+1
});


// map = [0,3,4]
```

---

## Find

A find listafunkció, átfut minden elemen és visszahozza az elemet amely a kondicióval igaz lesz
Visszahoz egy objektumot = {}/adat

```
const find = [1,2,3,4].find( x=> {
return x%2===0
});

// find = 2
```

---

## Filter

A filter listafunkció, átfut minden elemen és visszahozza az elemeket amelyek a kondicióval igazak lesznek
Visszahoz egy listát = []

```
const filter = [1,2,3,4].find( x=> {
return x%2===0
});

// filter = [2,4]
```


komponens argumentum ha van ha nincs
flexbox
bootstrap grid

