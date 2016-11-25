# alpine-anaconda3 / Dockerfile

This Dockerfile is a file for building a Python environment with Anaconda3 on Alpine Linux.

## Requirements

* [Docker](https://www.docker.com) 1.12.1+

## Usage

To create a Docker image, use the following command:

```text
docker build -t my-anaconda3 .
```

To run the Docker image you just created, use the following command:

```text
docker run -it my-anaconda3
```

## License

This is licensed under the [MIT](https://github.com/asakaguchi/dockerfiles/blob/master/LICENSE) license.