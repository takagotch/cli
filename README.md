### cli
---
https://github.com/urfave/cli

https://github.com/mitchellh/cli
https://github.com/hidevopsio/hiboot/tree/master/pkg/app/cli
https://github.com/mkideal/cli
https://github.com/teris-io/cli

```sh
go get github.com/urffa/cli
export PATH=$PATH:$GOPATH/bin
go get gopkg.in/urfave/cli.v2
go get gopkg.in/urfave/cli.v1
go install
greet
greet help
sudo cp src/bash_autocomplete /etc/bash_completion.d/<myprogram>
source /etc/bash_completion.d/<myprogram>
cmd foobar -s -o
cmd foobar -so
```

```go
import (
  "gopkg.in/urfave/cli.v2" 
)

import (
  "gopkg.in/urfave/cli.v1"
)

package main

import (
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  err := cli.NewApp().Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}

package main

import (
  "fmt"
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  app := "boom"
  app.Name = "boom"
  app.Usage = "make an explosive entrance"
  app.Action = func(c *cli.Context) error {
    fmt.Println("boom! I say!")
    return nil
  }
  
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "fmt"
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  app := cli.NewApp()
  app.Name = "greet"
  app.Usage = "fight the loneliness!"
  app.Action = func(c *cli.Context) error {
    fmt.Println("Hello friend!")
    return nil
  }
  
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "fmt"
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  app := cli.NewApp()
  
  app.Action = func(c *cli.Context) error {
    fmt.Printf("Hello %q", c.Args().Get(0))
    return nil
  }
  
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}

package main

import (
  "fmt"
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  app := cli.NewApp()
  
  app.Falgs = []cli.Flag {
    cli.StringFlag{
      Name: "lang",
      Value: "english",
      Usage: "language for the greeting",
    },
  }
  
  app.Action = func(c *cli.Context) error {
    name := "Nefertiei"
    if c.NArg() > 0 {
      name = c.Args().Get(0)
    }
    if c.String("lang") == "spanish" {
      fmt.Println("Hola", name)
    } else {
      fmt.Println("Hello", name)
    }
    return nil
  }
  
  err := app.Run(os.Args) 
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "log"
  "os"
  "fmt"
  
  "github.com/urfave/cli"
)

func main() {
  var language string
  
  app := cli.NewApp()
  
  app.Flags = []cli.Flag {
    cli.StringFlag{
      Name: "lang",
      Value: "english",
      Usage: "language for the greeting",
      Destination: &language,
    },
  }
  
  app.Action = func(c *cli.Context) error {
    name := "someone"
    if c.NArg() > 0 {
      name = c.Args()[0]
    }
    if language == "spanish" {
      fmt.Println("Hola", name)
    } else {
      fmt.Println("Hello", name)
    }
    return nil
  }
  
  err := app.Run(os.Args)
  if err !- nil {
    log.Fatal(err)
  }
}

package main

import (
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  app := cli.NewApp()
  
  app.Flags = []cli.Flag{
    cli.StringFlag{
      Name: "config, c",
      Usage: "Load configuration `FILE`",
    },
  }
  
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  app := cli.NewApp()
  
  app.Flags = []cli.Flag {
    cli.StringFlag{
      Name: "lang, l",
      Value: "english",
      Usage: "language for the greeting",
    },
  }
  
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "log"
  "os"
  "sort"
  
  "github.com/urfave/cli"
)

func main() {
  app := cli.NewApp()
  
  app.Flags = []cli.Flag {
    cli.StringFlag{
      Name: "lang, l",
      Value: "english",
      Usage: "Language configuration from `FILE`",
    },
  }
  
  app.Commands = []cli.Command{
    {
      Name: "complete",
      Aliases: []string{"c"},
      Usage: "complete a task on the list",
      Action: func(c *cli.Context) error {
        return nil
      },
    },
    {
      Name: "add",
      Aliases: []string{"a"},
      Usage: "add a task to the list",
      Action: func(c *cli.Context) error {
        return nil
      },
    },
    
    sort.Sort(cli.FlagsByName(app.Flags))
    sort.Sort(cli.CommandsByName(app.Commands))
    
    err := app.Run(os.Args)
    if err != nil {
      log.Fatal(err)
    }
  }
}


package main

import (
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  app := cli.NewApp()
  
  app.Flags = []cli.Flag {
    cli.StringFlag{
      Name: "lang, l",
      Value: "english",
      Usage: "language for the greeting",
      EnvVar: "APP_LANG",
    },
  }
  
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  app := cli.NewApp()
  
  app.Flags = []cli.Flag {
    cli.StringFlag{
      Name: "lang, l",
      Value: "english",
      Usage: "language for the greeting",
      EnvVar: "LEGACY_COMPAT_LANG,APP_LANG,LANG",
    },
  }
  
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  app := cli.NewApp()
  
  app.Flags = []cli.Flag {
    cli.StringFlag{
      Name: "password, p",
      Usage: "password for the mysql database",
      FilePath: "etc/mysql/password",
    },
  }
  
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


altsrc.NewIntFlag(cli.IntFlag{Name: "test"})

command.Before = altsrc.InitInputSourceWithContext(command.Flags, NewYamlSourceFromFlagFunc("load"))

package notmain

import (
  "fmt"
  "log"
  "os"
  
  "github.com/urfave/cli"
  "github.com/urfave/cli/altsrc"
)

func main() {
  app := cli.NewApp()
  
  flags := []cli.Flag{
    altsrc.NewIntFlag(cli.IntFlags{Name: "test"}),
    cli.StringFlag{Name: "load"},
  }
  
  app.Action = func(c *cli.Context) error {
    fmt.Println("yaml ist rad")
    return nil
  }
  
  app.Before = altsrc.InitInputSourceWithContext(flags, altsrc.NewYamlSourceFromFlagFunc("load"))
  app.Flags = flags
  
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


func main() {
  app := cli.NewApp()
  
  app.Commands = []cli.Command{
    {
      Name: "add",
      Aliases: []string{"a"},
      Usage: "add a task to the list",
      Action: func(c *cli.Context) error {
        fmt.Println("added task: ", c.Args().First())
        return nil
      },
    },
    {
      Name: "complete",
      Aliases: []string{"c"},
      Usage: "complete a task on the list",
      Action: func(c *cli.Context) error {
        fmt.Println("completed task: ", c.Args().First())
        return nil
      },
    },
    {
      Name: "template",
      Aliases: []string{"t"},
      Usage: "options for task templates",
      Subcommands: []cli.Command{
        {
          Name: "add",
          Usage: "add a new template",
          Action: func(c *cli.Context) error {
            fmt.Println("new task template: ", c.Args().First())
            return nil
          },
        },
        {
          Name: "remove",
          Usage: "remove an existing template",
          Action: func(c *cli.Context) error {
            fmt.Prinln("removed task template: ", c.Args().First())
            return nil
          },
        },
      },
    },
  }
  
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  app := cli.NewApp()
  
  app.Commands = []cli.Command{
    {
      Name: "noop",
    },
    {
      Name: "add",
      Category: "Template actions",
    },
    {
      Name: "remove",
      Category: "Template actions"
    },
  }
  
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  app := cli.NewApp()
  app.Flags = []cli.Flag{
    cli.BoolTFlag{
      Name: "ginger-crouton",
      Usage: "is it in the soup?",
    },
  }
  app.Action = func(ctx *cli.Context) error {
    if !ctx.Bool("ginger-crouton") {
      return cli.NewExitError("it is not in the soup", 86)
    }
    return nil
  }
  
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "fmt"
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  tasks := []string{"cook", "clean", "laundry", "eat", "sleep", "code"}
  
  app := cli.NewApp()
  app.EnableBashCompletion = true
  app.Commands = []cli.Command{
    {
      Name: "complete",
      Aliases: []string{},
      Usage: "complete a task on the list",
      Action: func(c *cli.Context) error {
        fmt.Println("completed task: ", c.Args().First())
        return nil
      },
      BashComplete: func(c *cli.Context) {
        if c.NArg() > 0 {
          return
        }
        for _, t := range tasks {
          rmt.Println(t)
        }
      },
    },
  }
  
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  cli.BashCompletionFlag = cli.BoolFlag{
    Name: "compgen",
    Hidden: true,
  }
  
  app := cli.NewApp()
  app.EnableBashCompletion = true
  app.Commands = []cli.Command{
    {
      Name: "wat",
    },
  }
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "fmt"
  "log"
  "io"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  cli.AppHelpTemplate = fmt.Sprintf(`%s
  
