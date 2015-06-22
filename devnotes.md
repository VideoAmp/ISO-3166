Just random things, nothign to see here


iso3166.json
```
var list = [
    [
        "numerical",
        "parent",
        "name",
        "code",
        "alpha2",
        "alpha3",
        "subdivision"
    ]
];

function listItems(v) {
    list.push([
        parseInt(v.numericalCode) || "",
        parseInt(this.parent.numericalCode) || "",
        v.name || "",
        v.alpha2 || "",
        (v.alpha2 && v.alpha3) ? v.alpha2 : "",
        v.alpha3 || "",
        (v.alpha2 && !v.alpha3) ? v.alpha2 : ""
    ]);

    if ( v.entities ) {
        _.each(v.entities,listItems,{parent:v});
    }
}

_.each(regions,listItems);

JSON.stringify(list);
```



byCode.json
```
_.chain(list).map(function(v){
    return {
        numerical: v[0],
        parent: v[1],
        name: v[2],
        code: v[3],
        alpha2: v[4],
        alpha3: v[5],
        subdivision: v[6],
    };
}).indexBy("code").value()
```



byNumerical.json
```
var byNumerical = _.chain(list).map(function(v){
    return {
        numerical: v[0],
        parent: v[1],
        name: v[2],
        code: v[3],
        alpha2: v[4],
        alpha3: v[5],
        subdivision: v[6],
    };
}).indexBy("code").indexBy("numerical").value()
delete byNumerical[""];
JSON.stringify(byNumerical);
```



byRegion.json
```
var byAlpha2 = _.chain(list).map(function(v){
    return {
        numerical: v[0],
        parent: v[1],
        name: v[2],
        code: v[3],
        alpha2: v[4],
        alpha3: v[5],
        subdivision: v[6],
    };
}).indexBy("code").indexBy("alpha2").value()
delete byAlpha2[""];
delete byAlpha2["alpha2"];
JSON.stringify(byAlpha2);
```



bySubregion.json
```
var bySubregion = _.chain(list).map(function(v){
    return {
        numerical: v[0],
        parent: v[1],
        name: v[2],
        code: v[3],
        alpha2: v[4],
        alpha3: v[5],
        subdivision: v[6],
    };
}).indexBy("code").indexBy("subdivision").value();
delete bySubregion["subdivision"];
delete bySubregion[""];
JSON.stringify(bySubregion);

```

