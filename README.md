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
