[//title]: (jq-command-to-parse-json-field)
[//englishtitle]: (jq-command-to-parse-json-field)
[//category]: (bash,linux,snippet)
[//tags]: (bash,jq,linux,snippet)
[//createtime]: (20220303)
[//updatetime]: (20220303)

```bash
$ echo '{"name":"Alice", "age":10}' | jq '.name'
"Alice"
```

if you don't want the quote, just the string itself, use `-r` option

```bash
$ echo '{"name":"Alice", "age":10}' | jq -r '.name'
Alice
```

## notes

`-r`: output raw strings, not JSON texts
