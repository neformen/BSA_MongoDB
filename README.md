# BSA2017 : MongoDB

## Написать запрос для поиска всех студентов, у которых score > 87% и < 93% по любому из типов выполненных заданий:

```javascript
db.student.find({ $or: [
    { 'scores.0.score': { $gt: 87, $lt: 93 }}, 
    { 'scores.1.score': {$gt: 87, $lt: 93 }}, 
    { 'scores.2.score': {$gt: 87, $lt: 93 }}, 
    { 'scores.3.score': {$gt: 87, $lt: 93 }}
]});
```

## Написать запрос-агрегацию для выборки всех студентов, у которых результат по экзамену (type: "exam") более 90% (использование unwind):

```javascript
db.student.aggregate([
    { $unwind: "$scores" },
    { $match: {
        $and:[
            { "scores.type": "exam"},
            {"scores.score": {$gt: 90}}
        ]}
    }
]);
```



## Студентам с именем Dusti Lemmond добавить поле “accepted” со значением true:

```javascript
db.student.update({name: "Dusti Lemmond"}, {$set: {accepted: "true"}}, {multi: true});
```