# d3.sunburst

[d3.sunburst](http://jgaffuri.github.io/d3.sunburst/) is a library to easily create sunburst charts such as this one:

[![COICOP sunburst](img/coicop.png "COICOP sunburst" =50%x50%)](http://jgaffuri.github.io/EurostatVisu/coicop_sunburst.html)

# Quick start

An example is provided in [example_v3.html](http://jgaffuri.github.io/d3.sunburst/example_v3.html).

First, add the element where the chart should bloom:

```html
<div id="sunburst"></div>
```

The data structure is defined like that:

```javascript
//build codes hierarchy
var codesHierarchy = {code:"Total",children:[
    {code:"Part1",children:[{code:"1_1"},{code:"1_2"},{code:"1_3"},{code:"1_4"}]},
    {code:"Part2",children:[
        {code:"2_1",children:[{code:"2_1_1"},{code:"2_1_2"},{code:"2_1_3"},]},
        {code:"2_2"}
    ]},
    {code:"Part3",children:[{code:"3_1"}]},
    {code:"Part4"}
]};
```

Values are then defined for some codes:

```javascript
//first set of values
var values = {
    "1_1":12.4, "1_2":2.4, "1_3":5.8, "1_4":9.2, "2_1_1":2.0, "2_1_2":6.0, "2_1_3":10, "2_2":5.4, "3_1":15.8, "Part4":32.3
};
```

Finally, the chart is built with:

```javascript
//build sunburst with first set of values
var sb = d3.sunburst()
    .codesHierarchy(codesHierarchy)
    .set(values);
```

The chart can simply be updated with another set of values:

```javascript
var valuesNew = {"1_1":1.7, ...};
sb.set(valuesNew);
```

See the code example here: https://github.com/jgaffuri/d3.sunburst/blob/gh-pages/example_v3.html

# Documentation

It is an addon to [D3 library](https://d3js.org/).

