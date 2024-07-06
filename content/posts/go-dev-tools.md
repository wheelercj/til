+++
title = 'Go dev tools'
date = 2024-07-02T01:14:26-07:00
lastmod = 2024-07-05T14:14:54-07:00
+++

Below are a bunch of commonly used packages and other tools for software development with Go. Go has excellent backwards and forwards compatability, so tools that haven't been updated in a long time may still be a great choice. Unless otherwise noted, each tool listed here appears to me to be good enough at what it does that I don't feel the need to look at alternatives.

If you're new to Go, check out [Learning Go](/intro-to-go).

{{< toc >}}

## Miscellaneous

#### [godotenv](https://pkg.go.dev/github.com/joho/godotenv)

`import "github.com/joho/godotenv"`

Load environment variables from .env files.

#### [lumberjack](https://github.com/natefinch/lumberjack)

`import "gopkg.in/natefinch/lumberjack.v2"`

A log rolling package for Go. This can be used as the backend behind the Go standard library's `log/slog` package.

#### [gorilla/websocket](https://github.com/gorilla/websocket)

`import "github.com/gorilla/websocket"`

gorilla/websocket is a fast, well-tested and widely used WebSocket implementation for Go. It passes the server tests in the [Autobahn Test Suite](https://github.com/crossbario/autobahn-testsuite).

#### [templ](https://templ.guide/)

`go install github.com/a-h/templ/cmd/templ@latest`

Create components that render fragments of HTML and compose them to create screens, pages, documents, or apps. Using templ with [htmx](https://htmx.org/) is popular because it provides "many of the benefits of React with reduced overall complexity." React can also be used with templ; see [Using React with templ | templ docs](https://templ.guide/syntax-and-usage/using-react-with-templ/).

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

#### [gonew](https://go.dev/blog/gonew)

`go install golang.org/x/tools/cmd/gonew@latest`

A tool for instantiating new projects in Go from predefined templates.

#### [air](https://github.com/air-verse/air)

`go install github.com/air-verse/air@latest`

Live reload for Go apps. I'm not interested in this, but I often see people new to Go ask if something like this exists.

## Code analysis

#### [golangci-lint](https://github.com/golangci/golangci-lint)

Fast linters runner for Go. They have an [official GitHub Action](https://github.com/golangci/golangci-lint-action).

#### [NilAway](https://github.com/uber-go/nilaway)

Practical nil panic detection for Go. Created by Uber, this static analysis tool can be installed and used locally, but is recommended to be used with a system like golangci-lint.

#### [goleak](https://github.com/uber-go/goleak)

`import "go.uber.org/goleak"`

A goroutine leak detector created by Uber.

#### [deadcode](https://go.dev/blog/deadcode)

`go install golang.org/x/tools/cmd/deadcode@latest`

Find unreachable functions. This tool never accidentally says a reachable function is unreachable, unless it's only called from code not written in Go. Its creators "run deadcode periodically on our projects, especially after refactoring work, to help identify parts of the program that are no longer needed."

## Database tools

#### [pgx](https://github.com/jackc/pgx)

`import "github.com/jackc/pgx/v5"`

A PostgreSQL driver and toolkit for Go. Postgres seems to be by far the most popular choice among the SQL technologies in Go.

#### [sqlc](https://github.com/sqlc-dev/sqlc)

`go install github.com/sqlc-dev/sqlc/cmd/sqlc@latest`

Generate type-safe code from SQL. sqlc is Go's most popular query builder and use of query builders is popular in Go; use of ORMs is strongly discouraged by almost all Go developers.

#### [goose](https://github.com/pressly/goose)

`go install github.com/pressly/goose/v3/cmd/goose@latest`

A database migration tool that supports SQL migrations and Go functions. I haven't looked into alternatives for this yet.

## HTTP routers

In Go, it's common to build web servers without using a framework because Go has several excellent routers.

The Go standard library's [net/http](https://pkg.go.dev/net/http) package has only the most basic features but is said to have the best performance.

Among third-party routers, [chi](https://github.com/go-chi/chi) and [gorilla/mux](https://github.com/gorilla/mux) are probably the most widely used. They are very similar. It appears gorilla/mux was more popular than chi in the past, but chi started catching up when gorilla/mux temporarily went unmaintained for a while. In online discussions, I almost always see people prefer chi over gorilla/mux. chi was implemented with a trie and gorilla/mux was implemented with regex.

`import "github.com/go-chi/chi/v5"`

`import "github.com/gorilla/mux"`

[Here's a big list of more routers](https://github.com/avelino/awesome-go?tab=readme-ov-file#routers).

## HTTP frameworks

Although Go has many HTTP frameworks, below are just the ones I hear about often. Using a framework solves some problems, but also creates problems. For some use cases, they create more problems than they solve. [Here's a more complete list of HTTP frameworks](https://github.com/avelino/awesome-go#web-frameworks).

#### [Echo](https://github.com/labstack/echo)

`import "github.com/labstack/echo/v4"`

Echo appears to be the current most popular framework for new projects. It's minimal, has a lot of middlewares available, and is one of the highest-performance frameworks. A commonly mentioned downside is that it's different from Go's standard library.

#### [Fiber](https://gofiber.io/)

`import "github.com/gofiber/fiber/v2"`

Fiber's design is based on Express, the JavaScript framework. It has the best performance out of all of Go's widely used frameworks, but is specialized for specific use cases and does not support some things like detecting when the client has closed the site's tab.

#### [Gin](https://github.com/gin-gonic/gin)

`import "github.com/gin-gonic/gin"`

Gin might be Go's most widely used HTTP framework, but in online discussions, almost all Go developers recommend against using it for a wide variety of reasons. Some describe it as "bloated" or as a framework designed for developers that prefer Java. Gin uses custom interfaces that make it incompatible with much of the rest of the ecosystem. Apparently it also has poor performance and error handling.

## Desktop app frameworks

Web-based GUI frameworks have way more features than native GUI frameworks, but may require more work to create simple GUIs.

#### [Wails](https://wails.io/)

`go install github.com/wailsapp/wails/v2/cmd/wails@latest`

Wails is a toolkit for creating web-based GUIs with Go. This is Go's version of Electron or Tauri and is significantly more efficient than Electron.

#### [Fyne](https://fyne.io/)

`import "fyne.io/fyne/v2@latest"` and `go install fyne.io/fyne/v2/cmd/fyne@latest`

Fyne is a toolkit for creating native GUIs with Go.
