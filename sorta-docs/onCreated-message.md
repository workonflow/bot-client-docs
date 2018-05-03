## Пример сообщения

#### если комментарий создали в потоке

```js
{ teamId: 'some team id',
  data: {
    id: 'comment id',
    userId: 'some user id',
    content: {
      createdAt: 1524043332761,
      type: '',
      updatedAt: 1524043332761,
      to: [],
      from: 'user id',
      metadata: { userId: 'some user id' },
      att:  [ { type: 'text', data: { text: 'some text' } } ],
      streamId: 'some stream id',
      _id: 'comment id',
    }
  }
}
```

#### если комментарий создали в задаче

```js
{ teamId: 'some team id',
  data: {
    id: 'comment id',
    threadId: 'some thread id',
    userId: 'some user id',
    content: {
      createdAt: 1524043417953,
      type: '',
      updatedAt: 1524043417953,
      to: [],
      from: 'user id',
      metadata: { userId: 'some user id' },
      att:  [ { type: 'text', data: { text: 'some text' } } ],
      threadId: 'some thread id',
      streamId: 'some stream id',
      _id: 'comment id'
    }
  }
}
```

#### в остальных случаях
```js
{ teamId: 'some team id',
  data: {
    id: 'comment id',
    content: {
      createdAt: 1524044053403,
      type: 'some comment type',
      updatedAt: 1524044053403,
      to: [],
      from: '',
      metadata: [Object],
      att: [],
      threadId: 'thread id if comment in thread',
      streamId: 'stream id if comment in stream',
      _id: 'comment id',
      __v: 0 } },
}
```