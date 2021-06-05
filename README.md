# GoogleFitApiDoc(Unofficial)
Personal Android/Rest Api note/example for badly written Google Fit official Doc
PR welcome

## Move Minute
**Name**
```
com.google.active_minutes
```
### Rest Api: </br>
**OAuth Scope**:
```
https://www.googleapis.com/auth/fitness.activity.read
https://www.googleapis.com/auth/fitness.activity.write
```
**Request url**:
```
https://www.googleapis.com/fitness/v1/users/userId/dataset:aggregate
```
**Request body**:
```js
{
  "aggregateBy": [
    {
      "dataTypeName": "com.google.active_minutes"  // <===this is where you use the Name
    }
  ],
  "endTimeMillis": 1622849926000,
  "startTimeMillis": 1622504326000,
   // sperate your data by bucket, this can affect your data accuracy
   // E.g. one data can be divided into multiple
  "bucketByTime": { "durationMillis": 86400000 },
}
```
**Request response**:
```js
{
  "bucket": [
    // valid data
    {
      "startTimeMillis": "1622504326000", 
      "endTimeMillis": "1622590726000", 
      "dataset": [
        {
          "dataSourceId": "derived:com.google.active_minutes:com.google.android.gms:aggregated", 
          "point": [
            {
              "startTimeNanos": "1622574300000000000", 
              "originDataSourceId": "derived:com.google.step_count.delta:com.google.android.gms:estimated_steps", 
              "endTimeNanos": "1622586000000000000", 
              "value": [
                {
                  "mapVal": [], 
                  "intVal": 72 // this is the move minute value
                }
              ], 
              "dataTypeName": "com.google.active_minutes"
            }
          ]
        }
      ]
    },
    //example of empty data you might want to filter out
    {
      "startTimeMillis": "1622763526000", 
      "endTimeMillis": "1622849926000", 
      "dataset": [
        {
          "dataSourceId": "derived:com.google.active_minutes:com.google.android.gms:aggregated", 
          "point": []
        }
      ]
    }
  ]
}
```
