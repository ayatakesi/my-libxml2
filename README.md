# libxml2
GNU Emacs30.0.50に含まれる`java/INSTALL`にしたがってパッチを適用したlibxml2モジュール)のレポジトリ。

# 作成した手順
1. [Google Gitのlibxml2](https://android.googlesource.com/platform/external/libxml2/)をclone


```bash
$: git clone https://android.googlesource.com/platform/external/libxml2/
```

2. `nougat-release`ブランチから修正用ブランチ`my/nougat-release`をcheckout

```bash
$: cd libxml2
$: git checkout nougat-release
$: git checkout -b my/nougat-release
```

3. `java/INSTALL`にしたがいHTMLサポートを削除するコミット[edb5870767fed8712a9b77ef34097209b61ab2db](https://android.googlesource.com/platform/external/libxml2/+/edb5870767fed8712a9b77ef34097209b61ab2db)をrevert[1^]

```bash
$: git revert edb5870767fed8712a9b77ef34097209b61ab2db
```

4. `java/INSTALL`にしたがいpatchを適用

```bash
$: patch -p1 < PATCH_FOR_LIBXML2.patch
```

4. 上記patch ファイルとpatch適用後ファイルをcommitして空レポジトリにpush

```bash
$: git add -A
$: git commit -m 'nanika commit messages...'
$: gh repo create my-libxml2 --public
$: git remote add mine https://github.com/JIBUN/my-libxml2.git
$: git branch -M my/nougat-release
$: git push -u mine my/nougat-release
```
[1^]: このrevertによってHTMLサポートを復活させないと、少なくともewwは動かなかったです。