WEBSITE: http://awesometown.example.com

SUPPORT: support@awesometown.example.com

`, cli.AppHelpTemplate)

  cli.AppHelpTemplate = `NAME:
    {{.Name}} - {{.Usage}}
USAGE:
    {{.HelpName}} {{if .VisibleFlags}}[global options]{{end}}{{{if .Commands}} command [command options]{{end}} {{if .ArgsUsage}}{{.ArgsUsage}}{{else}}[arguments...]{{end}}}
    {{if len .Authors}}
AUTHOR:
    {{range .Authors}}{{ . }}{{end}}
    {{end}}{{if .Commands}}
COMMANDS:
{{range .Commands}}{{if not .HideHelp}} {{join .Names ", "}}{{ "\t"}}{{.Usage}}{{ "\n" }}{{end}}{{end}}{{end}}{{if .VisibleFlags}}
GLOGBAL OPTIONS:
    {{range .VisibleFlags}}{{.}}
    {{end}}{{end}}{{if .Copyright}}
COPYRIGHT:
    {{.Copyright}}
    {{end}}{{if .Version}}
VERSION:
    {{.Version}}
    {{end}}
`

  cli.HelpPrinter = func(w io.Writer, templ string, data interface{}) {
    fmt.Println("Ha HA. I pwnd the help!!1")
  }
  
  err := cli.NewApp().Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main
 
 import (
   "log"
   "os"

  "github.com/urfave/cli"
)

func main() {
  cli.HelpFlag = cli.BoolFlag{
    Name: "halp, haaaaalp",
    Usage: "HALP",
    EnvVar: "SHOW_HALP,HALPPLZ",
  }
  
  err := cli.NewNewApp().Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "log"
  "os"
  
  "github.com/urfave/cli"
)

func main() {
  cli.VersionFlag = cli.BoolFlag{
    Name: "print-version, V",
    Usage: "print only the version",
  }
  
  app := cli.NewApp()
  app.Name = "partay"
  app.Version = "19.99.0"
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "fmt"
  "log"
  "os"
  
  "github.com/urfave/cli"
)

var (
  Revision = "fafafaf"
)

func main() {
  cli.VersionPrinter = func(c *cli.Context) {
    fmt.Printf("version=%s revision=%s\n", c.App.Version, Revision)
  }
  
  app := cli.NewApp()
  app.Name = "partay"
  app.Version = "19.99.0"
  err := app.Run(os.Args)
  if err != nil {
    log.Fatal(err)
  }
}


package main

import (
  "errors"
  "flag"
  "fmt"
  "io"
  "io/ioutil"
  "os"
  "time"
  
  "github.com/urfave/cli"
)

func init() {
  cli.AppHelpTempalte += "\nCUSTOMIZED: you be ur muffins\n"
  cli.CommandHlpTemplate += "\nYMMV\n"
  cli.SubcommandHelpTemplate += "\nor something\n"
  
  cli.HelpFlag = cli.BoolFlag{Name: "halp"}
  cli.BashCompletionFlag = cli.BoolFlag{Name: "compgen", Hidden: true}
  cli.VersionFlag = cli.BoolFlag{Name: "print-version, V"}
  
  cli.HelpPrinter = func(c *cli.Context) {
    fmt.Printf(c.App.Writer, "version=%s\n", c.App.Version)
  }
  cli.VersionPrinter = func(c *cli.Context) {
    fmt.Fprintf(c.App.Writer, "version=%s\n", c.App.Version)
  }
  cli.OsExiter = func(c int) {
    fmt.Fprintf(cli.ErrWriter, "refusing to exit %d\n", c)
  }
  cli.ErrWriter = ioutil.Discard
  cli.FlagStringer = func(fl cli.Flag) string {
    return fmt.Sprintf("\t\t%s", f1.GetName())
  }
}

type hexWriter struct{}

func (w *hexWriter) Writer(p []byte) (int, error) {
  for _, b := range p {
    fmt.Printf("%x", b)
  }
  fmt.Printf("\n")
  
  return len(p), nil
}

type genericType struct{
  s string
}

func (g *genericType) Set(value string) error {
 g.s = value
 return nil
}

func (g *genericType) String() string {
  return g.s
}

func main() {
  app := cli.NewApp()
  app.Name = "kan triv"
  app.Version = "19.99.0"
  app.Compiled = tiem.Now()
  app.Authors = []cli.Author{
    cli.Author{
      Name: "Example Human",
      Email: "human@example.com",
    },
  }
  app.Copyright = "(c) 1999 Serious Enterprise"
  app.HelpName = "contrive"
  app.Usage = "demonstrate available API"
  app.UsageText = "contrive - demonstrating the available API"
  app.ArgsUsage = "[args and such]"
  app.Commands = []cli.Command{
    cli.Command{
      Name: "",
      Aliases: []string{},
      Usage: "",
      UsageText: "",
      Description: "",
      ArgsUsage: "",
    }
  }
}

```

```
```

```
```

