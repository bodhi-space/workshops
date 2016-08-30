# Transaction Service





## getDriversByInterval

/concept/store/getDriversByInterval?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&volume_type=TABLE&data_type=ACTUAL


````
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getDriversByInterval?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&volume_type=TABLE&data_type=ACTUAL"
````




## getGuestCounts

/concept/store/getGuestCounts?start_date=YYYY-MM-DDT00:00:00&end_date=YYYY-MM-DDT00:00:00"

```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getGuestCounts?start_date=2016-04-30T00:00:00&end_date=2016-05-03T00:00:00"
```



## getVolumeCounts

/concept/store/getVolumeCounts?start_date=YYYY-MM-DDT00:00:00&end_date=YYYY-MM-DDT00:00:00&volume_type=TABLE

```
curl -X GET -H "Content-Type:application/json" -u U:P "https://api.bodhi.space/namespace/controllers/vertx/hotschedules/1/1/getVolumeCounts?start_date=2015-04-30T00:00:00&end_date=2016-05-03T00:00:00&volume_type=TABLE"
```

## Set Guest Count


## Set Volume Count

