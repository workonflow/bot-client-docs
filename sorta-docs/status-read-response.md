## Пример ответа

```js
{ code: 200,
  message: 'OK',
  data: [ {
    color: "status color in format #c0c0c0",
    name: "name status",
    streamId: "id stream",
    teamId: "id team",
    type: "global status Wait, In progress or Done",
    workflow: "",
    _id: "status id"
  }, {
    // если запрос был по streamId то тут будут перечисленны все статусы
  }, {
    ...
  }]
}

```