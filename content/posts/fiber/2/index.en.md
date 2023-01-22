---
title: "Fiber basic routing"
date: 2023-01-22T18:01:16+01:00
draft: true
tags: [fiber, go]
weight: 2
---

## Introduction
In this post we're gonna se how to make basic routing tasks with [fiber](https://gofiber.io).
Fiber has an easy to user router similar to [Express](https://expressjs.com)

## Previous requirements
This post is the seccond part of [fiber tutorial](/tags/fiber). Go to [fiber-1](/posts/fiber-1)
to create a simple fiber project.

## Simple routes
To make a simple route we need to specify the method and a path.

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

	app.Get("/my-route", func (c *fiber.Ctx) error {
		return c.SendString("Method: GET Path: \"/my-route\"");
	})

	app.Post("/my-route", func (c *fiber.Ctx) error {
		return c.SendString("Method: POST Path: \"/my-route\"");
	})

	app.Put("/my-route", func (c *fiber.Ctx) error {
		return c.SendString("Method: PUT Path: \"/my-route\"");
	})

	app.Delete("/my-route", func (c *fiber.Ctx) error {
		return c.SendString("Method: DELETE Path: \"/my-route\"");
	})

	// Start server at port 3000 and log returned error if server fails
	log.Fatal(app.Listen(":3000"))
}
```

## How to test it
I recommend you to use software like [postman](https://postman.com) or [insomnia](https://insomnia.rest).
There are clients that allows you to customize http requests and more. For the moment is all that we need.
I use postman but if you like to use any other use it 😉.


