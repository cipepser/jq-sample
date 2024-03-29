# jq芸の練習

[JSON Example](https://json.org/example.html)から使えそうなサンプルを借りてくる。

`[]`で配列になっているjson

```json
❯ cat menu.json | jq '.menu.items[].id'
"Open"
"OpenNew"
null
"ZoomIn"
"ZoomOut"
"OriginalView"
null
"Quality"
"Pause"
"Mute"
null
"Find"
"FindAgain"
"Copy"
"CopyAgain"
"CopySVG"
"ViewSVG"
"ViewSource"
"SaveAs"
null
"Help"
"About"
```

長さやtypeを知りたいとき

```json
❯ cat menu.json | jq '.menu.items | length'
22

❯ cat menu.json | jq '.menu.items | type'
"array"

❯ cat menu.json | jq '.menu.items[] | type'
"object"
"object"
"null"
"object"
"object"
"object"
"null"
"object"
"object"
"object"
"null"
"object"
"object"
"object"
"object"
"object"
"object"
"object"
"object"
"null"
"object"
"object"
```

keyを知りたいとき

```json
❯ cat menu.json | jq '.menu.items[] | keys'
[
  "id"
]
[
  "id",
  "label"
]
jq: error (at <stdin>:76): null (null) has no keys
```

valueの置換。便利そうだけど具体的にいつ使うんだろう。  
自分でサンプル用のjson作るときとか？

```json
❯ cat menu.json | jq '.menu.items[] | .id = .id + "-hoge"'
{
  "id": "Open-hoge"
}
{
  "id": "OpenNew-hoge",
  "label": "Open New"
}
{
  "id": "-hoge"
}
{
  "id": "ZoomIn-hoge",
  "label": "Zoom In"
}
{
  "id": "ZoomOut-hoge",
  "label": "Zoom Out"
}
{
  "id": "OriginalView-hoge",
  "label": "Original View"
}
{
  "id": "-hoge"
}
{
  "id": "Quality-hoge"
}
{
  "id": "Pause-hoge"
}
{
  "id": "Mute-hoge"
}
{
  "id": "-hoge"
}
{
  "id": "Find-hoge",
  "label": "Find..."
}
{
  "id": "FindAgain-hoge",
  "label": "Find Again"
}
{
  "id": "Copy-hoge"
}
{
  "id": "CopyAgain-hoge",
  "label": "Copy Again"
}
{
  "id": "CopySVG-hoge",
  "label": "Copy SVG"
}
{
  "id": "ViewSVG-hoge",
  "label": "View SVG"
}
{
  "id": "ViewSource-hoge",
  "label": "View Source"
}
{
  "id": "SaveAs-hoge",
  "label": "Save As"
}
{
  "id": "-hoge"
}
{
  "id": "Help-hoge"
}
{
  "id": "About-hoge",
  "label": "About Adobe CVG Viewer..."
}
```

簡単なmap。`.`で指定したことなかったけど、便利そう。

```json
❯ echo '[1,2,3,4,5]' | jq 'map(. * 2)'
[
  2,
  4,
  6,
  8,
  10
]
```

map_values。

```json
❯ echo '{"a":1, "b":2, "c":3, "d":4, "e":5}' | jq 'map_values(. * 2)'
{
  "a": 2,
  "b": 4,
  "c": 6,
  "d": 8,
  "e": 10
}
```

to_entries

```json
❯ echo '{"a":1, "b":2, "c":3, "d":4, "e":5}' | jq
{
  "a": 1,
  "b": 2,
  "c": 3,
  "d": 4,
  "e": 5
}

❯ echo '{"a":1, "b":2, "c":3, "d":4, "e":5}' | jq 'to_entries'
[
  {
    "key": "a",
    "value": 1
  },
  {
    "key": "b",
    "value": 2
  },
  {
    "key": "c",
    "value": 3
  },
  {
    "key": "d",
    "value": 4
  },
  {
    "key": "e",
    "value": 5
  }
]
```

`from_entries`で上記の戻しができる。


結果をコンパクトに表示。

```json
❯ cat menu.json | jq -c '.menu.items[] | {id}'
{"id":"Open"}
{"id":"OpenNew"}
{"id":null}
{"id":"ZoomIn"}
{"id":"ZoomOut"}
{"id":"OriginalView"}
{"id":null}
{"id":"Quality"}
{"id":"Pause"}
{"id":"Mute"}
{"id":null}
{"id":"Find"}
{"id":"FindAgain"}
{"id":"Copy"}
{"id":"CopyAgain"}
{"id":"CopySVG"}
{"id":"ViewSVG"}
{"id":"ViewSource"}
{"id":"SaveAs"}
{"id":null}
{"id":"Help"}
{"id":"About"}
```

arrayに戻す

```json
❯ cat menu.json | jq -c '.menu.items[] | {id}' | jq -s
[
  {
    "id": "Open"
  },
  {
    "id": "OpenNew"
  },
  {
    "id": null
  },
  {
    "id": "ZoomIn"
  },
  {
    "id": "ZoomOut"
  },
  {
    "id": "OriginalView"
  },
  {
    "id": null
  },
  {
    "id": "Quality"
  },
  {
    "id": "Pause"
  },
  {
    "id": "Mute"
  },
  {
    "id": null
  },
  {
    "id": "Find"
  },
  {
    "id": "FindAgain"
  },
  {
    "id": "Copy"
  },
  {
    "id": "CopyAgain"
  },
  {
    "id": "CopySVG"
  },
  {
    "id": "ViewSVG"
  },
  {
    "id": "ViewSource"
  },
  {
    "id": "SaveAs"
  },
  {
    "id": null
  },
  {
    "id": "Help"
  },
  {
    "id": "About"
  }
]
```


## References
- [シェル芸で使いたい jqイディオム \- Qiita](https://qiita.com/nmrmsys/items/5b4a4bd2e3909db161b1)
- [JSON Example](https://json.org/example.html)
- [jqで連続するオブジェクトを配列にする \- Qiita](https://qiita.com/eielh/items/aff045e1689be8e89972)