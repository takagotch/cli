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
















```

```
```

```
```

