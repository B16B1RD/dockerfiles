# alpine-anaconda3 / Dockerfile

This Dockerfile is a file for building a Python environment with Anaconda3 on Alpine Linux.

## Requirements

* [Docker](https://www.docker.com) 1.12.1+

## Usage

To create a Docker image, execute the command as follows.

```text
docker build -t my-anaconda3 .
```

To execute the Docker image, execute the command as follows.

```text
docker run -it my-anaconda3
```

## Tips

With macOS, if you want to draw graphs using Matplotlib, use XQuartz and socat.

To install XQuartz and socat, execute the command as follows.

```text
brew install Caskroom/cask/xquartz
brew install socat
```

Before executing the Docker image, execute the command as follows.

```text
open -a Xquartz
socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"
```

To execute the Docker image, specify the environment variable DISPLAY and execute the command as follows.

```text
docker run --rm -it -e DISPLAY=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}'):0 my-anaconda3
```

## License

This is licensed under the [MIT](https://github.com/asakaguchi/dockerfiles/blob/master/LICENSE) license.