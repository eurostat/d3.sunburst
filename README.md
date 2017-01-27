# d3.sunburst

[d3.sunburst](http://jgaffuri.github.io/d3.sunburst/) is a library to easily create sunburst visualisations such as this one:

[![COICOP sunburst](img/coicop.png "COICOP sunburst")](http://jgaffuri.github.io/EurostatVisu/coicop_sunburst.html)

# Quick start

An example is provided in [example_v3.html](http://jgaffuri.github.io/d3.sunburst/example_v3.html).

First, add the element where the sunburst visualisation should bloom:

```html
    <div id="sunburst"></div>
```

Second, build the data structure like that:

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

```javascript
        //first set of values
        var values1 = {
            "1_1":12.4,
            "1_2":2.4,
            "1_3":5.8,
            "1_4":9.2,
            "2_1_1":2.0,
            "2_1_2":6.0,
            "2_1_3":10,
            "2_2":5.4,
            "3_1":15.8,
            "Part4":32.3
        };


```





TODO: describe simple example. based on template


# Documentation

It is an addon to [D3 library](https://d3js.org/).

