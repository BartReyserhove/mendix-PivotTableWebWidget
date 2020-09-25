## PivotTableWebWidget
Pivot table widget

## Features
- Use a datasource or a REST service call for the data.
- Values and labels for the X and Y axis are attributes of the entity.
- Perform actions on the data in each cell.
- React to click events on the cells.
- Apply styling thresholds to highlight certain values
- Export the table data as CSV
- When there is no data, no table will be rendered but a (configurable) text will be shown.

## Entity to use
Because non persistent entities are kept in the client state, these are not the preferred way when using a datasource. It is best to use persistent entities and make sure the objects are committed.

However, existing implementations of this widget probably use non-persistent entities because that was the preferred way for Mendix 4 thru 6.

Especially when using non-persistent entities it is best to use a web service rather than a datasource because the web service does not return Mendix objects but only JSON data.

## Usage
[step by step instructions]

## Web service
The widget can call webservices, which can improve performance, especially for larger datasets. As no Mendix objects are transferred, only JSON, the result will not impact the client state. Combining this with OQL to aggegate your data in the backend can be a great combination.

### Only to the app backend
The widget will only call services on the app backend. If you wish to use external data, make that service call in your app logic.

### Authorization
Make sure that current session is (also) allowed for the web service because the widget will use the current session to authenticate.

### Result
The service should return a list of data items in the following format:

| Element     | Req.? | Description |
|-------------|:-:|--|
| idValueX    | Y | ID value for the X axis |
| labelValueX |   | Label value for the X axis, ID value will be used if empty |
| idValueY    | Y | ID value for the Y axis |
| labelValueY |   | Label value for the Y axis, ID value will be used if empty |
| value       | ? | Value, required when Cell value action is not Count |

The values can either be strings or numbers, depending on the type of data returned. As JSON does not know about dates, a date is to be transmitted as UTC date string, format: 2020-09-15T09:53:56.771Z, the widget will process it as a date.

For ID values, it is best to format the dates in the backend as aggregation usually takes place on an entire month or year. The key is then yyyyMM or just yyyy.

The demo project has an example of the service and mappings.


## Demo project
https://testpivottablewebw-sandbox.mxapps.io/

## Issues, suggestions and feature requests
https://github.com/Itvisors/mendix-PivotTableWebWidget/issues
