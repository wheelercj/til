+++
title = 'Learning Go'
date = 2022-11-22T17:39:10-08:00
lastmod = 2024-07-06T12:34:41-07:00
+++

Here are various resources that are good to know about if you want to start learning the Go programming language.

I created a list of commonly used Go packages and other dev tools at [Go dev tools](/go-dev-tools).

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
* [Go Roadmap - roadmap.sh](https://roadmap.sh/golang)
* [Go Programming Language Wiki](https://zchee.github.io/golang-wiki/)

### miscellaneous

* [Pointers vs. references](/pointers-vs-references)
* [Go Databases](https://blog.teamortix.com/posts/2021/08/go-databases/) by Hamza Ali - comparisons of various Go database libraries and why to not use an ORM
* [Logging in Go with Slog: The Ultimate Guide](https://betterstack.com/community/guides/logging/logging-in-go/) by Better Stack Community
* [Don't defer Close() on writable files](https://www.joeshaw.org/dont-defer-close-on-writable-files/) by Joe Shaw
* [My favorite build options for Go](https://opensource.com/article/22/4/go-build-options), by Gaurav Kamathe, covers commands that show how Go creates binaries, what intermediate assembly it uses, and how to make Go binaries smaller.
* [Interface Upgrades in Go](https://avtok.com/2014/11/05/interface-upgrades.html) by Avtok
* [Reading Google Sheets from a Go program](https://eli.thegreenplace.net/2024/reading-google-sheets-from-a-go-program/) by Eli Bendersky

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
* [Gokrazy](https://news.ycombinator.com/item?id=37583234) - deploy Go programs as appliances to a Raspberry Pi or PC

### contexts

* [How To Use Contexts in Go](https://www.digitalocean.com/community/tutorials/how-to-use-contexts-in-go) by DigitalOcean
* [Context Control in Go](https://zenhorace.dev/blog/context-control-go/)

### profiling, benchmarking, & execution tracing

* [Profiling Go Programs](https://go.dev/blog/pprof) (using pprof) by Russ Cox and Shenghou Ma
* [How to write benchmarks in Go](https://dave.cheney.net/2013/06/30/how-to-write-benchmarks-in-go) by Dave Cheney
* [More powerful Go execution traces](https://go.dev/blog/execution-traces-2024)
