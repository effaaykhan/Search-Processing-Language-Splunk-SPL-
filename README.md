# Search-Processing-Language-Splunk-SPL-
- Search Processing Language (SPL) is used to make the search more effective. It comprises various functions and commands used together to form complex yet effective search queries to get optimized results.
- Splunk Search Processing Language comprises of multiple functions, operators and commands that are used together to form a simple to complex search and get the desired results from the ingested logs. Main components of SPL are explained below:

## ➡️﻿Search Field Operators

Splunk field operators are the building blocks used to construct any search query. These field operators are used to filter, remove, and narrow down the search result based on the given criteria. Common field operators are Comparison operators, wildcards, and boolean operators.

  - ### Comparison Operators
    - Equal       ```=```: 	This operator is used to match values against the field. In this example, it will look for all the events, where the value of the field UserName is equal to Mark.
         - example: ```UserName=Mark```
    - Not Equal to ```!=```: This operator returns all the events where the UserName value does not match Mark.
         - example: ```UserName!=Mark```
    - Less Than   ```<```: Showing all the events with the value less than any value.
         - example: ```Age<10```
    - Less Than or Equal to ```<=```: Showing all the events with the value less than or equal to value.
         - example: ```Age<=10```
    - Greater Than ```>```: This will return all the events where the Outbound traffic value is over 50 MB.
         - example: ```outbound_traffic>50```
    - Greater Than or Equal to: ```>=```: This will return all the events where the Outbound traffic value is greater or equal to 50 MB.
         - example: ```outbound_traffic>=50```

  - ### Boolean Operators
    - ```NOT``` : Ignore the events from the result where field_A contain the specified value.
         - example: ```field_A NOT value```
    - ```OR```  : Return all the events in which field_A contains either value1 or value2.
         - example: ```field_A=value1 OR field_B=value2```
    - ```AND```: Return all the events in which field_A contains value1 and field_B contains value2.
         - example: ```field_A=value1 OR field_B=value2```
     
  - ### Wild Card
    - Splunk supports wildcards to match the characters in the strings.
    - "Wildcard Symbol" ```*```: It will return all the results with values
       - example: ```status=fail*``` will return ```status=failed``` or ```status=failure```
  
## ➡️﻿ Filtering the results in SPL
- Our network generates thousands of logs each minute, all ingesting into our SIEM solution. It becomes a daunting task to search for any anomaly without using filters. SPL allows us to use Filters to narrow       down the result and only show the important events that we are interested in. We can add or remove certain data from the result using filters. The following commands are useful in applying filters to the 
  search results.
  - ```field```: Fields command is used to add or remove mentioned fields from the search results. To remove the field, minus sign ```-``` is used before the fieldname and plus ```+``` is used before the fields 
                 which we want to display.
      - example:
           ```
           fields + HostName - EventID
           ```
  - ```search```: This command is used to search for the raw text while using the chaining command ```|```
    
      - example:
           ```
           |search powershell
           ```
  - ```dedup```: Dedup is the command used to remove duplicate fields from the search results. We often get the results with various fields getting the same results. These commands remove the duplicates to show 
                 the unique values.
    
      - example:
           ```
           |dedup EventID
           ```
  - ```rename```: It allows us to change the name of the field in the search results. It is useful in a scenario when the field name is generic or log, or it needs to be updated in the output.
    
      - example:
           ```
           |rename User as Employees
           ```

## ➡️﻿ Structuring the search results
- SPL provides various commands to bring structure or order to the search results. These sorting commands like ```head```, ```tail```, and ```sort``` can be very useful during logs investigation. These  
  ordering commands are explained below:
  - table: Each event has multiple fields, and not every field is important to display. The Table command allows us to create a table with selective fields as columns.
    
    - example:
         ```
         index=windowslogs | table EventID Hostname SourceName
         ```
  - ```head```: The head command returns the first 10 events if no number is specified.
    
    - example:
        ```
        index=windowslogs |  table _time EventID Hostname SourceName | head 5
        ```
  - ```tail```: The Tail command returns the last 10 events if no number is specified.
    
    - example:
         ```
         index=windowslogs |  table _time EventID Hostname SourceName | tail 5
         ```
  - ```sort```: The Sort command allows us to order the fields in ascending or descending order.
    
    - example:
         ```
          index=windowslogs |  table _time EventID Hostname SourceName | sort Hostname
         ```
  - ```reverse```: The reverse command simply reverses the order of the events.

     - example:
          ```
          index=windowslogs | table _time EventID Hostname SourceName | reverse
          ```
