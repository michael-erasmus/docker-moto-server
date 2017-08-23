# docker-moto-server

Docker build for running a local [moto](https://github.com/spulec/moto) [stand-alone server](https://github.com/spulec/moto#stand-alone-server-mode)

This is useful for doing local integration testing of clients that use AWS services without actually hitting AWS

## Usage

Start a local kinesis service

```sh
docker run -it --rm --net=host michaelerasmus/moto-server kinesis
```

To test it. Make sure you have aws-cli installed

```sh
aws kinesis list-streams --endpoint-url http://localhost:5000
```

Using it in docker-compose:

```yaml
version: "3"
services:
  kinesis:
    image: michaelerasmus/moto-server
    command: ["kinesis", "-H",  "0.0.0.0"]
    expose:
      - "5000"

```

Building the image locally:

```
git clone https://github.com/michael-erasmus/docker-moto-server
cd docker-moto-server
docker build -t michaelerasmus/moto-server .
```

Using a custom `Dockerfile`:

```Dockerfile
FROM michaelerasmus/moto-server

#Customize things here
```

## License

[MIT License](/LICENSE) © 2017 Michael Erasmus
