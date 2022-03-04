[//title]: (extract-file-while-downloading-to-save-space)
[//englishtitle]: (extract-file-while-downloading-to-save-space)
[//category]: (wget,linux,snippet)
[//tags]: (wget,linux,snippet)
[//createtime]: (20220304)
[//updatetime]: (20220304)

Q: Let's say you have 200G disk space, you need download a 110G tar file and extract it in same disk, so it takes 220G at least, the extract will fail. so what you can do?

A: You can extract the tar file while downloading, and only keep the extracted file, with this command

```bash
wget -q -O- <URL> | tar zxvf -
```

## Notes

`-q`: Turn off Wget's output, so there's no wget-output file.

`-O` flag is the short notation for the flag --output-document in wget command-line utility.

The hypen `-` after the flag denotes STDOUT.

So `-O-` means get as a file and print the result on STDOUT.

## Learn By Example

- wget -O liushiming.cn writes the output to index.html file
- wget -O custom.txt liushiming.cn writes the output to your custom.txt file as mentioned
- wget -O - liushiming.cn writes output to your terminal's STDOUT

## Reference

https://stackoverflow.com/questions/9830242/what-does-wget-o-mean
