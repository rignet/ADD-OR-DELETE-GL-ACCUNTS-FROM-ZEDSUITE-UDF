# ADD OR DELETE GL ACCUNTS FROM ZEDSUITE UDF ( Column ID = U_V33_GLact)

# Description
>
> sentence to update GL account field on zedsuite to add or delete an account from the chose from list objects 

## Execution methods

> Can be run it on SAP B1 query manager or SQL Studio. 

## Config Location

> the configuration tables are in R101, this configuration tables affect all the entities, (one ring to rules all!!!)

## Method type

> UPDATE STAMENT


## Fields and Tables on SAP B1 

#### ZED_FMSReplacement Table

> Field               | Table                  | type        | Size  |Description                             |
> --------------------|------------------------|-------------|-------|----------------------------------------|
> ID                  | ZED_FMSReplacement     | int         |   11  |Unique ID on table                      |
> LegalEntity         | ZED_FMSReplacement     | nvarchar    |   254 |Entiti DB                               |
> FormType            | ZED_FMSReplacement     | nvarchar    |   15  |From Code on SAP                        |
> ItemId              | ZED_FMSReplacement     | nvarchar    |   15  |Item Id of the form                     |
> ColumnID            | ZED_FMSReplacement     | nvarchar    |   30  |Column id on matrix                     |
> DependingOn         | ZED_FMSReplacement     | nvarchar    |  254  |Condition case to be use                |
> Definition          | ZED_FMSReplacement     | ntext       |   -   |Definition to show                      |
> Definition Type     | ZED_FMSReplacement     | nvarchar    |    4  |Type of Definition                      |
> Definiton Object    | ZED_FMSReplacement     | nvarchar    |   30  |Definition object   (1)                 |
> Definition Alias    | ZED_FMSReplacement     | nvarchar    |   30  |Definition Alias option  (field on SAP) |
> Definition Values   | ZED_FMSReplacement     | nvarchar    |   15  |default values to be show on the field  |

> # GUIDE or Steps to follow

> Add a GL Account code to the GL Account Detail field on the Purchase Request Detail matrix

#### 1. Check the id field to be updated

> use this query to find the id's to be updated (Field = ID) for this case must be id's 4 and 89
> use the condition and the column id to determinate the rows to be update
> DependingOn = U_V33_USE in (Consumable, Cons) and ColumnID = U_V33_GLact
``` 
select * from ZED_FMSReplacement where ColumnId = 'U_V33_GLact' and DependingOn = 'U_V33_USE in (Consumable, Cons)'

``` 
#### 2. this query will return two values

> this query will return two values , one for alll entities and other for R801 because the last one have a diferent configuration.

#### 3. run the update statment base on the ID's of the last steps

> Sample : we want to add the GL Account code 32421 to the Chose fromo list on the GL field on the PR matrix, so we add to the Definition field list (string) the  **or FormatCode=''32421''** and them execute the query 
> Sample : to take it off one of the account just delte the **or FormatCode=''32421''** of the account you want and excecute the update statement

