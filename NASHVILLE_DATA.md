#Nashville Data

##Angular, APIs, and Charts

For this project, you must use Angular, and the [Angular Google Chart](http://angular-google-chart.github.io/angular-google-chart/docs/latest/guides/getting-started/) library to create a chart based on data from [data.Nashville.gov](data.nashville.gov).

------
###Setup
```
mkdir -p ~/workspace/exercises/rich-browser/nashvilledata && cd $_
```

Use *npm* to install Angular and charting library.

```bash
npm install angular angular-route angular-google-chart@0.1.0 --save
```

------
###Instructions

1. Use Angular routing to create two partials for the application.
    1. A chart partial that shows the different types of community resources available (listed under the contact_type in the JSON resource) and the number of resources available of each type.
    1. A list partial that shows the name (contact), type (contact_type), phone number, and notes, if any, for each resource. 
1. Create a factory that uses the `$http` module in Angular to retrieve the JSON located at https://data.nashville.gov/resource/8zc7-2afq.json
1. In a controller, use the JSON from the factory and reformat it so that each `contact_type` and the number of resources of that contact_type can be fed into the addChartRows function.
1. In your list.html and listController.js, you will make a list of all of the resources and the contact info from the json from the apiFactory.

##### Example chart partial

```html
<!-- Add this line to create your chart-->
<div class="chart" google-chart chart="chartObject"></div> 
```

##### Example `app.js`

```js
// Be sure to add the google chart directive to the app in the initial declaration
var NashvilleChart = angular.module('nashvilleChart', ['googlechart']); 
```

##### Example controller

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

