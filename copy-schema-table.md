# COPY SCHEMA TABLE

````  
SELECT * INTO DestinationTableName FROM SourceTableName
````  

## Copy structure only (copy all the columns)
````  
SELECT Top 0 * INTO NewTable FROM OldTable
````  
## Copy structure only (copy some columns)
````  
SELECT Top 0 Col1,Col2,Col3,Col4,Col5 INTO NewTable FROM OldTable
````  
## Copy structure with data
````  
SELECT * INTO NewTable FROM OldTable
````  
## If you already have a table with same structure and you just want to copy data then use this
````  
INSERT INTO NewTable SELECT * FROM OldTable
````
