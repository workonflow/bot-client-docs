## Пример ответа

```js
 { code: 200,
  message: 'OK',
  data: [ {
    _id: 'thread id',
    archived: false,
    createdAt: 1524055334667,
    customFields: [],
    deadline: [],
    responsibleUserId: '',
    status: 'status id',
    streamId: 'stream id',
    teamId: 'team id',
    title: 'title name',
    customerId: 'id customer',
    customerIds: [],
    commentsFilter: {},
    type: '',
    roles: [responsible list],
    updatedAt: 1524056052883,
    position: -1900
  }, {
    если в запросе был указан statusId или streamId то тредов будет несколько
  }, {
    ...
  }]
}
```