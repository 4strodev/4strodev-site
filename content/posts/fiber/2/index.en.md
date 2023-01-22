---
title: "Fiber basic routing"
date: 2023-01-22T18:01:16+01:00
draft: false
tags: [fiber, go]
weight: 2
---

## Introduction
In this post we're gonna se how to make basic routing tasks with [fiber](https://gofiber.io).
Fiber has an easy to user router similar to [Express](https://expressjs.com)

## Previous requirements
This post is the seccond part of [fiber tutorial](/tags/fiber). Go to [fiber quickstart](/posts/fiber/1)
to create a simple fiber project.

## HTTP verbs
Fiber router has a method for each http verb. If you want to make
a route using GET verb you have to use `Get` method. The same for `Post` `Put` `Delete`.

I reccomend to see [fiber package docs](https://pkg.go.dev/github.com/gofiber/fiber/v2#Delete)
for a full list of available methods.

{{< code language="go" title="Example: HTTP verbs" expand="Show" collapse="Hide" isCollapsed="true" >}}
package main

import (
	"log"
	"github.com/gofiber/fiber/v2"
)

func main() {
	// Create a new fiber instance
	app := fiber.New()

	app.Get("/my-route", func (c *fiber.Ctx) error {
		return c.SendString("Method: GET Path: '/my-route'");
	})

	app.Post("/my-route", func (c *fiber.Ctx) error {
		return c.SendString("Method: POST Path: '/my-route'");
	})

	app.Put("/my-route", func (c *fiber.Ctx) error {
		return c.SendString("Method: PUT Path: '/my-route'");
	})

	app.Delete("/my-route", func (c *fiber.Ctx) error {
		return c.SendString("Method: DELETE Path: '/my-route'");
	})

	// Start server at port 3000 and log returned error if server fails
	log.Fatal(app.Listen(":3000"))
}
{{< /code >}}

## Paths
There are moment that our application needs to recieve parameters from the client.
We could achieve that using `route params`, query params and `body params`.

- ### Route params
Normally this params are used to send a tiny amount of date being this data simple.
For example an ID associated with a requested resource. Normally the data pased here
is data that will be used to differenciate a resource. A unique username, an ID, etc.

1. If route is called without param fiber will return a 404 error.

{{< code language="go" title="Example: Route can be called without query params" expand="Show" collapse="Hide" isCollapsed="true" >}}
package main

import (
	"fmt"
	"log"

	"github.com/gofiber/fiber/v2"
)

func main() {
	// Create a new fiber instance
	app := fiber.New()

	// Here we are getting user ID from route and saving in a variable named `id`
	app.Get("/user/:id", func (c *fiber.Ctx) error {
		// Getting route params.
		// Notice that we have to pass the same name that we specified in route
		id := c.Params("id")

		// Doing needed operations to get user
		
		// Sending response
		return c.SendString(fmt.Sprintf("User with id %s", id))
	})

	// Start server at port 3000 and log returned error if server fails
	log.Fatal(app.Listen(":3000"))
}
{{< /code >}}

- ### Query params
If we have to pass multiple params to a route we can use query params. We can use query params
to do the same as we use route params. But with two differences.

1. The route can be called if there are no query params. So we have to make a manual check.

{{< code language="go" title="Example: Route params" expand="Show" collapse="Hide" isCollapsed="true" >}}
package main

import (
	"fmt"
	"log"

	"github.com/gofiber/fiber/v2"
)

func main() {
	// Create a new fiber instance
	app := fiber.New()

	// As you can se we are not defining any query param in route
	// This is why this route could be called if there is no query
	// params in the request
	app.Get("/user", func (c *fiber.Ctx) error {
		// Getting query params.
		// If no param is passed fiber automatically
		// returns an empty string.
		id := c.Query("id")

		if id == "" {
			return c.SendString("No id is passed!")
		}
		
		// Sending response
		return c.SendString(fmt.Sprintf("User with id %s", id))
	})

	// Start server at port 3000 and log returned error if server fails
	log.Fatal(app.Listen(":3000"))
}
{{< /code >}}

2. We can send multiple params in the same route.

{{< code language="go" title="Example: Route params" expand="Show" collapse="Hide" isCollapsed="true" >}}
package main

import (
	"fmt"
	"log"

	"github.com/gofiber/fiber/v2"
)

func main() {
	// Create a new fiber instance
	app := fiber.New()

	// As you can se we are not defining any query param in route
	// This is why this route could be called if there is no query
	// params in the request
	app.Get("/user", func (c *fiber.Ctx) error {
		// Getting query params.
		// If no param is passed fiber automatically
		// returns an empty string.
		id := c.Query("id")
		name := c.Query("name")
		email := c.Query("email")
		phone := c.Query("phone")

		if id == "" {
			return c.SendString("No id is passed!")
		}

		// Checking all params ...
		
		// Sending response
		return c.SendString(fmt.Sprintf("Returning user with data: id -> %s, name -> %s, email -> %s, phone -> %s", id, name, email, phone))
	})

	// Start server at port 3000 and log returned error if server fails
	log.Fatal(app.Listen(":3000"))
}
{{< /code >}}

- ### Body params
Body params can be a complex structure of data that the client are sending to us.
It can be un json, xml, html forms encoding, etc. This are a little bit complex and require their own post.
I will upload a new article talking about body params in a future. For the moment remind this.

1. The route can be executed wihtou body params.
2. The params needs to be parsed to start working with it.

## Resume
In this case we have seen basic routing but fiber gives us more useful tools to make routes.

- Wildcards
- Constraints
- Groups
- Middlewares

> I reccommend you to visit [fiber docs](https://gofiber.io) to se more details about the frameowrk
