# Go Get Dependencies

This script searches for dependencies of your Go project and installs them
via `go get`. It is meant to be run from your project's directory.
Test dependencies are also installed.

## How It Works

`go-get-dependencies` looks for `*.go` files in the current directory and
subdirectories. In each Go file the script looks for the first
`import ( ... )` block. For each import in that block, it then checks whether
the import starts with what appears to be a domain name (`xxx.yyy`, something
with a dot). Such imports are collected and go-got.

## Why

This script does not care if you use symlinks, how your code is organized,
whether your project is inside GOPATH, etc. It just works.
(You still need to have `GOPATH` set for `go get` to function.)

## Caveats

Import matching is somewhat rudimentary. If this script does not work,
`go fmt` your code and try again.

## License

Released under the MIT license.
