# d3.sunburst

[d3.sunburst](http://eurostat.github.io/d3.sunburst/) is a library to easily create sunburst charts such as this one:

[<img src="img/coicop.png" alt="COICOP sunburst" width="400" height="400" />](http://eurostat.github.io/EurostatVisu/coicop_sunburst.html)

Sunburst charts are very much suitable to show statistics defined on hierarchical code lists such as [NACE](http://ec.europa.eu/eurostat/ramon/nomenclatures/index.cfm?TargetUrl=LST_NOM_DTL&StrNom=NACE_REV2), [COICOP](http://ec.europa.eu/eurostat/ramon/nomenclatures/index.cfm?TargetUrl=LST_NOM_DTL&StrNom=HICP_2000&IntPcKey=37591913&StrLayoutCode=HIERARCHIC), [COFOG](http://ec.europa.eu/eurostat/ramon/nomenclatures/index.cfm?TargetUrl=LST_NOM_DTL&StrNom=COFOG_99&StrLanguageCode=EN&IntPcKey=&StrLayoutCode=HIERARCHIC), [ACL](http://ec.europa.eu/eurostat/ramon/nomenclatures/index.cfm?TargetUrl=LST_NOM_DTL&StrNom=TIMEUSE_08&IntPcKey=&StrLayoutCode=HIERARCHIC).


## Quick start

Let's start with [this simple example](https://bl.ocks.org/jgaffuri/434e5ae309deef74715a1758afa8130d).

First, add the libraries and an HTML element where the chart should bloom:

```html
<script src="https://d3js.org/d3.v3.min.js"></script>
<script src="https://cdn.jsdelivr.net/gh/eurostat/d3.sunburst@0.9.9/d3-sunburst.js"></script>
...
<div id="sunburst"></div>
```

The codes hierarchy is then defined like that:

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

Statistical values are then defined for some codes:

```javascript
//values
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
var newValues = {"1_1":1.7, ...};
sb.set(newValues);
```

See the code example [here](https://bl.ocks.org/jgaffuri/434e5ae309deef74715a1758afa8130d).

## Documentation

| Method | Returns | Description |
| --- | --- | --- |
| codesHierarchy(Object codeHierarchy) | this or Object | Set or get the code hierarchy to be visualised. The structure follows the pattern: '{code:"RootCode",children:[{code:"firstChildCode",children:[...]}, ...]}' as described in the example above. |
| set(Object values, Number transitionDuration) | this | Update the chart with new values. The values should be specified as a dictionary '{"code1":value1, "code2":value2, ...}' where the values are positive real numbers. The transition duration is in milliseconds. If omitted, the default is 0 (instant). |
| drawLabels(Number transitionDuration) | this | Draw the text labels. |
| eraseLabels(Number transitionDuration) | this | Erase the text labels. |
| div(String divString) | this or String | Set or get the id of the HTML element where to show the chart. Default value: "sunburst". |
| radius(Number radius) | this or Number | Set the radius of the chart in pixel number. Default value: 150 |
| strokeWidth(Number width) | this or Number | The stroke width to draw the sectors outline. Default value: 1 |
| strokeColor(String color) | this or String | The stroke color to draw the sectors outline. Default value: "white" |
| codeToColor(Function fun) | this or Function | A function 'function(code){ ... }' returning the color to fill the sectors depending on the code. Default value: 'function(code){ return "#ccc";}' |
| setmouseover(Function fun) | this or Function | A function 'function(code){ ... }' executed on mouseover a sector. By default, the sector is shaded. |
| setmouseout(Function fun) | this or Function | A function 'function(code){ ... }' executed on mouseout a sector. By default, the sector is set to its initial value. |
| codeToLabelText(Function fun) | this or Function | A function 'function(code){ ... }' returning the label text. By default, the label is the code: function(code){ return code;} |
| fontFamily(Function fun) | this or Function | A function 'function(depth){ ... }' returning the label font family depending on the ring depth. Default value: 'Myriad'. |
| fontSize(Function fun) | this or Function | A function 'function(depth){ ... }' returning the label font size depending on the ring depth. Usually, deaper labels need to be smaller. Default value: '12', whatever the depth. |
| fontFill(Function fun) | this or Function | A function 'function(depth){ ... }' returning the label color depending on the code ring. Usually, deaper labels are filled with lighter colors. Default value: Dark gray "#333", whatever the depth. |
| fontWeight(Function fun) | this or Function | A function 'function(depth){ ... }' returning the label [font weight](https://www.w3.org/wiki/CSS/Properties/font-weight) depending on the ring depth. Usually, deaper labels are filled with weaker font weights. Default value: 'bold' for the first ring, 'regular' for the others. 'function(depth){ return depth<=1?"bold":"regular";}' |
| fontOrientation(Function fun) | this or Function | A function 'function(depth){ ... }' returning the label orientation depending on the ring depth. The values can be 'h' for horizontal or 'n' for normal (following the sector angle). Default value: 'h' for the first ring, 'n' for the others. 'function(depth){ return depth<=1?"h":"n";}' |
| labelRotationParameter(Function fun) | this or Function | A function 'function(depth){ ... }' returning a parameter used the the label rotation depending on the ring depth. For small sectors, a 90° rotation is automatically applied to the label so that it fits to its sector - the threshold when this rotation is applied is controlled with this parameter. Default value: 1 |
| labelRemovalParameter(Function fun) | this or Function | A function 'function(depth){ ... }' returning the label deletion parameter depending on the ring depth. When a sector is too small, no label is shown - the threshold when this occurs is controlled with this parameter. Default value: 1 |

## About

[d3.sunburst](http://eurostat.github.io/d3.sunburst/) is designed as an add-on of [D3 library](https://d3js.org/) inspired from the numerous existing sunburst examples such as [this one](https://bl.ocks.org/mbostock/4348373). It follows the approach presented [here](https://bost.ocks.org/mike/chart/), which also adopted in [C3js](http://c3js.org/).

