## Пример ответа

#### ответ загрузки на амазон (getPUTUrl)

```js
 { code: 200,
  message: 'OK',
  data: {
    id: "file id"
    url: "url address for download file"
  }
}
```

#### ответ получения с амазона (getGETUrl)

```js
 { code: 200,
  message: 'OK',
  data: {
    filename: "fileName.format",
    id: "file id",
    url: "url address for upload file"
    urlPreview: null
  }
}
```
