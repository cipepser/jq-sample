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


## References
- [シェル芸で使いたい jqイディオム \- Qiita](https://qiita.com/nmrmsys/items/5b4a4bd2e3909db161b1)
- [JSON Example](https://json.org/example.html)