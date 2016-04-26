#Angular, APIs, and Charts

This project will be a basic Angular application that queries a open dataset from data.Nashville.gov and creates a chart and a list view.

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
--chart.js
stylesheets
--main.css
views
--chart.html
--list.html


```

------
###Instructions

1. Your app must use angular.
2. This app has a parent page (index.html) and two partial views (chart.html and list.html)
3. Use angular routing to navigate between the views.
2. Create an angular factory (apiFactory) that uses $http to call for the json located at https://data.nashville.gov/resource/8zc7-2afq.json
3. In your chartController, you need to get the json from the apiFactory and reformat it so that each contact_type and the number of resources of that contact_type can be fed into the addChartRows function
4. In your list.html and listController.js, you will make a list of all of the resources and the contact info from the json you get from the apiFactory.

####chart.html
```html
//add this line to create your chart
<div class="chart" google-chart chart="chartObject"></div> 
```

####app.js
```js
//be sure to add the google chart directive to the app in the initial declaration
var app = angular.module('nashvilleData', ['googlechart']); 
```
####chartController.js
Include this code in your chartController and use the addChartRow function to add rows to the chart. 
```js
function addChartRow (nameOfService, numberOfProviders){
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

 - This charts is powered by [Angular Google Chart](https://github.com/angular-google-chart/angular-google-chart/)
