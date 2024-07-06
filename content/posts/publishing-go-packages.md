+++
title = 'Publishing Go packages'
date = 2024-01-12T17:14:08-08:00
lastmod = 2024-01-15T07:35:02-08:00
+++

There are many ways you can share Go code and applications. Here are a few.

## publishing to the Go package index (pkg.go.dev)

This allows anyone with Go installed to download your package with `go get` or `go install`. `go get` is for getting code, and `go install` is for installing executables (more details on that in [the Go docs](https://go.dev/doc/go-get-install-deprecation) and [this Stack Overflow discussion](https://stackoverflow.com/questions/24878737/what-is-the-difference-between-go-get-and-go-install)).

Here are the official docs on publishing to pkg.go.dev:

* [Publishing Go Modules](https://tip.golang.org/blog/publishing-go-modules)
* [Publishing a module](https://go.dev/doc/modules/publishing)
    * The PowerShell equivalent of the command in step 6 is {{< highlight powershell >}}$env:GOPROXY="proxy.golang.org" && go list -m example.com/mymodule@v0.1.0{{< /highlight >}}

The package may take some time to appear in the package index because the servers are not always running at 100%. If you want to, you may be able to speed up indexing by searching for your package at pkg.go.dev, or especially by using `go get` on the package.

## Homebrew and Snap

Although I haven't tried it myself, [this repo](https://github.com/wakatara/harsh) appears to be a good example of how to automatically publish to the Homebrew and Snap package managers.

## as executable files (binaries)

With Go, it's super easy to create and publish executables for all major platforms using [GoReleaser](https://goreleaser.com/) and [the GoReleaser GitHub Action](https://github.com/marketplace/actions/goreleaser-action). You can see an example of the result [here](https://github.com/wheelercj/email-linter/releases). If you publish your executables on the web, you may want to also [submit the Windows executable(s) to Microsoft for malware analysis](https://www.microsoft.com/en-us/wdsi/filesubmission) as a software developer to try to prevent users from getting the Windows Defender SmartScreen warning.
