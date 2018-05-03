## Пример ответа

```js
 { code: 200,
  message: 'OK',
  data: [{
    accountId: "channel id",
    attachments: [],
    cc: null,
    conversationId: "conversation id",
    date: "create date", // example format Fri, 20 Apr 2018 11:53:18 +0300
    from: "ereskoe@list.ru",
    headers: "header",
    html: "html mail",
    inReplyTo: null,
    messageId: "message id in mail client format", // example <1524214398.529320890@f338.i.mail.ru>
    name: "contact name",
    receivedDate: "date response mail", // example format Fri, 20 Apr 2018 11:53:18 +0300
    references: null,
    streamId: "",
    subject: "subject title mail",
    teamId: "team id",
    text: "text mail",
    threadId: "thread id",
    to: "channel mail",
    type: "incoming",
    _id: "conversation id",
  }, {
    // если запрос был по ids, вернёт несколько елементов
  }, {
    ...
  }]
}
```