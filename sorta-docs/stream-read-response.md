## Пример ответа

```js
{ code: 200,
  message: 'OK',
  data: [ {
    _id: 'stream id',
    name: 'stream name',
    roles: [Array responsible users],
    threadStatuses: [Array statuses],
    visibility: [],
    seenBy: {},
    settings: [{
      widgets: {
        DataTime: { on: true, options: 'deadline', type: 'DataTime' },
        Priority: { on: true, type: 'Priority' },
        Responsible: { on: true, type: 'Responsible' },
        WorkflowStatus: { on: true, type: 'WorkflowStatus' },
        StreamSelect: { on: true, type: 'StreamSelect' },
        Customers: { type: 'Customers', on: true },
        Points: { type: 'Points', on: true }
      },
      notify: {}
    }],
    teamId: 'team id',
    index: 1516360789475,
    owner: 'id creator stream',
    isPrivate: true,
    createdAt: 1516360789475,
    updatedAt: 1516360789475,
    admins: [id admin list]
  } ]
}

```