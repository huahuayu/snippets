[//title]: (recursively-delete-files-when-filename-matchs-regex)
[//englishtitle]: (recursively-delete-files-when-filename-matchs-regex)
[//category]: (snippet,bash,regex,find)
[//tags]: (snippet,bash,regex,find)
[//createtime]: (20230324)
[//updatetime]: (20230324)

Recursively delete files when filename matches regex.

```bash
find /your/dir -type f | grep -E ".*\.(jpg|png|gif)$" | sed 's/ /\\ /g' | xargs rm
```

`find /your/dir -type f` will find all files in the directory and subdirectories.

`grep -E ".*\.(jpg|png|gif)$"` will filter the files with the extension jpg, png or gif.

`sed 's/ /\\ /g'` will escape the spaces in the dir/file names. This is necessary because `xargs` will split the arguments by spaces.

`xargs rm` will remove the files.