_Application Developer tutorials_
# typescript-webpack - kendo

#### Summary
- Details on building and running this applications are **[here](https://github.com/aurelia/skeleton-navigation/blob/master/skeleton-typescript-webpack/README.md)**.

- Kendo Core and KendoUI bridge installation is defined in **[this section of the Installation document](https://aurelia-ui-toolkits.gitbooks.io/kendo-ui-sdk-installation/content/installation/installing%20kendo/advanced/core/jspm.html).** 

***

#### Details

##### Step 1. 

Add the following stylesheets to the head section of `index.html:
    ```
    <link rel="stylesheet" href="node_modules/kendo-ui-core/css/web/kendo.common.core.min.css">
    <link rel="stylesheet" href="node_modules/kendo-ui-core/css/web/kendo.default.min.css">
    ```
##### Step 2. 

Run the command **`npm install kendo-ui-core aurelia-kendoui-bridge --save`** in the console.

##### Step 3. 

Add the following import to **`main.js`**: **`import "kendo-ui-core";`**

##### Step 4. 

Add the following to `webpack.config.babel.js` following to `aurelia bundles`
    ```
    kendo: [
       'aurelia-kendoui-bridge'
    ]
    ```

##### Step 5.

Add the following to **`webpack.config.babel.ts`** file to **`generateConfig`** entry property
    ```
    'aurelia-kendoui-bridge': ['aurelia-kendoui-bridge]'
    ````

##### Step 6.

Run the following command in the console:
 ```
 typings install kendo-ui --source=dt --global
 ```
    
##### Step 7.

Add this **`autocomplete.ts`** file to the project
    ```
    import 'kendo-ui/js/kendo.autocomplete.min';

    export class autocomplete{
      constructor() {
        this.datasource = {
          transport: {
            read: {
              dataType: 'jsonp',
              url: '//demos.telerik.com/kendo-ui/service/Customers'
            }
          }
        };
      }	
    }
    ```

##### Step 8.

Add this **`autocomplete.html`** file (_note that kendo specific stylesheets are defined in index.html_)
    ```
    <template>
      <require from="aurelia-kendoui-bridge/autocomplete/autocomplete"></require>
      <require from="aurelia-kendoui-bridge/common/template"></require>
      <require from="./autocomplete.css"></require>

      <div id="example" style="margin-top: 20px; margin-left: 20px">
        <div class="demo-section k-content">
          <p><strong>Customers:</strong></p>

          <ak-autocomplete k-data-source.bind="datasource"
                          k-height.bind="400"
                          k-min-length.bind="1"
                          k-data-text-field="ContactName">
            <ak-template>
              <span class="k-state-default" style="background-image: url('http://demos.telerik.com/kendo-ui/content/web/Customers/${CustomerID}.jpg')"></span>
              <span class="k-state-default"><h3>${ContactName}</h3><p>${CompanyName}</p></span>
            </ak-template>
            <ak-template for='headerTemplate'>
              <div class="dropdown-header k-widget k-header">
                <span>Photo</span>
                <span>Contact info</span>
              </div>
            </ak-template>

            <input id="autocomplete-customizing-templates-customers" style="width: 50%"/>
          </ak-autocomplete>

          <p class="demo-hint">Start typing to find a customer. E.g. "Ann" </p>
        </div>
      </div>
    </template>
    ```

##### Step 9.

Add the `autocomplete.css` file
    ```
    .dropdown-header {
            border-width: 0 0 1px 0;
            text-transform: uppercase;
        }

        .dropdown-header > span {
            display: inline-block;
            padding: 10px;
        }

        .dropdown-header > span:first-child {
            width: 50px;
        }

        .k-item {
            line-height: 1em;
            min-width: 300px;
        }

        /* Material Theme padding adjustment*/

        .k-material .k-item,
        .k-material .k-item.k-state-hover,
        .k-materialblack .k-item,
        .k-materialblack .k-item.k-state-hover {
            padding-left: 5px;
            border-left: 0;
        }

        .k-item > span {
            -webkit-box-sizing: border-box;
            -moz-box-sizing: border-box;
            box-sizing: border-box;
            display: inline-block;
            vertical-align: top;
            margin: 20px 10px 10px 5px;
        }

        .k-item > span:first-child {
            -moz-box-shadow: inset 0 0 30px rgba(0,0,0,.3);
            -webkit-box-shadow: inset 0 0 30px rgba(0,0,0,.3);
            box-shadow: inset 0 0 30px rgba(0,0,0,.3);
            margin: 10px;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background-size: 100%;
            background-repeat: no-repeat;
        }

        h3 {
            font-size: 1.2em;
            font-weight: normal;
            margin: 0 0 1px 0;
            padding: 0;
        }

        p {
            margin: 0;
            padding: 0;
            font-size: .8em;
        }

    ```
    
##### Step 11.

Add the request to load the aurelia-kendoui-bridge plugin by adding the highlighted statement below (`.plugin('aurelia-kendoui-bridge');` to the file `main.js`

<p align=center>
  <img src="https://cloud.githubusercontent.com/assets/2712405/21959138/412ffcfc-da8c-11e6-82bd-b326e34e830d.png"></img>
</p>

##### Step 12.

Add the following line to **`app.ts`**
    
 ```
    { route: 'autocomplete',  name: 'autocomplete', moduleId: 'autocomplete', nav: true, title: 'Autocomplete' }
 ```
    
***






