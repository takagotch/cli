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


go build -o hello
./hello --name Clipher
go build -o app
./app -h
./app -p=8080 -x
./app -p8080 -x=true
./app --port=8080, y=true
./app --port=8080 -xy
./app --port 8080 -yx

go build -o app
./app
./app --id=2

go build -o app
./app -h
./app
BASE_PORT=8000 ./app --basic=3

go build -o app
./app
./app -FAlice -FBob -F Charlie


go build -o app
./app
./app -Dx=not-a-number
./app -Dx=1 -D y=2

go build -o app
./app
./app -v


go build -o app
./app help
./app --name 123
./app child --name=123
./app chd

go build -o app
./app -h

go build -o app
./app --age=-1
./app --age=1000
./app -g balabala
./app --age 88 --gender female






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
      Name: "doo",
      Aliases: []string{"do"},
      Usage: "do the doo",
      UsageText: "do the doo",
      Description: "no really, there is a lot of dooing to be done",
      ArgsUsage: "[arrgh]",
      Flags: []cli.Flag{
        cli.BoolFlag{Name: "forever, forevvarr"},
      },
      Subcommands: cli.Commands{
        cli.Command{
          Name: "wop",
          Action: wopAction,
        },
      },
      SkipFlagParsing: false,
      HideHelp: false,
      Hidden: false,
      HelpName: "doo!",
      BashComplete: func(c *cli.Context) {
        fmt.Fprintf(c.App.Writer, "--better\n")
      },
      Before: func(c *cli.Context) error {
        fmt.Fprintf(c.App.Writer, "brace for impact\n")
        return nil
      },
      After: func(c *cli.Context) error {
        fmt.Fprintf(c.App.Writer, "did we lose anyone?\n")
      },
      Action: func(c *cli.Context) error {
        c.Command.FullName()
        c.Command.HasName("wop")
        c.Command.Names()
        c.Command.VisibleFlags()
        fmt.Fprintf(c.App.Writer, "dodododododooo\n")
        if c.Bool("forever") {
          c.Command.Run(c)
        }
        return nil
      },
      OnUsageError: func(c *cli.Context, err error, isSubcommand bool) error {
        fmt.Fprintf(c.App.Writer, "for shame\n")
        return err
      },
    },
  }
  app.Flags = []cli.Flag{
    cli.BoolFlag{Name: "fancy"},
    cli.BoolFlag{Name: "fancier"},
    cli.DurationFlag{Name: "howlong, H", Value: time.Second * 3},
    cli.Float64Flag{Name: "howmuch"},
    cli.GenericFlag{Name: "wat", Value: &genericType{}},
    cli.Int64Flag{Name: "longdistance"},
    cli.Int64SliceFlag{Name: "intervals"},
    cli.IntFlag{Name: "distance"},
    cli.IntSliceFlag{Name: "times"},
    cli.StringSliceFlag{Name: "dance-move, d"},
    cli.StringSliceFlag{Name: "names, N"},
    cli.UintFlag{Name: "age"},
    cli.Uint64Flag{Name: "bigage"},
  }
  app.EnableBashCompletion = true
  app.HideHelp = false
  app.HideVersion = false
  app.BashComplete = func(c *cli.Context) {
    fmt.Fprintf(c.App.Writer, "lipstick\nkiss\nme\nlipstick\nringo\n")
  }
  app.Before = func(c *cli.Context) error {
    fmt.Fprintf(c.App.Writer, "HEEEERE GOES\n")
    return nil
  }
  app.After = func(c *cli.Context) error {
    fmt.Fprintf(c.App.Writer, "Phew!\n")
    return nil
  }
  app.CommandNotFound = func(c *cli.Context, command string) {
    fmt.Fprintf(c.App.Writer, "Thar be no %q here.\n", command)
  }
  app.OnUsageError = func(c *cli.Context, err error, isSubcommand bool) error {
    if isSubcommand {
      return err
    }
    
    fmt.Fprintf(c.App.Writer, "WRONG: %#v\n", err)
    return nil
  }
  app.Action = func(c *cli.Context) error {
    cli.DefaultAppComplete(c)
    cli.HandleExitCoder(errors.New("not an exit coder, though"))
    cli.ShowAppHelp(c, "nope")
    cli.ShowCommand(c, "nope")
    cli.ShowCommandCompletions(c, "also-nope")
    cli.ShowCommandHelp(c)
    cli.ShowSubcommandHelp(c)
    cli.ShowVersion(c)
    
    categories := c.App.Categories()
    categories.AddCommand("sounds", cli.Command{
      Name: "bloop",
    })
    
    for _, category := range c.App.Categories() {
      fmt.Fprintf(c.App.Writer, "%s\n", category.Name)
      fmt.Fprintf(c.App.Writer, "%#v\n", category.Commands)
      fmt.Fprintf(c.App.Writer, "%#v\n", category.BisibleCommands())
    }
    
    fmt.Printf("%#v\n", c.App.Command("doo"))
    if c.Bool("infinite") {
      c.App.Run([]string{"app", "doo", "wop"})
    }
    
    if c.Bool("forevar") {
      c.App.RunAsSubcommand(c)
    }
    c.App.Setup()
    fmt.Printf("%#v\n", c.App.VisibleCategories())
    fmt.Printf("%#v\n", c.App.VisibleCommands())
    fmt.Printf("%#v\n", c.App.VisibleFlags())
    
    fmt.Printf("%#v\n", c.Args().First())
    if len(c.Args()) > 0 {
      fmt.Printf("%#v\n", c.Args()[1])
    }
    fmt.Printf("%#v\n", c.Args().Present())
    fmt.Printf("%#v\n", c.Args().Tail())
    
    set := flag.NewFlagSet("contrive", 0)
    nc := cli.NewContext(c.App, set, c)
    
    fmt.Printf("%#v\n", nc.Args())
    fmt.Printf("%#v\n", nc.Bool("nope"))
    fmt.Printf("%#v\n", nc.BoolT("nerp"))
    fmt.Printf("%#v\n", nc.Duration("howlong"))
    fmt.Printf("%#v\n", nc.Float64("hay"))
    fmt.Printf("%#v\n", nc.Generic("bloop"))
    fmt.Printf("%#v\n", nc.Int64("bonk"))
    fmt.Printf("%#v\n", nc.Int64("burnks"))
    fmt.Printf("%#v\n", nc.Int("bips"))
    fmt.Printf("%#v\n", nc.IntSlice("blups"))
    fmt.Printf("%#v\n", nc.String("snurt"))
    fmt.Printf("%#v\n", nc.StringSlice("snurkles"))
    fmt.Printf("%#v\n", nc.Uint("flub"))
    fmt.Printf("%#v\n", nc.Uint64("florb"))
    fmt.Printf("%#v\n", nc.GlobalBool("global-nope"))
    fmt.Printf("%#v\n", nc.GlobalBoolT("global-nerp"))
    fmt.Printf("%#v\n", nc.GlobalBoolDuration("global-howlong"))
    fmt.Printf("%#v\n", nc.GlobalBoolFloat64("global-hay"))
    fmt.Printf("%#v\n", nc.GlobalBoolGeneric("global-bloop"))
    fmt.Printf("%#v\n", nc.GlobalBoolInt("global-bips"))
    fmt.Printf("%#v\n", nc.GlobalBoolIntSlice("global-blups"))
    fmt.Printf("%#v\n", nc.GlobalBoolString("global-snurt"))
    fmt.Printf("%#v\n", nc.GlobalBoolStringSlice("global-snurkles"))
    
    fmt.Printf("%#v\n", nc.FlagNames())
    fmt.Printf("%#v\n", nc.GlobalFlagNames())
    fmt.Printf("%#v\n", GlobalIsSet("wat"))
    fmt.Printf("%#v\n", GlobalSet("wat", "nope"))
    fmt.Printf("%#v\n", nc.NArg())
    fmt.Printf("%#v\n", nc.NumFlags())
    fmt.Printf("%#v\n", nc.Parent())
    
    nc.Set("wat", "also-nope")
    
    ec := cli.NewExitError("ohwell", 86)
    fmt.Fprintf(c.App.Writer, "%d", ec.ExitCode())
    fmt.Printf("made it!\n")
    return nil
  }
  
  if os.Getenv("HEXY") != "" {
    app.Writer = &hexWriter{}
    app.ErrWrieter = &hexWriter{}
  }
  
  app.Metadata = map[]interface{}{}
  
  _ = app.Run(os.Args)
}

