+++
title = 'Learning Go'
date = 2022-11-22T17:39:10-08:00
lastmod = 2024-07-01T18:16:31-07:00
+++

Here are various resources that are good to know about if you want to start learning the Go programming language.

## getting started

* if you're new to programming, check out [Golang Tutorial For Beginners - YouTube](https://www.youtube.com/watch?v=Q0sKAMal4WQ)
* [A Tour of Go](https://go.dev/tour/welcome/1) is probably the best way for developers with experience in another language to start learning Go
* [Go Playground](https://go.dev/play/) is an online Go editor and runner
* [Tutorial: Get started with Go](https://go.dev/doc/tutorial/getting-started)
* [Go by Example](https://gobyexample.com/)
* [Go FAQs](https://go.dev/doc/faq)
* [go.dev/learn](https://go.dev/learn/)
* [Effective Go](https://go.dev/doc/effective_go)
* [Jamie Tanna's guide to learning Go](https://www.jvt.me/posts/2022/08/12/learning-new-language-go/)
* [Learn X in Y minutes where X=Go](https://learnxinyminutes.com/docs/go/)
* [_Learn Go With Tests_](https://quii.gitbook.io/learn-go-with-tests) by quii and Denise
* [Anthony GG - YouTube](https://www.youtube.com/@anthonygg_/videos)
* [Advent of Code](https://adventofcode.com/) is a great way to get practice with a new language
* [How To Code in Go](https://www.digitalocean.com/community/tutorial-series/how-to-code-in-go) is a list of many guides written by DigitalOcean
* [Go Programming Language Wiki](https://zchee.github.io/golang-wiki/)

### miscellaneous

* [Go Databases](https://blog.teamortix.com/posts/2021/08/go-databases/) by Hamza Ali - comparisons of various Go database libraries and why to not use an ORM
* [Logging in Go with Slog: The Ultimate Guide](https://betterstack.com/community/guides/logging/logging-in-go/) by Better Stack Community
* [Don't defer Close() on writable files](https://www.joeshaw.org/dont-defer-close-on-writable-files/) by Joe Shaw
* [My favorite build options for Go](https://opensource.com/article/22/4/go-build-options), by Gaurav Kamathe, covers commands that show how Go creates binaries, what intermediate assembly it uses, and how to make Go binaries smaller.
* [Interface Upgrades in Go](https://avtok.com/2014/11/05/interface-upgrades.html) by Avtok

### error handling

* [A Beautiful Way To Deal With ERRORS in Golang HTTP Handlers - YouTube](https://www.youtube.com/watch?v=aS1cJfQ-LrQ)
* [Error handling in Go HTTP applications](https://www.joeshaw.org/error-handling-in-go-http-applications/) by Joe Shaw
* [How to Add Extra Information to Errors in Go](https://www.digitalocean.com/community/tutorials/how-to-add-extra-information-to-errors-in-go) by DigitalOcean

### web APIs

* [4 Things to Consider When Choosing a Go API Framework](https://markphelps.me/posts/4-things-to-consider-when-choosing-a-go-api-framework/) by Mark Phelps
* [Backend from the Beginning](https://eblog.fly.dev/backendbasics.html) by Efron Licht

### deployment and distribution

* [Go docker images: small and simple](https://laurentsv.com/blog/2024/06/25/stop-the-go-and-docker-madness.html) by Laurent Demailly
* [GoogleContainerTools/distroless](https://github.com/GoogleContainerTools/distroless) - language focused docker images, minus the operating system
* [publishing Go packages](/publishing-go-packages)
* [GoReleaser](https://goreleaser.com/) - release Go projects as fast and easily as possible
* [GoReleaser Action](https://github.com/marketplace/actions/goreleaser-action) - a GitHub Action for GoReleaser
* [Gokrazy](https://news.ycombinator.com/item?id=37583234) - deploy Go programs as appliances to a Raspberry Pi or PC

### contexts

* [How To Use Contexts in Go](https://www.digitalocean.com/community/tutorials/how-to-use-contexts-in-go) by DigitalOcean
* [Context Control in Go](https://zenhorace.dev/blog/context-control-go/)

### profiling, benchmarking, & execution tracing

* [Profiling Go Programs](https://go.dev/blog/pprof) (using pprof) by Russ Cox and Shenghou Ma
* [How to write benchmarks in Go](https://dave.cheney.net/2013/06/30/how-to-write-benchmarks-in-go) by Dave Cheney
* [More powerful Go execution traces](https://go.dev/blog/execution-traces-2024)

## packages

### miscellaneous

* [godotenv](https://pkg.go.dev/github.com/joho/godotenv) by John Barton - loads environment variables from .env files
* [lumberjack](https://github.com/natefinch/lumberjack) by Nate Finch - a log rolling package for Go
* [air](https://github.com/air-verse/air) - live reload for Go apps
* [Cobra](https://github.com/spf13/cobra) by spf13 - for creating command-line interfaces
* [Viper](https://github.com/spf13/viper) by spf13 - configuration management
* [NilAway](https://github.com/uber-go/nilaway) by Uber - practical nil panic detection for Go
* [goleak](https://github.com/uber-go/goleak) by Uber - Goroutine leak detector
* [gonew](https://go.dev/blog/gonew) by Cameron Balahan - project templates
* [deadcode](https://go.dev/blog/deadcode) by Alan Donovan - find unreachable functions
* [Reading Google Sheets from a Go program](https://eli.thegreenplace.net/2024/reading-google-sheets-from-a-go-program/) by Eli Bendersky
* [golangci-lint](https://github.com/golangci/golangci-lint) - fast linters runner for Go
* I've also starred [a bunch of Go dev tools](https://github.com/stars/wheelercj/lists/go-dev-tools) that I like or plan to try in the future

### databases

* [sqlc](https://github.com/sqlc-dev/sqlc) - generate type-safe code from SQL
* [goose](https://github.com/pressly/goose) by pressly - a database migration tool that supports SQL migrations and Go functions

### web API routers

For small web servers, a framework might just be unnecessary complexity. Routers are perfect for these situations.

* [the Go standard library's net/http package](https://pkg.go.dev/net/http) - an HTTP client and server implementation
* [gorilla/mux](https://github.com/gorilla/mux) - an HTTP router
* [chi](https://github.com/go-chi/chi) - an HTTP router

### web API frameworks

Although there are many others, here are a few I hear about often:

* [Echo](https://github.com/labstack/echo)
* [Gin](https://github.com/gin-gonic)
* [Fiber](https://gofiber.io/)

## desktop apps

* [Wails](https://wails.io/) - a toolkit for creating web-based GUIs with Go
* [Fyne](https://fyne.io/) - a toolkit for creating GUIs with Go
