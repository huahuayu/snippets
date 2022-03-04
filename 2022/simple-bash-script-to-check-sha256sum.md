[//title]: (simple-bash-script-to-check-sha256sum)
[//englishtitle]: (simple-bash-script-to-check-sha256sum)
[//category]: (linux,bash,snippet)
[//tags]: (linux,bash,checksum,snippet)
[//createtime]: (20220303)
[//updatetime]: (20220303)

```bash
if [[ $(sha256sum /file/to/check | awk '{print $1}') = "58f17545056267f57a2d95f4c9c00ac1d689a580e220c5d4de96570fbbc832e1" ]]; then echo "OK"; else echo "MISMATCHED"; fi;
```