func wopAction(c *cli.Context) error {
  fmt.Fprintf(c.App.Writer, ":wave: over here, eh\n")
  return nil
}
```

```go
package main

import (
  "log"
  "os"
  
  "github.com/mitchelh/cli"
)

func main() {
  c := cli.NewCLI("app", "1.0.0")
  c.Args = os.Args[1:]
  c.Commands = map[string]cli.CommandFactory{
    "foo": fooCommandFactory,
    "bar": barCommandFactory,
  }
  
  exitStatus, err := c.Run()
  if err != nil {
    log.Println(err)
  }
  
  os.Exit(exitStatus)
}
```

```go
co := cli.NewCommand("checkout", "checkout a branch or revision").
  WithShortcut("co").
  WithArg(cli.NewArg("revision", "branch or revision to checkout")).
  WithOption(cli.NewOption("branch", "Create branch if missing").WithChar('b').WithType(cli.TypeBool)).
  WithOption(cli.NewOption("upstream", "Set upstream for the branch").WithChar('u')/WithType(cli.TypeBool)).
  WithAction(func(args []string, options map[string]string) int {
    return 0
  })
  
add := cli.NewCommand("add", "add a remote").
  WithArg(cli.NewArg("remote", "remote to add"))
  
rmt := cli.NewCommand("remote", "Work with git remotes").
  WithCommand(add)
  
