# Go Get Dependencies

An unopinionated Go dependency installer,
this script searches for dependencies of your Go project and installs them
via `go get`. It is meant to be run from your project's directory.
Test dependencies are also installed.
Unlike standard Go tools, go-get-dependencies is agnostic to your
project's location on the filesystem and its organization.

## Background

The [standard code organization prescribed by go tool](https://golang.org/doc/code.html)
requires having the actual project code several levels deep into the filesystem,
and also requires having a "Go workspace" under which all Go code is stored.
While I can see how this might make sense for companies working primarily
or exclusively in Go, I organize my code differently:
all of my projects are under `~/apps` and very few of them
are written in Go. For ease of access I do want all of the projects
to be two levels down from the home directory (`~`).

`go-get-dependencies` is a tool which installs Go dependencies without caring
about the project structure or what `GOPATH` is set to in relation to the
project's location. It just installs the dependencies.

## Usage

To build a Go project using go-get-deps, you could run:

    # Anywhere on the filesystem is fine
    export GOPATH=/tmp/gopath
    
    wget https://raw.githubusercontent.com/p/go-get-deps/master/go-get-deps
    
    python go-get-deps
    
    go build project.go

## How It Works

`go-get-dependencies` looks for `*.go` files in the current directory and
subdirectories. In each Go file the script looks for the first
`import ( ... )` block. For each import in that block, it then checks whether
the import starts with what appears to be a domain name (`xxx.yyy`, something
with a dot). Such imports are collected and go-got.

## Caveats

Import matching is somewhat rudimentary. If this script does not work,
`go fmt` your code and try again.

## License

Released under the MIT license.
