# escaper [![GoDoc](http://img.shields.io/badge/go-documentation-blue.svg?style=flat_square)](http://godoc.org/github.com/lucasem/escaper)

**`escaper`** lets you create your own formatting syntax. By design,
expanding a format string with this utility requires no additional arguments
(unlike fmt.Sprinf) by letting you easily register your own escape handlers.

![escaper](http://i.imgur.com/qAAPq5y.png)

## Install

```bash
go get github.com/lucasem/escaper
```

## Examples

### Basics

```go
format := "add some ANSI %F{blue}text color%f easily"

esc := escaper.Default()
output := esc.Expand(format)
```

### Advanced

```go
format := "my name is %n, and the time is %D{3:04PM}"
name := "Ben Bitdiddle"

// use New() if you don't want the default ANSI escapes
esc := escaper.New()
esc.Register('n', func() string {
  return name
})
esc.RegisterArg('D', func(arg string) string {
  return time.Now().Format(arg)
})
output := esc.Expand(format)
```

## The Default

The default escaper supports the following:
- `%F{<color>}some text%f` colors the text
- `%K{<color>}some text%k` colors the background
- `%Bsome text%b` bolds the text
- `%Usome text%u` underlines the text
- `%Ssome text%s` standouts (color inverts) the text

`<color>` can be one of:
- `black`, or `0`
- `red`, or `1`
- `green`, or `2`
- `yellow`, or `3`
- `blue`, or `4`
- `magenta`, or `5`
- `cyan`, or `6`
- `white`, or `7`

## License

The MIT License (MIT) - see [`LICENSE`](https://github.com/lucasem/escaper/blob/master/LICENSE) for details
