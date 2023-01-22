---
title: "Advanced routing"
date: 2023-01-22T22:24:06+01:00
draft: true
---
1. You can use wildcards
2. You can add constraints

> Constraints are simple type validations for your params. If the type don't match
> Fiber will return a 404 error. **Attention** constraints only check type but not convert it.
> If you get the param you will recieve a string.

> See [constraints page](https://docs.gofiber.io/guide/routing#constraints) for more information

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
	app.Get("/user/:id<int>", func (c *fiber.Ctx) error {
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
