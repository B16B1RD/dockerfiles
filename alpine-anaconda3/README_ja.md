# alpine-anaconda3 / Dockerfile

この Dockerfile は、Alpine Linux 上に Anaconda3 で Python 環境を構築するためのファイルです。

## Requirements

* [Docker](https://www.docker.com) 1.12.1+

## Usage

Docker イメージを作るには、次のコマンドを使用します。

```text
docker build -t my-anaconda3 .
```

作成した Docker イメージを実行するには、次のコマンドを使用します。

```text
docker run -it my-anaconda3
```

## License

This is licensed under the [MIT](https://github.com/asakaguchi/dockerfiles/blob/master/LICENSE) license.