```
UPDATE ZED_FMSReplacement SET Definition = 'FormatCode=''21720'' or FormatCode=''21750'' or FormatCode=''71101'' or FormatCode=''71110'' or FormatCode=''71120'' or FormatCode=''71130'' or FormatCode=''71151'' or FormatCode=''71171'' or FormatCode=''71201'' or FormatCode=''71251'' or FormatCode=''71301'' or FormatCode=''71351'' or FormatCode=''71353'' or FormatCode=''71360'' or FormatCode=''71401'' or FormatCode=''71451'' or FormatCode=''71501'' or FormatCode=''71502'' or FormatCode=''71505'' or FormatCode=''71551'' or FormatCode=''71601'' or FormatCode=''71602'' or FormatCode=''71611'' or FormatCode=''71612'' or FormatCode=''71651'' or FormatCode=''71681'' or FormatCode=''71701'' or FormatCode=''71702'' or FormatCode=''71703'' or 
FormatCode=''71704'' or FormatCode=''71705'' or FormatCode=''71706'' or FormatCode=''71707'' or FormatCode=''71708'' or FormatCode=''71709'' or FormatCode=''71710'' or FormatCode=''71711'' or FormatCode=''71712'' or FormatCode=''71713'' or FormatCode=''71714'' or FormatCode=''71715'' or FormatCode=''71720'' or FormatCode=''71721'' or FormatCode=''71722'' or FormatCode=''71723'' or FormatCode=''71724'' or FormatCode=''71725'' or FormatCode=''71726'' or FormatCode=''71730'' or FormatCode=''71731'' or FormatCode=''71732'' or FormatCode=''71733'' or FormatCode=''71734'' or FormatCode=''71735'' or FormatCode=''71751'' or FormatCode=''71752'' or FormatCode=''71755'' or FormatCode=''71801'' or 
FormatCode=''71810'' or FormatCode=''71820'' or FormatCode=''71851'' or FormatCode=''71901'' or FormatCode=''71902'' or FormatCode=''71903'' or FormatCode=''71904'' or FormatCode=''71905'' or FormatCode=''71906'' or FormatCode=''71910'' or FormatCode=''71911'' or FormatCode=''71920'' or FormatCode=''71998'' or FormatCode=''71999'' or FormatCode=''73101'' or FormatCode=''73102'' or FormatCode=''73103'' or FormatCode=''73104'' or FormatCode=''73105'' or FormatCode=''73106'' or FormatCode=''73107'' or FormatCode=''73108'' or FormatCode=''73109'' or FormatCode=''73510'' or FormatCode=''73520'' or FormatCode=''73521'' or FormatCode=''73530'' or FormatCode=''73531'' or FormatCode=''73532'' or 
FormatCode=''73540'' or FormatCode=''73541'' or FormatCode=''73542'' or FormatCode=''73543'' or FormatCode=''73550'' or FormatCode=''73560'' or FormatCode=''73561'' or FormatCode=''73570'' or FormatCode=''73571'' or FormatCode=''73580'' or FormatCode=''73590'' or FormatCode=''73593'' or FormatCode=''73599'' or FormatCode=''74101'' or FormatCode=''74102'' or FormatCode=''74103'' or FormatCode=''74104'' or FormatCode=''74105'' or FormatCode=''74106'' or FormatCode=''74107'' or FormatCode=''74108'' or FormatCode=''74109'' or FormatCode=''74110'' or FormatCode=''74111'' or FormatCode=''74112'' or FormatCode=''74113'' or FormatCode=''74114'' or FormatCode=''74120'' or FormatCode=''74121'' or 
FormatCode=''74122'' or FormatCode=''74123'' or FormatCode=''74130'' or FormatCode=''74131'' or FormatCode=''74180'' or FormatCode=''74181'' or FormatCode=''74182'' or FormatCode=''74183'' or FormatCode=''74184'' or FormatCode=''74201'' or FormatCode=''74251'' or FormatCode=''74252'' or FormatCode=''74253'' or FormatCode=''74290'' or FormatCode=''74301'' or FormatCode=''74401'' or FormatCode=''74402'' or FormatCode=''74403'' or FormatCode=''74404'' or FormatCode=''74405'' or FormatCode=''74406'' or FormatCode=''74407'' or FormatCode=''74411'' or FormatCode=''74421'' or FormatCode=''74422'' or FormatCode=''74431'' or FormatCode=''74441'' or FormatCode=''74501'' or FormatCode=''74502'' or 
FormatCode=''74503'' or FormatCode=''74504'' or FormatCode=''74505'' or FormatCode=''74506'' or FormatCode=''74507'' or FormatCode=''74508'' or FormatCode=''74580'' or FormatCode=''74601'' or FormatCode=''74602'' or FormatCode=''74603'' or FormatCode=''74604'' or FormatCode=''74605'' or FormatCode=''74701'' or FormatCode=''74702'' or FormatCode=''74703'' or FormatCode=''74704'' or FormatCode=''74710'' or FormatCode=''74751'' or FormatCode=''74780'' or FormatCode=''74801'' or FormatCode=''74901'' or FormatCode=''74902'' or FormatCode=''74903'' or FormatCode=''74904'' or FormatCode=''74910'' or FormatCode=''74911'' or FormatCode=''74912'' or FormatCode=''74920'' or FormatCode=''74950'' or 
FormatCode=''74980'' or FormatCode=''75101'' or FormatCode=''75102'' or FormatCode=''79001'' or FormatCode=''79999'' or FormatCode=''81101'' or FormatCode=''82201'' or FormatCode=''82301'' or FormatCode=''82401'' or FormatCode=''82402'' or FormatCode=''32421'' ' 
WHERE ID IN  ('89','4')
```
#### 4. Check the changes

#### 5. End



update by kenneth : wowwww 