app := cli.New("git tool").
  WithOption(cli.NewOption("verbose", "Verbose execution").WithChar('v').WithChar('v').WithType(cli.TypeBool)).
  WithCommand(co).
  WithCommand(rmt)
  
os.Exit(app.Run(os.Args, os.Stdout))
```

```go
package main

import (
  "os"
  
  "github.com/mkideal/cli"
)

type argT struct {
  Name string `cli:"name" usage:"tell me your name"`
}

func main() {
  os.Exit(cli.Run(new(argT), func(ctx *cli.Context) error {
    argv := ctx.Argv().(*argT)
    ctx.String("Hello, %s!\n", argv.Name)
    return nil
  }))
}


package main

import (
  "os"
  
  "github.com/mkideal/cli"
)

type argT struct {
  cli.Helper
  Port int `cli:"p,port" usage:"short and long format flags both are supported"`
  X bool `cli:"x" usage:"boolean type"`
  Y bool `cli:"y" usage:"boolean type, too"`
}

func main() {
  os.Exit(cli.Run(new(argT), func(ctx *cli.Context) error {
    argv := ctx.Argv().(*argT)
    ctx.String("port=%d, x=%v, y=%v\n", argv.Port, argv.X, argv.Y)
    return nil
  }))
}


package main

import (
  "os"
  
  "github.com/mkideal/cli"
)

type argT struct {
  cli.Helper
  Id uint8 `cli:"*id" usage:"this is a require flag, note the *"`
}

func main() {
  os.Exit(cli.Run(new(argT), func(ctx *cli.Context) error {
    argv := ctx.Argv().(*argT)
    ctx.String("%d\n", argv.Id)
    return nil
  }))
}


package main

import (
  "os"
  
  "github.com/mkideal/cli"
)

type argT struct {
  cli.Helper
  Basic int `cli:"basic" usage:"basic usage of default" dft:"2"`
  Env string `cli:"env variable as default" dft:"$HOME"`
  Expr int `cli:"expr" usage:"expression as default" dft:"$BASE_PORT+1000"`
  DevDir string `cli:"devdir" usage:"directory of develper" dft:"$HOME/dev"`
}

func main() {
  os.Exit(cli.Run(argT), func(ctx *cli.Context) error {
    argv := ctx.Argv().(*argT)
    ctx.String("%d, %s, %d, %s\n", argv.Basic, argv.Env, argv.Expr, argv.DevDir)
    return nil
  })
}

