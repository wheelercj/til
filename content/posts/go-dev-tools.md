+++
title = 'Go dev tools'
date = 2024-07-02T01:14:26-07:00
+++

Below are a bunch of commonly used packages and other tools for software development with Go. If you're new to Go, check out [Learning Go](/intro-to-go).

{{< toc >}}

## Miscellaneous

#### [godotenv](https://pkg.go.dev/github.com/joho/godotenv)

`import "github.com/joho/godotenv"`

Load environment variables from .env files.

#### [lumberjack](https://github.com/natefinch/lumberjack)

`import "gopkg.in/natefinch/lumberjack.v2"`

A log rolling package for Go. This can be used as the backend behind the Go standard library's `log/slog` package.

#### [air](https://github.com/air-verse/air)

`go install github.com/air-verse/air@latest`

Live reload for Go apps.

#### [Cobra](https://github.com/spf13/cobra)

`import "github.com/spf13/cobra"`

A library for creating powerful modern CLI applications.

#### [cobra-cli](https://github.com/spf13/cobra-cli/blob/main/README.md)

`go install github.com/spf13/cobra-cli@latest`

A tool for generating Cobra code made by the creators of Cobra.

#### [Viper](https://github.com/spf13/viper)

`import "github.com/spf13/viper"`

A complete configuration solution for Go applications including [12-Factor apps](https://12factor.net/#the_twelve_factors). This was also made by the creators of Cobra.

#### [GoReleaser](https://goreleaser.com/)

Release Go projects as fast and easily as possible. There's an [official GitHub Action](https://github.com/marketplace/actions/goreleaser-action).

#### [golangci-lint](https://github.com/golangci/golangci-lint)

Fast linters runner for Go. They have an [official GitHub Action](https://github.com/golangci/golangci-lint-action).

#### [NilAway](https://github.com/uber-go/nilaway)

`go install go.uber.org/nilaway/cmd/nilaway@latest`

Practical nil panic detection for Go. Created by Uber.

#### [goleak](https://github.com/uber-go/goleak)

`import "go.uber.org/goleak"`

A goroutine leak detector created by Uber.

#### [gonew](https://go.dev/blog/gonew)

`go install golang.org/x/tools/cmd/gonew@latest`

A tool for instantiating new projects in Go from predefined templates.

#### [deadcode](https://go.dev/blog/deadcode)

`go install golang.org/x/tools/cmd/deadcode@latest`

Find unreachable functions.

## Databases

#### [sqlc](https://github.com/sqlc-dev/sqlc)

`go install github.com/sqlc-dev/sqlc/cmd/sqlc@latest`

Generate type-safe code from SQL.

#### [goose](https://github.com/pressly/goose)

`go install github.com/pressly/goose/v3/cmd/goose@latest`

A database migration tool that supports SQL migrations and Go functions.

## HTTP routers

In Go, it's common to build web servers without using a framework because Go has an excellent alternative to frameworks: routers. They're often best for APIs that aren't serving frontend content.

[The Go standard library's net/http package](https://pkg.go.dev/net/http) has only the most basic features but is said to have the best performance.

Among third-party routers, [chi](https://github.com/go-chi/chi) and [gorilla/mux](https://github.com/gorilla/mux) are probably the most widely used. They are very similar in nearly every way. It appears gorilla/mux was more popular than chi in the past, but chi started catching up when gorilla/mux temporarily went unmaintained for a while. In online discussions, I usually see people prefer chi over gorilla/mux. gorilla/mux was implemented with regex and chi was implemented with a trie.

`import "github.com/go-chi/chi/v5"`

`import "github.com/gorilla/mux"`

[Here's a big list of more routers](https://github.com/avelino/awesome-go?tab=readme-ov-file#routers).

## HTTP frameworks

Although Go has many HTTP frameworks, below are just a few I hear about often. [Here's a more complete list](https://github.com/avelino/awesome-go#web-frameworks).

#### [Echo](https://github.com/labstack/echo)

`import "github.com/labstack/echo/v4"`

Echo appears to be the current most popular framework for new projects. It's minimal, has a lot of middlewares available, and is one of the highest-performance frameworks. A commonly mentioned downside is that it's different from Go's standard library.

#### [Gin](https://github.com/gin-gonic/gin)

`import "github.com/gin-gonic/gin"`

Gin is probably Go's most widely used HTTP framework, but it seems to be rare for anyone to recommend using it now. I've seen some describe it as "bloated", and others were surprised there's an official Go guide for using Gin.

#### [Fiber](https://gofiber.io/)

`import "github.com/gofiber/fiber/v2"`

Fiber's design is based on Express, the JavaScript framework. It has the best performance out of all of Go's widely used frameworks, but is specialized for specific cases and does not support some things like detecting when the client has closed the site's tab.

## Desktop apps

Web-based GUI frameworks tend to have way more features than native GUI frameworks.

#### [Wails](https://wails.io/)

`go install github.com/wailsapp/wails/v2/cmd/wails@latest`

Wails is a toolkit for creating web-based GUIs with Go. This is Go's version of Electron or Tauri and is significantly more efficient than Electron.

#### [Fyne](https://fyne.io/)

`import "fyne.io/fyne/v2@latest"` and `go install fyne.io/fyne/v2/cmd/fyne@latest`

Fyne is a toolkit for creating native GUIs with Go.
