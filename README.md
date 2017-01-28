# d3.sunburst

[d3.sunburst](http://jgaffuri.github.io/d3.sunburst/) is a library to easily create sunburst charts such as this one:

[<img src="img/coicop.png" alt="COICOP sunburst" width="400" height="400" />](http://jgaffuri.github.io/EurostatVisu/coicop_sunburst.html)

Sunburst charts are very much suitable to show statistical values defined on hierarchical code lists such as (TODO list examples here).

## Quick start

Let's start with a simple example: [example_v3.html](http://jgaffuri.github.io/d3.sunburst/example_v3.html).

First, add the libraries and an HTML element where the chart should bloom:

```html
<script src="https://d3js.org/d3.v3.min.js"></script>
<script src="d3-sunburst-v3.js"></script>
...
<div id="sunburst"></div>
```

The data structure is then defined like that:

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
var newValues = {"1_1":1.7, ...};
sb.set(newValues);
```

See the code example here: https://github.com/jgaffuri/d3.sunburst/blob/gh-pages/example_v3.html

## Documentation

| Method | Returns | Description |
| --- | --- | --- |
| codesHierarchy(Object codeHierarchy) | this or Object | Set or get the code hierarchy to be visualised. The structure follows the pattern: '{code:"RootCode",children:[{code:"firstChildCode",children:[...]}, ...]}' as described in the example above. |
| set(Object values, Number transitionDuration) | this | Update the chart with new values. The values should be specified as a dictionnary {code1;value1, code2;value2, ...}. The transition duration is in milliseconds. It is set to 0 by default. |
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

[d3.sunburst](http://jgaffuri.github.io/d3.sunburst/) is designed as an add-on of [D3 library](https://d3js.org/) inspired from the numerous existing sunburst examples such as [this one](https://bl.ocks.org/mbostock/4348373). It follows the approach presented [here](https://bost.ocks.org/mike/chart/), which also adopted in [C3js](http://c3js.org/).
