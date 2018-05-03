#### Пример ответа 

## пользователь

```js
{ code: 200,
  message: 'OK',
  data: [ {
    _id: 'user id',
    billingType: 'users',
    basicData: {
      name: 'user name',
      email: [ 'user email' ],
      phone: [ 'user phone' ]
    },
    extension: 'number extension in system',
    canonicalPhone: [],
    teamId: 'team id',
    createdAt: '2017-10-30T10:15:53.245Z',
    updatedAt: 1517574060991,
    color: 'background name color',
    hrData: { position: '' },
    status: 'on||off (online or no)',
    voiceRules: [ {
      type: 'webrtc',
      enabled: true,
      timeout: '',
      extension: '100*9 (default number extension + *9)',
      visible: true
    }, {
      type: 'sip',
      enabled: true,
      timeout: '',
      extension: '100*1 (default number extenseion + *1)',
      visible: true
    } ]
  } ]
}
```

## контакт

```js
{ code: 200,
  message: 'OK',
  data: [ {
    _id: '5ad848cc014201001f82c947',
    basicData: { name: 'new name customer' },
    customFields:  [ {
      id: 'B1R5NTS3z',
      label: 'Company',
      value: '',
      type: 'company'
    }, {
      id: 'B1l094TB2M',
      label: 'Work phone',
      value: '',
      type: 'phone'
    }, {
      id: 'rkbA9VTH3M',
      label: 'Work e-mail',
      value: '',
      type: 'email'
    } ],
    billingType: 'contacts',
    teamId: '59f6fbd69af753001e453905',
    createdAt: '2018-04-19T07:44:12.942Z',
    updatedAt: '2018-04-19T07:44:12.942Z',
    color: '#718699',
    status: 'off',
    voiceRules: [ {
      type: 'webrtc',
      enabled: true,
      timeout: '',
      extension: '*9',
      visible: true
    }, {
      type: 'sip',
      enabled: true,
      timeout: '',
      extension: '*1',
      visible: true
    } ]
  } ]
}
```