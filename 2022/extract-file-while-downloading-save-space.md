[//title]: (extract-file-while-downloading-to-save-space)
[//englishtitle]: (extract-file-while-downloading-to-save-space)
[//category]: (wget,linux,snippet)
[//tags]: (wget,linux,snippet)
[//createtime]: (20220227)
[//updatetime]: (20220227)

Extract big compressed file while downloading to save time and disk space. The compressed file won't store.

```bash
wget -q -O - <URL> | tar -I lz4 -xvf -
```
