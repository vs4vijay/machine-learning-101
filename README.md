```javascript
For each CS in CS_List {

    # In case of Never Ending
    if(CS.End_datetime == null) {
        
        # In case of "YEARLY"
        if(CS.type == "YEARLY") {
            if(DAY_MONTH(CS.start_datetime) == DAY_MONTH(Cleaning_end_time) ) {
                # Do Nothing
            } else {
                # Continue to next CS
                continue
            }
        } else {
            # In case of "DAILY", "WEEKLY" and "MONTHLY"

            # This “Cleaning_end_time” is already converted into Timezone Aware object,           hence get the weekday only.
            Week_day = Get Week Day of Cleaning_end_time

            if(CS.days.contains(Week_day)) {

                # In case of "MONTHLY"
                Month_week = Get Which Week of Month from Cleaning_end_time

                if(CS.type == "MONTHLY") {
                    if(CS.week_in_month == Month_week) {
                        # Do Nothing
                    } else {
                        # Continue to next CS
                        continue
                    }
                } else {
                    # Do Nothing for "DAILY" and "WEEKLY"
                }
            }
        }

        # Check "end_time" for frequencies
        For each Frequency in CS.frequencies {
            if(Cleaning_start_time <= Frequency.end_time <= Cleaning_end_time) {
                # Consider this CS for returning rooms
            }
        }

    } else {

        # Does Not Repeat (Not Never Ending Case)
        # Just check if cleaning_end_time is in between Cleaning Schedules span

        if(CS.start_datetime <= Cleaning_end_time <= CS.end_datetime) {
            # Check for each frequency as above
        }
    }
}
```
