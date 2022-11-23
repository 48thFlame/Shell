# Command-shell

A go library for creating simple command-based `tui`'s (terminal user interfaces).
Built on top of this [keyboard package](https://github.com/eiannone/keyboard).

## Features/TODO

- [x] Default `exit` command
- [x] Minimal number of arguments safety
- [x] Customizable `LinePrefix`
- [ ] Commands can store data
- [ ] Default & automatic `help` command
- [ ] Up-arrow for previous command
- [ ] History
- [ ] Tab autocomplete
- [ ] Cursor moving around line
- [ ] And more...

## Example

### output

```terminal
> add 2 6
8
>
```

### code

```go
package main

import (
    "fmt"
    "strconv"

    "github.com/48thFlame/Command-shell"
)

func addCommand(input *shell.CommandHandlerInput) error {
    args := input.Args
    a, err := strconv.Atoi(args[0])
    if err != nil {
        return err
    }
    b, err := strconv.Atoi(args[1])
    if err != nil {
        return err
    }

    fmt.Fprint(input.Stdout, a+b)

    return nil
}

func main() {
    s, err := shell.NewShell(shell.NewCommand("add", 2, addCommand))
    if err != nil {
        panic(err)
    }

    err = s.Run()
    if err != nil {
        panic(err)
    }
}
```
