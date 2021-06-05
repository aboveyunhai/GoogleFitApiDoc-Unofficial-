# GoogleFitApiDoc(Unofficial)
Personal Android/Rest Api note/example for badly written Google Fit official Doc
PR welcome

Google Playground to test Rest Api:

https://developers.google.com/oauthplayground

## Move Minute
**Name**
```
com.google.active_minutes
```
**OAuth Scope**:
```
https://www.googleapis.com/auth/fitness.activity.read
https://www.googleapis.com/auth/fitness.activity.write
```
### Rest Api: </br>
**HTTP method**:
```
POST
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

## Sleep
**Name**
```
com.google.sleep.segment
```
**OAuth Scope**:
```
https://www.googleapis.com/auth/fitness.sleep.read
https://www.googleapis.com/auth/fitness.sleep.write
```
### Rest Api: </br>
**Request url**:
```
https://www.googleapis.com/fitness/v1/users/userId/dataset:aggregate
```
**Request body**: 

Similar to **Move Minutes**
just change `"dataTypeName": "com.google.active_minutes"` to `"dataTypeName": com.google.sleep.segment` in **Request body**

**Request response**: 

Similar to **Move Minutes**, but `intVal`(from 1-6) for sleep holds its own meaning:
| Sleep stage type | Value |
| ------------- | ------------- |
| Awake (during sleep cycle) | 1 |
| Sleep | 2 |
| Out-of-bed | 3 |
| Light sleep | 4 |
| Deep sleep | 5 |
| REM | 6 |



