# JSON - Syntaks
JSON data er baseret på javascripts objekt syntaks og er struktureret i key / value pairs.

```js
"key": "value"
```
___
### JSON objekter
I JSON indkapsles objekter med krøllede paranteser på samme måde som i javascript:
```js
{
    "name": "John"
}
```
Objekternes datasæt adskilles med komma:
```js
{
    "firstname": "Oliver",
    "lastname": "Hansen",
    "phone": 22334455
}
```
Objekter kan også have værdier med datatypen objekt:
```js
{
    "firstname": "Oliver",
    "lastname": "Hansen",
    "contact": 
        {
            "phone": 22334455,
            "email": "oliver@hansen.dk"
        }
}
```
___
### JSON arrays
I JSON indkapsles arrays med firkantede  paranteser på samme måde som i javascript:
```js
["Jan", "Bo", "Signe", "Søren"]
```
Arrays kan også indgå som værdier i et objekt:
```js
{
    "users": ["Jan", "Bo", "Signe", "Søren"]
}
```
Og omvendt kan objekter optræde som værdier i et array:
```js
{
    "users": [
        {
            "firstname": "Ole",
            "lastname": "Jensen"  
        },
        {
            "firstname": "Lis",
            "lastname": "Hansen"  
        }
    ]
}
```
___
## Test af JSON
- [Test dit json dokument](https://jsonformatter.curiousconcept.com/)
