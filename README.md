# Web Dev

## Getting Started: Basic Web App

This creates a basic web application using [net/http](https://pkg.go.dev/net/http?utm_source=gopls)

## 1.10.2 - initialize go module

initialize go module

## 2.1 Dynamic reloading

Add dynamic reloading with [modd](https://github.com/cortesi/modd).

When we run `modd`, this will tell it to do two things:

- Watch for changes to any `.go` files, including test files, and to run tests for any changed directories.
- To watch for changes to any non-test `.go` file and to build and restart our app if a change is detected.

The `modd` command runs the lenslocked app. I've added `make run` to execute `modd`.

## 2.2 Setting header values

Set the header type in http response using `w.Header().Set("Content-Type", "text/html; charset=utf-8")`.

## 2.3 Create a contact page

Create a new handler func for handling requests to `"/contact"`.

## 2.4

Add a pathHandler function that can detect requests to different paths.

## 2.5

Use switch statement to handle traffic to different paths in `pathHandler` function.

## 2.7

Update `pathHandler` to deal with pages not found.

## 2.8

Create router type with a ServeHTTP method.

## 2.9

Convert pathHandler to the http.HandlerFunc type, which implements the Handler interface. This gives it the ServeHTTP method, which implements the Handler interface.

## 2.10

Switch back to using router in http.ListenAndServe and the ServeHTTP method.

## 2.11

Add faq handler.

## 3.3

Install Chi to handle routing.

- [https://go-chi.io](https://go-chi.io/)
- [https://github.com/go-chi/chi](https://github.com/go-chi/chi)
