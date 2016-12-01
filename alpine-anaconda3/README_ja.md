# alpine-anaconda3 / Dockerfile

この Dockerfile は、Alpine Linux 上に Anaconda3 で Python 環境を構築するためのファイルです。

## Requirements

* [Docker](https://www.docker.com) 1.12.1+

## Usage

Docker イメージを作るには、次のようにコマンドを実行します。

```text
docker build -t my-anaconda3 .
```

Docker イメージを実行するには、次のようにコマンドを実行します。

```text
docker run -it my-anaconda3
```

## Tips

macOS で、Matplotlib を使ったグラフ描画を行いたい場合は、XQuartz と socat を使います。

XQuartz と socat のインストールは、次のようにコマンドを実行します。

```text
brew install Caskroom/cask/xquartz
brew install socat
```

Docker イメージを実行する前に、次のようにコマンドを実行します。

```text
open -a Xquartz
socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"
```

Docker イメージを実行するには、環境変数 DISPLAY を指定して、次のようにコマンドを実行します。

```text
docker run --rm -it -e DISPLAY=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}'):0 my-anaconda3
```

## License

This is licensed under the [MIT](https://github.com/asakaguchi/dockerfiles/blob/master/LICENSE) license.