[//title]: (install-docker-compose)
[//englishtitle]: (install-docker-compose)
[//category]: (docker,linux,snippet)
[//tags]: (docker,linux,snippet)
[//createtime]: (20220429)
[//updatetime]: (20220429)

```bash
wget https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)
sudo mv docker-compose-$(uname -s)-$(uname -m) /usr/local/bin/docker-compose
sudo chmod -v +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

## Note

The last line is essential, otherwise `docker-compose` command can't be found when you use non-root user to install `docker-compose` and use sudo to run it.

```bash
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```
