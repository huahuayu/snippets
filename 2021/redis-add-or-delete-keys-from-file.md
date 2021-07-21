[//title]: (redis-batch-add-or-delete-key-from-file)
[//englishtitle]: (redis-batch-add-or-delete-key-from-file)
[//category]: (redis,bash,snippet)
[//tags]: (redis,bash,snippet)
[//createtime]: (20210721)
[//updatetime]: (20210721)

batch export keys to file

```bash
redis-cli -a $passwd keys "$key" > key_export.txt
```

batch add keys from file

```bash
for i in `cat /tmp/t.txt`; do redis-cli -a pass set $i 1; done
```

batch delete keys

```bash
redis-cli -a $passwd keys "$key" | xargs redis-cli -a $passwd del
```
