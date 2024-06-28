+++
title = 'Learning Go'
date = 2022-11-22T17:39:10-08:00
lastmod = 2024-06-28T16:02:24-07:00
+++

Here are various resources that are good to know about if you want to start learning the Go programming language.

* [A Tour of Go](https://go.dev/tour/welcome/1) is probably the best way to start learning Go
* [go.dev/learn](https://go.dev/learn/)
* [Go Playground](https://go.dev/play/) is an online Go editor and runner
* [Go FAQs](https://go.dev/doc/faq)
* [Jamie Tanna's guide to learning Go](https://www.jvt.me/posts/2022/08/12/learning-new-language-go/)
* [Tutorial: Get started with Go](https://go.dev/doc/tutorial/getting-started)
* [Learn X in Y minutes where X=Go](https://learnxinyminutes.com/docs/go/)
* [_Learn Go With Tests_](https://quii.gitbook.io/learn-go-with-tests) by quii and Denise
* [Anthony GG - YouTube](https://www.youtube.com/@anthonygg_/videos)
* [Don't defer Close() on writable files](https://www.joeshaw.org/dont-defer-close-on-writable-files/) by Joe Shaw
* [publishing Go packages](/publishing-go-packages)
* [Profiling Go Programs](https://go.dev/blog/pprof) (using pprof) by Russ Cox and Shenghou Ma
* [How to write benchmarks in Go](https://dave.cheney.net/2013/06/30/how-to-write-benchmarks-in-go) by Dave Cheney
* [Finding unreachable functions with deadcode](https://go.dev/blog/deadcode) by Alan Donovan
* [Experimenting with project templates](https://go.dev/blog/gonew) (using gonew) by Cameron Balahan

## third party libraries, frameworks, and tools

* [Cobra](https://github.com/spf13/cobra) by spf13 – for creating command-line interfaces
* [Viper](https://github.com/spf13/viper) by spf13 – configuration management
* [NilAway](https://github.com/uber-go/nilaway/?uclick_id=43206374-f01b-4b03-9250-506f8c102a81) by Uber – practical nil panic detection for Go
* [goleak](https://github.com/uber-go/goleak) by Uber - Goroutine leak detector
* [Wails](https://wails.io/) – a toolkit for creating web-based GUIs with Go
* [Fyne](https://fyne.io/) – a toolkit for creating GUIs with Go
* [Go Databases](https://blog.teamortix.com/posts/2021/08/go-databases/) by Hamza Ali – comparisons of various Go database libraries and why to not use an ORM
* [golangci-lint](https://github.com/golangci/golangci-lint) – fast linters runner for Go
* [Gokrazy](https://news.ycombinator.com/item?id=37583234) – deploy Go programs as appliances to a Raspberry Pi or PC

## web API tech

With most programming languages, you would almost always want to use a framework when creating API backend services. Go has many frameworks too, but also some excellent non-framework alternatives that many people prefer:

* [the Go standard library's net/http package](https://pkg.go.dev/net/http) – an HTTP client and server implementation
* [gorilla/mux](https://github.com/gorilla/mux) – an HTTP router
* [chi](https://github.com/go-chi/chi) – an HTTP router

### frameworks

Although there are many others, here are a few I hear about often:

* [Echo](https://github.com/labstack/echo)
* [Gin](https://github.com/gin-gonic)
* [Fiber](https://gofiber.io/)

### guides

* [4 Things to Consider When Choosing a Go API Framework](https://markphelps.me/posts/4-things-to-consider-when-choosing-a-go-api-framework/) by Mark Phelps
* [Error handling in Go HTTP applications](https://www.joeshaw.org/error-handling-in-go-http-applications/) by Joe Shaw
* [How To Use Contexts in Go | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-use-contexts-in-go)
* [Backend from the Beginning](https://eblog.fly.dev/backendbasics.html) by Efron Licht
