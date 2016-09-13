# alpine-textlint / Dockerfile

この Dockerfile は、[textlint](https://github.com/textlint/textlint) の導入を簡単にする Docker イメージを作成するためのファイルです。作成する Docker イメージのベースイメージには、Alpine Linux を使用しています。

この textlint Docker イメージで使用できるルールは以下のとおりです。

* [textlint\-rule\-no\-todo](https://github.com/azu/textlint-rule-no-todo)
* [textlint\-rule\-preset\-ja\-technical\-writing](https://github.com/textlint-ja/textlint-rule-preset-ja-technical-writing)
* [textlint\-rule\-ja\-yahoo\-kousei](https://www.npmjs.com/package/textlint-rule-ja-yahoo-kousei)
* [textlint\-rule\-spellchecker](https://github.com/nodaguti/textlint-rule-spellchecker)
* [textlint\-rule\-spacing](https://github.com/textlint-ja/textlint-rule-spacing)

デフォルトの textlint 設定ファイル（`.textlintrc`）では、`no-todo` ルールと `preset-ja-technical-writing` プリセットを有効にしています。

```
{
  "rules": {
    "no-todo": true,
    "preset-ja-technical-writing": true
  }
}
```

## Requirements

* [Docker](https://www.docker.com) 1.12.1+

## Usage

自身で Docker イメージを作成して使用する場合は、`docker build` コマンドを使います。

```
docker build -t asakaguchi/textlint .
```

もし Docker イメージを作らずに、既製の Docker イメージを使用する場合は、`docker pull` コマンドを使います。

```
docker pull asakaguchi/textlint
```

この textlint Docker イメージを使用して文章をチェックするには、`docker run --rm` コマンドを使います。

以下は、カレントディレクトリの `foo.txt` というファイルに保存された文章をチェックする例です。`foo.txt` ファイルのパスが `/data/foo.txt` となっていることに注意してください。

```
docker run --rm -v $(pwd):/data asakaguchi/textlint /data/foo.txt
```

`-v $(pwd):/data` により Docker イメージ化した textlint から `/data` のパスで、カレントディレクトリのファイルを参照できるようにしています。

HTML ファイル中の文章をチェックしたい場合は、`--plugin html` を指定します。

```
docker run --rm -v $(pwd):/data asakaguchi/textlint --plugin html /data/bar.html
```

スペルチェックのルールを追加して、文章をチェックしたい場合は、`--rule spellchecker` を指定します。

```
docker run --rm -v $(pwd):/data asakaguchi/textlint --rule spellchecker /data/baz.txt
```

デフォルトの設定ファイルをカスタマイズして文章をチェックしたい場合は、以下のように `.textlintrc` ファイルをダウンロードします。

```
docker run --rm --entrypoint sh asakaguchi/textlint -c "cat /textlint/.textlintrc" > .textlintrc
```

ダウンロードしたファイルを編集します。以下は `ja-yahoo-kousei` ルールを追加した例です（"*****" はアプリケーション ID）。

```
{
  "rules": {
    "no-todo": true,
    "preset-ja-technical-writing": true,
    "ja-yahoo-kousei": {
      "appID": "********************************************************"
    }
  }
}
```

`-w /data` を指定して、文章をチェックします。

```
docker run --rm -v $(pwd):/data -w /data asakaguchi/textlint foo.txt
```

## License
This is licensed under the [MIT](https://github.com/asakaguchi/dockerfiles/blob/master/LICENSE) license.