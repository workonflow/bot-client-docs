### Пример ответа

```js
 { code: 200,
  message: 'OK',
  data: [{
    content: "{}", // JSON format example below
    created: 'create date in timestamp', // example 1515487277798
    editing: false,
    format: "draft.js",
    selection: null,
    teamId: "team id",
    updated: 'update date in timestamp', // example 1515487277798
    _id: "description id"
  }]
}
```
#### example JSON description by content field
```json
"{"type":"doc","content":[{"type":"paragraph","content":[{"type":"text","marks":[],"text":"text"}]},{"type":"paragraph","content":[{"type":"text","marks":[],"text":"text"}]},{"type":"paragraph","content":[{"type":"text","marks":[],"text":"text"}]},{"type":"paragraph","content":[{"type":"text","marks":[{"type":"strike"}],"text":"text"}]},{"type":"paragraph"},{"type":"paragraph","content":[{"type":"text","marks":[{"type":"underline"}],"text":"text"}]},{"type":"paragraph","content":[{"type":"text","marks":[{"type":"em"}],"text":"text"}]},{"type":"paragraph","content":[{"type":"text","marks":[{"type":"strong"}],"text":"text"}]},{"type":"ordered_check_list","content":[{"type":"check_list_item","attrs":{"isCheck":false},"content":[{"type":"paragraph","content":[{"type":"text","marks":[],"text":"text"}]}]}]},{"type":"ordered_list","content":[{"type":"list_item","attrs":{"id":null},"content":[{"type":"paragraph","content":[{"type":"text","marks":[],"text":"text"}]}]}]},{"type":"ordered_number_list","attrs":{"order":1},"content":[{"type":"list_item","attrs":{"id":null},"content":[{"type":"paragraph"},{"type":"horizontal_rule"},{"type":"paragraph"}]}]},{"type":"paragraph","content":[{"type":"text","marks":[],"text":"text text"}]}]}"
```

#### in JSON parse

```js
{
  "type": "doc",
  "content": [{
    "type": "paragraph",
    "content": [{
      "type": "text",
      "marks": [],
      "text": "text"
    }]
  }, {
    "type": "paragraph",
    "content": [{
      "type": "text",
      "marks": [],
      "text": "text"
    }]
  }, {
    "type": "paragraph",
    "content": [{
      "type": "text",
      "marks": [],
      "text": "text"
    }]
  }, {
    "type": "paragraph",
    "content": [{
      "type": "text",
      "marks": [{
        "type": "strike"
      }],
      "text": "text"
    }]
  }, {
    "type": "paragraph"
  }, {
    "type": "paragraph",
    "content": [{
      "type": "text",
      "marks": [{
        "type": "underline"
      }],
      "text": "text"
    }]
  }, {
    "type": "paragraph",
    "content": [{
      "type": "text",
      "marks": [{
        "type": "em"
      }],
      "text": "text"
    }]
  }, {
    "type": "paragraph",
    "content": [{
      "type": "text",
      "marks": [{
        "type": "strong"
      }],
      "text": "text"
    }]
  }, {
    "type": "ordered_check_list",
    "content": [{
      "type": "check_list_item",
      "attrs": {
        "isCheck": false
      },
      "content": [{
        "type": "paragraph",
        "content": [{
          "type": "text",
          "marks": [],
          "text": "text"
        }]
      }]
    }]
  }, {
    "type": "ordered_list",
    "content": [{
      "type": "list_item",
      "attrs": {
        "id": null
      },
      "content": [{
        "type": "paragraph",
        "content": [{
          "type": "text",
          "marks": [],
          "text": "text"
        }]
      }]
    }]
  }, {
    "type": "ordered_number_list",
    "attrs": {
      "order": 1
    },
    "content": [{
      "type": "list_item",
      "attrs": {
        "id": null
      },
      "content": [{
        "type": "paragraph"
      }, {
        "type": "horizontal_rule"
      }, {
        "type": "paragraph"
      }]
    }]
  }, {
    "type": "paragraph",
    "content": [{
      "type": "text",
      "marks": [],
      "text": "text text"
    }]
  }]
}
```

