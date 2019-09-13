##### Notes for the chapter The Data Analysis Process


##### Quick notes on SQL
* what is the difference between rank, dense rank and row number?
  * Order By clause is must in all the 3 cases.
  
  * **row number** : gives unique number to the rows for a SELECT query. Always sequential.
  * **rank** : gives the same rank number for the duplicate rows of the column in orderby clause but it will skip the rank for the number of duplicated records. (1,1,1,4,4,6)
  * **dense rank** : gives the same rank number for the duplicate rows in the order by clause column but does not skips the rank. The values will be continuous ( 1,1,1,1,2,3,4,5)
