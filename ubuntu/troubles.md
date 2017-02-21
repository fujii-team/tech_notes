# 経験したトラブル一覧

## Error parsing PCC subspaces from PCCT と言われてUbuntuが起動しない

> The root filesystem on /dev/sda1 requires a manual fsck  

とか言われて
> (initramfs)

というプロンプトが出てくるので
> fsck -fy /dev/sda1

としてファイルシステムを修復する。
