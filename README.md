# stm_metro_bus_connection

This work attempts to answer the question: "What is the probabiltiy of missing an STM Bus transfer from a metro station?

The motivation is me missing my bus connections often when taking metro+bus, or having to run out of the station to catch the bus before departing. This gets worse at night, when the next bus arrives after a while.

Before executing the notebook, you should download the latest STM GTFS from [here](https://www.stm.info/sites/default/files/gtfs/gtfs_stm.zip) for the schedules.

### Preprocessing steps:
- Isolating metro stations (technically, their stop ids).
- Matching the closest bus stops to those stations using GeoPandas. This is verified using the test function <code>test_match_bus_to_metro</code>.
- Filtering services in calendar.txt so that we make sure bus and metro schedules are happening on the same days. We filter to weekday services and in a specifc time window of validity.

### Matching steps per station:
- For each metro arrival, we match:
  - The closest overall bus departure, and the next departure of the same bus
  - The closest bus departure and next same bus departure for each bus route passing through the station and each direction of that route.

### Metrics for each station
- <code>get_proba_missing_bus</code> -> Overall probability of missing the closest bus after the metro arrival
- <code>get_proba_missing_bus_daily</code> -> Hourly probability of missing the closest bus after the metro arrival, we apply it for all buses and per bus route+direction.
- <code>plot_latency_distribution</code> -> Distribution of time it takes between the metro arrival and the closest bus departure
- <code>get_proba_missing_bus_daily_per_metro_direction</code> -> Same as <code>get_proba_missing_bus_daily</code> but with each metro direction isolated.
- <code>get_average_wait_time_for_next_departure</code> -> Calculate the average wait time for next departures in case of missing a transfer.
- <code>plot_wait_times_for_next_departure</code> -> Plot the wait time distribution for next departures in case of missing a transfer.
