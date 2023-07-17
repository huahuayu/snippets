[//title]: (prevent-git-container-exit-after-start)
[//englishtitle]: (prevent-git-container-exit-after-start)
[//category]: (git,docker,snippet)
[//tags]: (git,docker,snippet)
[//createtime]: (20230717)
[//updatetime]: (20230717)

```bash
docker run -dit -v $(pwd):/git --entrypoint /bin/sh alpine/git
```

Note:

Without `--entrypoint /bin/sh`, the container will exit immediately.