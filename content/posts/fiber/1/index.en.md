---
title: "Fiber quickstart"
date: 2023-01-22T13:49:16+01:00
draft: false
tags: [fiber, go]
weight: 1
---

## Introduction
[Fiber](https://gofiber.io) is an [Express](https://expressjs.com) inspired web framework for go.
This framework is **fast**, **easy** to use and as I like **minimalist**.
In this post we're gona see how to create a web server with fiber.

## Create a project
First we have to create a project with go. If you make this many times I reccomend you to make a template.
To do it from scratch it's easy enough to have installed go and our favourite IDE or code editor.

### Create a go module
First of of create a directory where you want to save your project.

```sh
mkdir fiber-project-example
```

Then create a module following this convention. `<hosting>/<name>`.
In my case I'm going to host my package on GitHub.

```sh
go mod init github.com/4strodev/fiber-project-example
```

### Create config files
In my case I only need an **`.editorconfig`**.
```.editorconfig
# .editorconfig
root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true

# As go styles sais
[*.go]
indent_size = 8
indent_style = tab
```

### Create a `main.go` file
Then we have to create our main file. Thats easy just add this lines to your `main.go`.

```go
package main

import (
	"log"
	"github.com/gofiber/fiber/v2"
)

func main() {
	// Create a new fiber instance
	app := fiber.New()

	// Add a route with a controller to this server
	app.Get("/", func(c *fiber.Ctx) error {
		// Returning a simple string here we can also put raw html
		return c.SendString("Hello, World!")
	})

	// Start server at port 3000 and log returned error if server fails
	log.Fatal(app.Listen(":3000"))
}
```

## Launch server
We have or basic server created but we need to install fiber and launch that server.

### Install dependencies
Some tutorials show you that you need to install each dependency manually but go can
install all your dependencies automatically. Thanks to this command.

```sh
go mod tidy
```

### Launch server
Now you can run your server :P.

```sh
go run .
```

Then you can visit your [localhost:3000](http://localhost:3000) to see your server response.

