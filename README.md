# 概要 [![Actions Status](https://github.com/OUXT-Polaris/HP/workflows/github%20pages/badge.svg)](https://github.com/OUXT-Polaris/HP/actions)

これは、OUXTのHP（ https://www.ouxt.jp ）のリポジトリです。

Hugo + GitHub Pagesで構成されています。

このサイトの基本となっているのは、HugoのAcademic Themeです。

# 扱い方
1. git clone
2. issue
3. branch
4. marge

といった手順で行ってください。以下にざっくりと説明を示します。
## git clone
ssh-keyをgithubに登録してから、 'using ssh'でgit cloneしましょう

## issue
issueページで追加したいページや内容を記入しましょう。ここに記入することで、開発履歴として残ります。

## branch
上記のbranchに合わせて、develop/（issue番号_issue名）のbranchを作成

例：[develop/#1_edit_readme](https://github.com/OUXT-Polaris/HP/tree/develop/%231_edit_readme)

## marge
pull requestsのタブより、[develop/master](https://github.com/OUXT-Polaris/HP/tree/develop/master)ブランチへマージリクエスト/マージを行う。

続いて、[master](https://github.com/OUXT-Polaris/HP/)ブランチへ先ほどと同様にマージリクエスト/マージを行う

ここで、マージが通り、githubActionでエラーが発生しなければWebページとして公開されます。

# 追加でつけた機能
Google Analyst のID埋め込みがされています。
これによって、Google Search Consolに追加されているのでGoogle検索に表示されるようになっています。

OUXT管理者用アカウントに紐づけされています。

# その他
## License

Copyright 2017-present [George Cushen](https://georgecushen.com).

Released under the [MIT](https://github.com/sourcethemes/academic-kickstart/blob/master/LICENSE.md) license.

[![Analytics](https://ga-beacon.appspot.com/UA-78646709-2/academic-kickstart/readme?pixel)](https://github.com/igrigorik/ga-beacon)
