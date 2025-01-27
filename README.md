![kratos](docs/images/kratos.png) 

[![Language](https://img.shields.io/badge/Language-Go-blue.svg)](https://golang.org/)
[![Build Status](https://github.com/go-kratos/kratos/workflows/Go/badge.svg)](https://github.com/go-kratos/kratos/actions)
[![GoDoc](https://pkg.go.dev/badge/github.com/go-kratos/kratos/v2)](https://pkg.go.dev/github.com/go-kratos/kratos/v2)
[![Go Report Card](https://goreportcard.com/badge/github.com/go-kratos/kratos)](https://goreportcard.com/report/github.com/go-kratos/kratos)
[![Discord](https://img.shields.io/discord/766619759214854164?label=chat&logo=discord)](https://discord.gg/BWzJsUJ)

Translations: [English](README.md) | [简体中文](README_zh.md)

# Kratos
Kratos is a microservice-oriented governance framework implements by golang, which offers convenient capabilities to help you quickly build a bulletproof application from scratch.


>The name is inspired by the game God of War which is based on Greek myths, tells the Kratos from mortals to become a God of War and launches the adventure of killing god.


## Goals

Kratos boosts your productivity. With the integration of excellent resources and further support, programmers can get rid of most issues might encounter in the field of distributed systems and software engineering such that they are allowed to focus on the release of businesses only. Additionally, for each programmer, Kratos is also an ideal one learning warehouse for many aspects of microservices to enrich their experiences and skills.
### Principles

* **Simple**: Appropriate design, plain and easy code.
* **General**: Cover the various utilities for business development.
* **Highly efficient**: Speeding up the efficiency of businesses upgrading.
* **Stable**: The base libs validated in the production environment which have the characters of the high testability, high coverage as well as high security and reliability.
* **Robust**: Eliminating misusing through high quality of the base libs.
* **High-performance**: Optimal performance excluding the optimization of hacking in case of *unsafe*. 
* **Expandability**: Properly designed interfaces, you can expand utilities such as base libs to meet your further requirements.
* **Fault-tolerance**: Designed against failure, enhance the understanding and exercising of SRE within Kratos to achieve more robustness.
* **Toolchain**: Includes an extensive toolchain, such as the code generation of cache, the lint tool, and so forth.

## Features
* [APIs](examples/helloworld/helloworld): The communication protocol is based on the HTTP/gRPC through the definition of Protobuf.
* [Errors](examples/errors/api): Both the definitions of error code and the handle interfaces of code generation for tools are defined by the Enum of the Protobuf.
* [Metadata](examples/metadata): In the protocol of HTTP/gRPC, the transmission of service atomic information are formalized by the Middleware.
* [Config](examples/config): Multiple data sources are supported for configurations and integrations such that dynamic configurations are offered through the manner of *Atomic* operations.
* [Logger](examples/log): The standard log interfaces ease the integration of the third-party log libs and logs are collected through the *Fluentd*.
* [Metrics](examples/metrics): *Prometheus* integrated by default. Furthermore, with the uniform metric interfaces, you can implement your own metric system more flexible.
* [Tracing](examples/traces): The OpenTelemetry is conformed to achieve the tracing of microservices chains.
* [Encoding](encoding): The selection of the content encoding is automatically supported by Accept and Content-Type.
* [Transport](transport/transport.go): The uniform plugins for [Middleware](middleware) are supported by [HTTP](examples/http/middlewares)/[gRPC](examples/middleware/main.go).
* [Registry](examples/registry): The interfaces of the centralized registry is able to be connected with various other centralized registries through plug-ins.
* [Validation](examples/validate): Verification rules defined in Protobuf can be supported by HTTP/gRPC service.
* [SwaggerAPI](https://github.com/go-kratos/swagger-api/blob/main/examples/helloworld/server/main.go): Swagger API generated Automatically and embed Swagger UI endpoint can be started by adding [Swagger plugin](https://github.com/go-kratos/swagger-api).

## Getting Started
### Required
- [go](https://golang.org/dl/)
- [protoc](https://github.com/protocolbuffers/protobuf)
- [protoc-gen-go](https://github.com/protocolbuffers/protobuf-go)

### Installing
##### install from go get:
```
go get github.com/go-kratos/kratos/cmd/kratos/v2@latest
kratos upgrade
```
##### install from source code：
```
git clone https://github.com/go-kratos/kratos
cd kratos
make install
```

### Create a service
```
# create project template
kratos new helloworld

cd helloworld
# download modules
go mod download

# generate Proto template
kratos proto add api/helloworld/helloworld.proto
# generate Proto source code
kratos proto client api/helloworld/helloworld.proto
# generate server template
kratos proto server api/helloworld/helloworld.proto -t internal/service

# generate all proto source code, wire, etc.
go generate ./...

# run
kratos run
```

### Kratos Boot
```
import "github.com/go-kratos/kratos/v2"
import "github.com/go-kratos/kratos/v2/transport/grpc"
import "github.com/go-kratos/kratos/v2/transport/http"

httpSrv := http.NewServer(http.Address(":8000"))
grpcSrv := grpc.NewServer(grpc.Address(":9000"))

app := kratos.New(
    kratos.Name("kratos"),
    kratos.Version("latest"),
    kratos.Server(httpSrv, grpcSrv),
)
app.Run()
```

## Related

* [Tutorial](https://go-kratos.dev/docs/getting-started/start)
* [Examples](./examples)
* [Project Template](https://github.com/go-kratos/kratos-layout)
* [FAQ](https://go-kratos.dev/docs/getting-started/faq)

## Community
* [Wechat Group](https://github.com/go-kratos/kratos/issues/682)
* [Discord Group](https://discord.gg/BWzJsUJ)
* Website:  [go-kratos.dev](https://go-kratos.dev)
* QQ Group: 716486124

## Conventional commits
The structure of the commit message should look like the following
```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

The information should be commit in the following format:
- fix: simply describe the problem that has been fixed
- feat(log): simple describe of new features
- deps(examples): simple describe the change of the dependency
- break(http): simple describe the reasons for breaking change

## License
Kratos is MIT licensed. See the [LICENSE](./LICENSE) file for details.

## Contributors
Thanks for their outstanding contributions.
<a href="https://github.com/go-kratos/kratos/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=go-kratos/kratos" />
</a>
