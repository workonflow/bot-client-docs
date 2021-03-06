## workonflow-bot-client ##

#### Translation
 - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) [Russian](./translation/ru/ru.md)

#### Installation

```js
$ npm install workonflow-bot-client

const botConnect = require('workonflow-bot-client').connect

const creds = {
  email: "you email",
  password: "you password"
}

const botClient = await botConnect(creds)
```

### Instructions for use ###

```js
const botClient = await botConnect(creds)

const { comment } = botClient

comment.onDirect(async message => {
  console.log('ON_DIRECT', message)
  const { teamId } = message
  const to = message.data.content.from

  const att = [{ type: 'text', data: { text: "text for response" } }]
  const resp = await comment.create(teamId, { to, att })
  console.log('resp', resp)
})
```

|[comment](#comment)                           |[contact](#contact)                           |[status](#status)                        |[stream](#stream)                                     |[team](#team)                                                     |[thread](#thread)                                             |
|---|---|---|---|---|---|
|[count](#user-content-comment-conunt)         |[create](#user-content-contact-create)        |[create](#user-content-status-create)    |[create](#user-content-stream-create)                 |[getAccesses](#user-content-team-get-accesses)                    |[create](#user-content-thread-create)                         |
|[create](#user-content-comment-create)        |[getLocale](#user-content-contact-get-locale) |[read](#user-content-status-read)        |[deleteUser](#user-content-stream-delete-user)        |[inviteUser](#user-content-team-invite-user)                      |[onBudgetUpdated](#user-content-thread-on-budget-updated)     |
|[onCreated](#user-content-comment-on-created) |[read](#user-content-contact-read)            |[setName](#user-content-status-set-name) |[delete](#user-content-stream-delete)                 |[onAdminStatusGiven](#user-content-team-on-admin-status-given)    |[onCreated](#user-content-thread-on-created)                  |
|[onDirect](#user-content-comment-on-direct)   |                                              |                                         |[onUserDeleted](#user-content-stream-on-user-deleted) |[onAdminStatusRevoked](#user-content-team-on-admin-status-revoked)|[onDeadlineUpdated](#user-content-thread-on-deadline-updated) |
|[onEcho](#user-content-comment-on-echo)       |                                              |                                         |[onUserSet](#user-content-stream-on-user-set)         |[onUserInvited](#user-content-team-on-user-invited)               |[onStatusUpdated](#user-content-thread-status-updated)        |
|[onMention](#user-content-comment-on-mention) |                                              |                                         |[read](#user-content-stream-read)                     |[onUserRemoved](#user-content-team-on-user-removed)               |[readDescription](#user-content-thread-read-description)      |
|[read](#user-content-comment-read)            |                                              |                                         |[setAdmin](#user-content-stream-set-admin)            |[read](#user-content-team-read)                                   |[read](#user-content-thread-read)                             |
|                                              |                                              |                                         |[setName](#user-content-stream-set-name)              |                                                                  |[setBudget](#user-content-thread-set-budget)                  |
|                                              |                                              |                                         |[setUser](#user-content-stream-set-user)              |                                                                  |[setDeadline](#user-content-thread-set-deadline)              |
|                                              |                                              |                                         |[setDescription](#user-content-stream-set-description)|                                                                  |[setDescription](#user-content-thread-set-description)        |
|                                              |                                              |                                         |                                                      |                                                                  |[setPriority](#user-content-thread-set-priority)              |
|                                              |                                              |                                         |                                                      |                                                                  |[setResponsible](#user-content-thread-set-responsible)        |
|                                              |                                              |                                         |                                                      |                                                                  |[setStatus](#user-content-thread-set-status)                  |
|                                              |                                              |                                         |                                                      |                                                                  |[setStream](#user-content-thread-set-stream)                  |
|                                              |                                              |                                         |                                                      |                                                                  |[setTitle](#user-content-thread-set-title)                    |
|                                              |                                              |                                         |                                                      |                                                                  |[addCustomers](#user-content-thread-add-customers)            |
|                                              |                                              |                                         |                                                      |                                                                  |[removeCustomers](#user-content-thread-remove-customer)       |

| [file](#file)           |[mail](#mail)                      |[telephony](#telephony)              |
|---|---|---|
| [getGETUrl](#getGETUrl) |[getAccounts](#user-content-mail-get-accounts)|[create-user](#telephony-create-user)|
| [getPUTUrl](#getPUTUrl) |[onReceived](#user-content-mail-on-received)  |[delete-user](#telephony-delete-user)|
|                         |[onSent](#user-content-mail-on-sent)          |[get-user](#telephony-get-user)      |
|                         |[read](#user-content-mail-read)               |[update-user](#telephony-update-user)|
|                         |[send](#user-content-mail-send)               |                                     |

----------
### Comment

#### Methods for working with comments

```js
const botClient = await botConnect(creds)
const { comment } = botClient
```
#### <a name="user-content-comment-conunt">comment.count</a>

Method for obtaining the quantity of comments

```js
const { comment } = botClient
const query = { threadId }
const response = await comment.count(teamId, query)
console.log(response) // { code: 200, message: 'OK', count: 1 }
```

Where a query may take one following attributes:
- **threadId** - ID of a task;
- **threadIds** - an array of several task IDs;
- **streamId** - ID of a stream;
> Example response
```js
{ code: 200, message: 'OK', count: 1 }
```

<div style="border:1px,solid;"></div>

#### <a name="user-content-comment-create">comment.create</a>

Method for creating comments

```js
const { comment } = botClient
const query = { threadId }
const response = await comment.create(teamId, query)
console.log(response)
```

Where a query may take the parameters:
- **streamId** - ID of a stream (for publishing comments in the general stream chat);
- **threadId** - ID of a task (for publishing comments within a thread);
- **to** - ID of a user within the system. This might also be an array of user IDs (the **to** field is used for **direct messages**);
- **att** - Takes text or an array such as: [{ type: 'text' data: { text: 'string' } }] (**type** - the message type, for example a *text*, *file*. **data** - an object with text or a file ID)

> Example response
```js
{ code: 200, message: 'OK', data: {id: 'comment id'} }
```

#### <a name="user-content-comment-on-created">comment.onCreated</a>

Method for finding created comments

```js
const { comment } = botClient
const cb = message => {
  console.log(message)
}
await comment.onCreated(cb)
```
> View an example notification [here](./sorta-docs/onCreated-message.md)

#### <a name="user-content-comment-on-direct">comment.onDirect</a>

Method for capturing comments created in bot direct messages

```js
const { comment } = botClient
const cb = message => {
  console.log(message)
}
await comment.onDirect(cb)
```

> View an example notification [here](./sorta-docs/onDirect-message.md)

#### <a name="user-content-comment-on-echo">comment.onEcho</a>

Method for testing bot functionality

Upon receiving a direct message with the tag /echo, botClient automatically answers with a duplicate of the original message.

#### <a name="user-content-comment-on-mention">comment.onMention</a>

Method for capturing comments created where a bot is mentioned

```js
const { comment } = botClient
const cb = message => {
  console.log(message)
}
await comment.onMention({keepBotRef: true}, cb)
```
The method cuts out the bot mention. If the parameter { keepBotRef: true } is indicated, the method returns the entire message including the bot mention.

> View an example notification [here](./sorta-docs/onMention-message.md)

#### <a name="user-content-comment-read">comment.read</a>

Method for obtaining comments

```js
const { comment } = botClient
const query = { id }
const response = await comment.read(teamId, query)
console.log(response
```
Where a query may take the following parameters:
- **id** - Comment ID (returns comment)
- **streamId** - ID of stream (returns the last 100 comments of a stream)
- **threadId** - ID of task (returns the last 100 comments of a thread)
- **skip** - Additional parameter indicating the number of comments necessary to skip
- **type** - Additional parameter indicating the type of comment

> View an example response [here](./sorta-docs/comment-read-response.md)

-------------

### contact

#### Methods for working with contacts and users

```js
const botClient = await botConnect(creds)
const { contact } = botClient
```
#### <a name="user-content-contact-create">contact.create</a>

Method for creating a contact

```js
const { contact } = botClient
const query = {
  basicData: {name: "new name customer"}
  customFields: [
    {id: "B1R5NTS3z", label: "Company", value: "", type: "company"},
    {id: "B1l094TB2M", label: "Work phone", value: "", type: "phone"},
    {id: "rkbA9VTH3M", label: "Work e-mail", value: "", type: "email"}
  ]
}
const response = await contact.create(teamId, query)
console.log(response)
```
Where a query may take the parameters:
- **basicData** - Takes an object with the name of the contact
- **customFields** - Field for adding channels to the contact

> Example response
```js
{
  code: 200,
  message: 'OK',
  data: { insertedCount: 1, insertedId: 'new contact id' }
}
```

#### <a name="user-content-contact-get-locale">contact.getLocale</a>

Method for determining the user’s language

```js
const { contact } = botClient
const query = { id: 'user id' }
const response = await contact.getLocale(teamId, query)
console.log(response)
```

> Example response
```js
{ code: 200, message: 'OK', data: { locale: 'en' } }
```

#### <a name="user-content-contact-read">contact.read</a>

Method for acquiring users

```js
const { contact } = botClient
const query = { id: 'user id' }
const response = await contact.read(teamId, query)
console.log(response)
```
Where a query may be::
- **id** - Contact or user ID
- **ids** - Several contact or user IDs

> View an example response [here](./sorta-docs/contact-read-response.md)

------------


### Status

#### Methods for working with stream status

```js
const botClient = await botConnect(creds)
const { status } = botClient
```
#### <a name="user-content-status-create">status.create</a>

Method for creating stream status

```js
const { status } = botClient
const query = {
  name: 'new status name',
  streamId: 'id stream',
  type: 'Done',
  color: 'randomColor()'
}
const response = await status.create(teamId, query)
console.log(response)
```

Where a query may take the following parameters:
- **color** - Color of status (we typically use the [randomColor](https://www.npmjs.com/package/randomcolor) library for this or an color in the format: #c0c0c0)
- **name**- name of status
- **streamId** - ID of stream in which status is being created
- **type** - A global status: *Wait*, *In progress*, *Done*

> Example response
```js
{code: 200, message: "Ok", data: "id new status"}
```

#### <a name="user-content-status-read">status.read</a>

Method for obtaining a status

```js
const { status } = botClient
const query = { id: statusId }
const response = await status.read(teamId, query)
console.log(response)
```
Where a query may take the following parameters:
- **id** - Status ID
- **streamId** - ID of the stream from which to receive status

> View an example response [here](./sorta-docs/status-read-response.md)

#### <a name="user-content-status-set-name">status.setName</a>

Method for changing the name of a status

```js
const { status } = botClient
const query = { id: statusId, name: 'new status name' }
const response = await status.setName(teamId, query)
console.log(response)
```
Where a query may take the following parameters:
- **id** - ID of status
- **name** - New name of status

> View an example response [here](./sorta-docs/status-set-name-response.md)

-----------


### Stream

#### Methods for working with streams

```js
const botClient = await botConnect(creds)
const { stream } = botClient
```

#### <a name="user-content-stream-create">stream.create</a>

Method for creating a stream

```js
const { stream } = botClient
const query = {
  name: 'new stream name',
  isEmpty: true
}
const response = await stream.create(teamId, query)
console.log(response)
```

Where a query may take the following parameters:
- **name**- Name of stream
- **isEmpty** - By default, streams are created with three status. When this parameter is indicated, the stream will be left empty.
- **settings** - View parameter details [here](./sorta-docs/stream-create-settings.md)

> Example response
```js
{code: 200, message: "Ok", data: "id new stream"}
```

#### <a name="user-content-stream-delete-user">stream.deleteUser</a>

Method for deleting a stream participant

```js
const { stream } = botClient
const query = { id: 'stream id', user: 'user id' }
const response = await stream.deleteUser(teamId, query)
console.log(response)
```
Where a query may take the parameters:
- **id** - Status ID
- **user** - User ID being deleted from the list of stream participants

> Example response
```js
{ code: 200, message: "OK" }
```

#### <a name="user-content-stream-delete">stream.delete</a>

Method for deleting a stream

```js
const { stream } = botClient
const response = await stream.delete(teamId, { id: 'stream id' })
console.log(response)
```

> Example response
```js
{ code: 200, message: "OK" }
```

#### <a name="user-content-stream-on-user-deleted">stream.onUserDeleted</a>

Method for finding a deleted stream participant

```js
const { stream } = botClient
const cb = message => {
  console.log(message)
}
await stream.onUserDeleted({self: true}, cb)
```

The parameter {self: true} only finds notifications of deleted bots. If ‘false’ is indicated, it will locate notifications of deletion for any user.

> View an example notification [here](./sorta-docs/onUserDeleted-message.md)

#### <a name="user-content-stream-on-user-set">stream.onUserSet</a>

Method for finding an added stream participant

```js
const { stream } = botClient
const cb = message => {
  console.log(message)
}
await stream.onUserSet({self: true}, cb)
```

The parameter {self: true} only locates notifications of bots added to the stream. If a value of ‘false’ is indicated, it will locate notifications of the addition of any user.

> View an example notification [here](./sorta-docs/onUserSet-message.md)

#### <a name="user-content-stream-read">stream.read</a>

Method for obtaining a stream

```js
const { stream } = botClient
const query = { id: 'stream id' }
const response = await stream.read(teamId, { query })
console.log(response)
```

Where a query may take the following parameters:
- **id** - Stream ID
- **ids** - An array of several stream IDs

> View an example response [here](./sorta-docs/stream-read-response.md)

#### <a name="user-content-stream-set-admin">stream.setAdmin</a>

Method for granting a user administrative privileges in a stream

```js
const { stream } = botClient
const query = { id: 'stream id', userId: 'user id' }
const response = await stream.setAdmin(teamId, { query })
console.log(response)
```

> Example response
```js
{code: 200, message: "OK"}
```

#### <a name="user-content-stream-set-name">stream.setName</a>

Method for changing the name of a stream

```js
const { stream } = botClient
const query = { id: 'stream id', name: 'new stream name' }
const response = await stream.setName(teamId, query)
console.log(response)
```
Where a query may take the parameters:
- **id** - Status ID
- **name** - New name of stream

> Example response
```js
{ code: 200, message: "OK" }
```

#### <a name="user-content-stream-set-user">stream.setUser</a>

Method for adding a participant to a stream

```js
const { stream } = botClient
const query = { id: 'stream id', user: 'user id' }
const response = await stream.setUser(teamId, query)
console.log(response)
```
Where a query may take the parameters:
- **id** - Status ID
- **user** - ID of user being added to the stream

> Example response
```js
{ code: 200, message: "OK" }
```


#### <a name="user-content-stream-set-description">stream.setDescription</a>

Method for adding a stream description

```js
const { stream } = botClient
const query = {
  id: 'stream id',
  content: 'some text'
}
const response = await stream.setDescription(teamId, { query })
console.log(response)
```

> Example response
```js
{code: 200, message: "OK"}
```

----------


### Team

#### <a name="user-content-team-invite-user">team.inviteUser</a>

Method for inviting a new user to a team WorkonFlow via email

```js
const { team } = botClient
const query = { email: 'user email', name: 'user name' }
const response = await team.inviteUser(teamId, query)
console.log(response)
```
> Example response
```js
{
  code: 200,
  message: 'OK',
  data: {
    accountId: "account id"
    contactId: "user id"

  }
}
```

#### <a name="user-content-team-on-admin-status-given">team.onAdminStatusGiven</a>

Method for finding users who have received team administrative privileges

```js
const { team } = botClient
const cb = message => {
  console.log(message)
}
team.onAdminStatusGiven(cb)
```

> Example notification
```js
  data: { userId: 'user id' }
```

#### <a name="user-content-team-on-admin-status-revoked">team.onAdminStatusRevoked</a>

Method for finding users whose administrative privileges have been revoked

```js
const { team } = botClient
const cb = message => {
  console.log(message)
}
team.onAdminStatusRevoked(cb)
```
> Example notification
```js
  data: { userId: 'user id' }
```

#### <a name="user-content-team-on-user-invited">team.onUserInvited</a>

Method for finding a user who has been added to a team

```js
const { team } = botClient
const cb = message => {
  console.log(message)
}
team.onUserInvited({ self: true }, cb)
```

The parameter {self: true} only captures notifications of bots added to the team. Where a value of ‘false’ is indicated, it will capture notifications of the addition of any user.

> Example notification
```js
{ teamId: 'team id',
  data: {
    userId: 'user id',
    email: 'user email'
  }
}
```

#### <a name="user-content-team-on-user-removed">team.onUserRemoved</a>

Method for finding a user who has been deleted from a team

```js
const { team } = botClient
const cb = message => {
  console.log(message)
}
team.onUserRemoved({ self: true }, cb)
```

The parameter {self: true} only captures notifications of bots who have been deleted from the team. Where a value of ‘false’ is indicated, it will find notifications of deletion for any user.

> Example notification
```js
{ teamId: 'team id',
  data: { userId: 'user id' }
}
```
#### <a name="user-content-team-read">team.read</a>

Method for obtaining a team

> Information will only be available regarding teams in which the bot has been invited.

```js
const { team } = botClient
const response = await team.read(teamId)
console.log(response)
```

> Example response

----------


### Thread

#### <a name="user-content-thread-create">thread.create</a>

Method for creating threads

```js
const { thread } = botClient
const query = { title: 'some title', streamId, statusId }
const response = await thread.create(teamId, { query })
console.log(response)
```
Where a query may take the following parameters:
- **streamId** - Stream ID where thread is being created
- **statusId** - Status ID in the stream where thread is being created
- **title** - Name of thread
- **deadline** - Optional field indicating a deadline for the thread
- **responsibleUserId** - Optional field indicating a user responsible for the thread
- **customerId** - Optional field indicating a client/external user in the thread
- **roles** - Optional field containing indicating followers of the thread

> Example response
```js
{ code: 200, message: 'OK', data: 'id new thread' }
```

#### <a name="user-content-thread-on-budget-updated">thread.onBudgetUpdated</a>

Method for finding changes to a thread’s budget

```js
const { thread } = botClient
const cb = message => {
  console.log(message)
}
await thread.onBudgetUpdated(cb)
```

> View an example notification [here](./sorta-docs/thread-onBudgetUpdated-message.md)

#### <a name="user-content-thread-on-created">thread.onCreated</a>

Method for finding a created thread

```js
const { thread } = botClient
const cb = message => {
  console.log(message)
}
await thread.onCreated(cb)
```

> View an example notification [here](./sorta-docs/thread-onCreated-message.md)

#### <a name="user-content-thread-on-deadline-updated">thread.onDeadlineUpdated</a>

Method for finding changes to a thread’s deadline

```js
const { thread } = botClient
const cb = message => {
  console.log(message)
}
await thread.onDeadlineUpdated(cb)
```

> View an example notification [here](./sorta-docs/thread-onDeadlineUpdated-message.md)

#### <a name="user-content-thread-status-updated">thread.onStatusUpdated</a>

Method for finding changes to a thread’s status

```js
const { thread } = botClient
const cb = message => {
  console.log(message)
}
await thread.onStatusUpdated(cb)
```

> View an example notification [here](./sorta-docs/thread-onStatusUpdated-message.md)

#### <a name="user-content-thread-read-description">thread.readDescription</a>

Method for obtaining a thread description

```js
const { thread } = botClient
const query = { id: 'thread id' }
const response = await thread.readDescription(teamId, { query })
console.log(response)
```

> View an example response [here](./sorta-docs/thread-readDescription-response.md)

#### <a name="user-content-thread-read">thread.read</a>

Method for locating a thread

```js
const { thread } = botClient
const query = { id: threadId }
const response = await thread.read(teamId, { query })
console.log(response)
```

Where a query may take the following parameters:
- **id** - Thread ID
- **statusId** - Status ID (returns all threads with the indicated status)
- **statusIds** - An array of status IDs
- **streamId** - Stream ID (returns all threads in a stream)
- **ltUpdatedAt** - (Less than) Time limit for creation > less than
- **gtUpdatedAt** - (Greater than) Time limit for creation < greater than

> View an example response [here](./sorta-docs/thread-read-response.md)

#### <a name="user-content-thread-set-budget">thread.setBudget</a>

Method for changing a thread’s budget

```js
const { thread } = botClient
const query = { id: threadId, budget: 10000 }
const response = await thread.setBudget(teamId, { query })
console.log(response)
```

Where a query may take the following parameters:
- **id** - Thread ID
- **budget** - Quantity of the thread’s budget

> View an example response [here](./sorta-docs/thread-setBudget-response.md)

#### <a name="user-content-thread-set-deadline">thread.setDeadline</a>

Method for changing a thread’s deadline

```js
const { thread } = botClient
const query = { id: threadId, timestamp: [null, 1524902400000] }
const response = await thread.setDeadline(teamId, { query })
console.log(response)
```

Where a query may take the following parameters:
- **id** - Thread ID
- **timestamp** - An array of data in the format of a time stamp. The first element is the start of the thread and the second is its end (if the first element is given a value of null, the thread will only display a deadline).

> View an example response [here](./sorta-docs/thread-setDeadline-response.md)


#### <a name="user-content-thread-set-description">thread.setDescription</a>

Method for changing the thread’s description

```js
const { thread } = botClient
const query = {
  content: 'some text',
  id: "thread id"
}
const response = await thread.setDescription(teamId, { query })
console.log(response)
```

> Example response
```js
{code: 200, message: "OK", data: "description id"}
```
#### <a name="user-content-thread-set-priority">thread.setPriority</a>

Method for changing the priority of a thread

```js
const { thread } = botClient
const query = { id: threadId, priority: "HIGH" }
const response = await thread.setPriority(teamId, { query })
console.log(response)
```

Where a query may take the following parameters:
- **id** - Thread ID
- **priority** - Priority level (one of two options: ‘HIGH’ or ‘NORMAL.’ Must be in upper case letters.)

> View an example response [here](./sorta-docs/thread-setPriority-response.md)

#### <a name="user-content-thread-set-responsible">thread.setResponsible</a>

Method for designating a responsible party for a thread. It is necessary to send both the thread ID and the user ID

```js
const { thread } = botClient
const query = { id: threadId, userId }
const response = await thread.setResponsible(teamId, { query })
console.log(response)
```

> View an example response [here](./sorta-docs/thread-setResponsible-response.md)

#### <a name="user-content-thread-set-status">thread.setStatus</a>

Method for changing a thread’s status

```js
const { thread } = botClient
const query = { id: threadId, statusId: "status id" }
const response = await thread.setStatus(teamId, { query })
console.log(response)
```

Where a query may take the following parameters:
- **id** - Thread ID
- **statusId** - Status ID

> View an example response [here](./sorta-docs/thread-setResponsible-response.md)

#### <a name="user-content-thread-set-stream">thread.setStream</a>

Method for sending tasks to another stream

```js
const { thread } = botClient
const query = { id: threadId, streamId: "stream id" }
const response = await thread.setStream(teamId, { query })
console.log(response)
```

Where a query may take the following parameters:
- **id** - Thread ID
- **streamId** - Stream ID

> View an example response [here](./sorta-docs/thread-setResponsible-response.md)

#### <a name="user-content-thread-set-title">thread.setTitle</a>

Method for changing the name of a thread

```js
const { thread } = botClient
const query = { id: threadId, title: "new name stream" }
const response = await thread.setTitle(teamId, { query })
console.log(response)
```

Where a query may take the following parameters:
- **id** - Thread ID
- **title** - New name of the thread

> View an example response [here](./sorta-docs/thread-setResponsible-response.md)



#### <a name="user-content-thread-add-customers">thread.addCustomers</a>

Method for adding clients to a thread

```js
const { thread } = botClient
const query = { id: threadId, customerIds: [list customers ids] }
const response = await thread.addCustomers(teamId, { query })
console.log(response)
```

Where a query may take the following parameters:
- **id** - Thread ID
- **customerId** - ID of customer
- **customerIds** - Array of client IDs

> Example response

```js
{ code: 200, message: 'ok' }
```


#### <a name="user-content-thread-remove-customers">thread.removeCustomers</a>

Method for removing clients from a thread

```js
const { thread } = botClient
const query = { id: threadId, customerIds: [list customers ids] }
const response = await thread.removeCustomers(teamId, { query })
console.log(response)
```

Where a query may take the following parameters:
- **id** - Thread ID
- **customerId** - ID of customer
- **customerIds** - Array of customer IDs

> Example response

```js
{ code: 200, message: 'ok' }
```

---------


### File

#### file.getGETUrl

Method for receiving file URLs with with [Amazon](https://www.amazon.com/)

```js
const { file } = botClient
const query = { id: 'file id' }
const response = await file.getGETUrl(teamId, query)
console.log(response)
```
Where a query may take the following parameters:
- **id** - File ID
- **ids** - Array of file IDs

> View an example response [here](./sorta-docs/getGETUrl-response.md)

#### file.getPUTUrl

Method for receiving file download URLs on [Amazon](https://www.amazon.com/)

```js
const { file } = botClient
const query = {
  authorId: "user id",
  filename: "fileName.format",
  size: "number size",
  streamId: "stream id",
  threadId: "thread id"
}
const response = await file.getPUTUrl(teamId, query)
console.log(response)
```

> View an example response [here](./sorta-docs/getGETUrl-response.md)

---------


### Mail

#### <a name="user-content-mail-get-accounts">mail.getAccounts</a>

Method for obtaining email channels

```js
const { mail } = botClient
const query = { id: 'user id' }
const response = await mail.getAccounts(teamId, query)
console.log(response)
```
Where a query may take the following parameters:
- **id** - User ID (returns array of available channels)
- **ids** - Array of user IDs (analogous to **id**)
- **email** - Mail channel (returns channel with indicated email address)

> View an example response [here](./sorta-docs/mail-getAccounts-response.md)

#### <a name="user-content-mail-on-received">mail.onReceived</a>

Method for locating a message received via an email channel

```js
const { mail } = botClient
const cb = message => {
  console.log(message)
}
mail.onReceived(cb)
```

> Example notification

```js
{
  code: 200,
  message: 'OK',
  content:{ id: "mail id", conversationId: "conversation id" }
}
```

#### <a name="user-content-mail-on-sent">mail.onSent</a>

Method for locating a sent message from a WorkonFlow email channel

```js
const { mail } = botClient
const cb = message => {
  console.log(message)
}
mail.onSent(cb)
```

> Example notification

```js
{
  code: 200,
  message: 'OK',
  content:{ id: "mail id", conversationId: "conversation id" }
}
```

#### <a name="user-content-mail-read">mail.read</a>

Method for receiving email channels

```js
const { mail } = botClient
const query = { id: 'mail id' }
const response = await mail.read(teamId, query)
console.log(response)
```
Where a query may take the following parameters:
- **id** - Email ID;
- **ids** - Array of email IDs

> View an example response [here](./sorta-docs/mail-read-response.md)

#### <a name="user-content-mail-send">mail.send</a>

Method for sending email

```js
const { mail } = botClient
const query = {
  from: "channel email",
  html: "<div><p>some text</p></div>",
  messageId: "",
  subject: "some subject",
  text: "alt text",
  threadId: "thread id",
  to: "contact email"
}
const response = await mail.send(teamId, query)
console.log(response)
```
Where a query may take the parameters:
- **from** - Must indicate an email channel
- **html** - HTML layout for the letter. It not indicated in the letter, the **text** parameter will be displayed.
- **messageId** - ID of message in the form of an email client (leave blank if unknown)
- **subject** - Subject of message
- **text** - Text of message (displayed in the absence of an **HTML** layout)
- **threadId** - Thread ID
- **to** - Email of recipient

> Example response
```js
{code: 200, message: "OK"}
```

---------


### telephony

#### <a name="user-content-telephony-create-user">telephony.createUser</a>

User SIP method (still in development)

```js
const { telephony } = botClient
const query = {
  username: 'user name',
  password: 'user pass',
  domain: 'domain',
  contactId: 'user id'
}
const response = await telephony.createUser(teamId, query)
console.log(response)
```

> Example response
```js
{code: 200, message: "OK"}
```

#### <a name="user-content-telephony-delete-user">telephony.deleteUser</a>

Method for deleting user SIP from telephony (still in development)

```js
const { telephony } = botClient
const query = { id: 'sip id' }
const response = await telephony.deleteUser(teamId, query)
console.log(response)
```

> Example response
```js
{code: 200, message: "OK"}
```

#### <a name="user-content-telephony-get-user">telephony.getUser</a>

Method for obtaining user SIP (still in development)

```js
const { telephony } = botClient
const query = { id: 'sip id', username: 'sip user name', contactId: 'user id' }
const response = await telephony.getUser(teamId, query)
console.log(response)
```

#### <a name="user-content-telephony-update-user">telephony.updateUser</a>

User SIP method (still in development)

```js
const { telephony } = botClient
const query = {
  username: 'user name',
  password: 'user pass',
  domain: 'domain',
  contactId: 'user id'
}
const response = await telephony.updateUser(teamId, query)
console.log(response)
```

> Example response
```js
{code: 200, message: "OK"}
```
-----------