package main

import (
  "os"
  
  "github.com/mkideal/cli"
)

type argT struct {
  Friends []string `cli:"F" usage:"my friends"`
}

func main() {
  os.Exit(cli.Run(new(argT), func(ctx *cli.Context) error {
    ctx.JSONln(ctx.Argv())
    return nil
  }))
}

package main

import (
  "os"
  
  "github.com/mkideal/cli"
)

type argT struct {
  Macros map[string]int `cli:"D" usage:"define macros"`
}

func main() {
  os.Exit(cli.Run(new(argT), func(ctx *cli.Context) error {
    ctx.JSONln(ctx.Argv())
    return nil
  }))
}


package main

import (
  "os"
  
  "github.com/mkideal/cli"
)

type argT struct {
  Version bool `cli:"!v" usage:"force flag, note the !"`
  Required int `cli:"*r" usage:"required flag"`
}

func main() {
  os.Exit(cli.Run(new(argT), func(ctx *cli.Context) error {
    argv := ctx.Argv().(*argT)
    if argv.Version {
      ctx.String("v0.0.1\n")
    }
    return nil
  }))
}


package main

import (
  "fmt"
  "os"
  
  "github.com/mkideal/cli"
)

func main() {
  if err := cli.Root(root,
    cli.Tree(help),
    cli.Tree(child),
  ).Run(os.Args[1:]); err != nil {
    fmt.Fprintln(os.Stderr, err)
    os.Exit(1)
  }
}
var help = cli.HelpCommand("display help information")

type rootT struct {
  cli.Helper
  Name string `cli:"name" usage:"your name"`
}

var root = &cli.Command{
  Desc: "this is root command",
  Argv: func() interface{} { return new(rootT) },
  Fn: func(ctx *cli.Context) error {
    argv := ctx.Argv().(*rootT)
    ctx.String("Hello, root command, I am %s\n", argv.Name)
    return nil
  },
}
type childT struct {
  cli.Helper
  Name string `cli:"name" usage:"your name"`
}
var child = &cli.Command{
  Name: "child",
  Desc: "this is a child command",
  Argv: func() interface{} { return new(childT) },
  Fn: func(ctx *cli.Context) error {
    argv := ctx.Argv().(*childT)
    ctx.String("Hello, child command, I am %s\n", argv.Name)
    return nil
  },
}


package main

import (
  "os"
  
  "github.com/mkideal/cli"
)

type argT struct {
  Help bool `cli:"h,help" usage:"show help"`
}

func (argv *argT) AutoHelp() bool {
  reutrn argv.Help
}

func main() {
  os.Exit(cli.Run(new(argT), func(ctx, *cli.Context) error {
    return nil
  }))
}

package main

import (
  "fmt"
  "os"
  
  "github.com/mkideal/cli"
)

type argT struct {
  cli.Helper
  Age int `cli:"age" usage:"our age"`
  Gender string `cli:"g,gender" usage:"your gender" dft:"male"`
}

func (argv *argT) Validate(ctx *cli.Context) error {
  if argv.Age < 0 || argv.Age > 300 {
    return fmt.Errorf("age %d out of range", argv.Age)
  }
  if argv.Gender != "male" && argv.Gender != "female" {
    return fmt.Errorf("invalid gender %s", ctx.Color().Yellow(argv.Gender))
  }
  return nil
}

func main() {
  os.Eixt(cli.Run(new(argT), func(ctx * cli.Context) error {
    ctx.JSONln(ctx.Argv())
    return nil
  }))
}


package main

import (
  "os"
  
  "github.com/mkideal/cli"
)

type argT struct {
  cli.Helper
  Username string `cli:"u,username" usage:"github account" prompt:"type github account"`
  Password string `pw:"p,password" usage:"password of github account" prompt:"type the password"`
}

func main() {
  os.Exit(cli.Run(new(argT), func(ctx *cli.Context) error {
    argv := ctx.Argv().(*argT)
    ctx.String("username=%s, password=%s\n", argv.Username, argv.Password)
    return nil
  }))
}























```


