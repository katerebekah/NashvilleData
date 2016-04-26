#Angular, APIs, and Charts

This project queries a open dataset from [data.Nashville.gov](data.nashville.gov) and creates a chart and a list view.

------
###Setup
```
mkdir -p ~/workspace/exercises/rich-browser/nashvilledata && cd $_
```

Your basic file structure should look like this:
```
index.html
app
--app.js
--homeController.js
--chartController.js
--listController.js
--apiFactory.js
scripts
--angular.js
--ng-google-chart.js **
stylesheets
--main.css
views
--chart.html
--list.html
```
** ng-google-chart.js can be found [here](http://angular-google-chart.github.io/angular-google-chart/docs/latest/guides/getting-started/).

------
###Instructions

1. Your app must use angular
3. Use angular routing to navigate between the partial views
2. Create an angular factory (apiFactory) that uses $http to call for the json located at https://data.nashville.gov/resource/8zc7-2afq.json
3. In your chartController, use the json from the apiFactory and reformat it so that each contact_type and the number of resources of that contact_type can be fed into the addChartRows function
4. In your list.html and listController.js, you will make a list of all of the resources and the contact info from the json from the apiFactory.

####chart.html
```html
<!--add this line to create your chart-->
<div class="chart" google-chart chart="chartObject"></div> 
```

####app.js
```js
//be sure to add the google chart directive to the app in the initial declaration
var app = angular.module('nashvilleChart', ['googlechart']); 
```
####chartController.js
Include this code in your chartController and use the addChartRow function to add rows to the chart. 
```js
function addChartRow (nameOfContactType, numberOfProviders){
    var chartDatum = {
        c: [
            { v: nameOfService },
            { v: numberOfProviders }
        ]
    };
    $scope.chartObject.data.rows.push(chartDatum);
}

$scope.chartObject = {
	type: "BarChart",
	data: {
        "cols": [
            { id: "t", label: "Type of Service", type: "string" },
            { id: "s", label: "Number of Providers", type: "number" }
        ], "rows": [] //You'll be adding the rows with addChartRow
    },
    options: {
        title: "Nashville Services"
    }
}
```

------
###Notes

 - This chart is powered by [Angular Google Chart](https://github.com/angular-google-chart/angular-google-chart/)

