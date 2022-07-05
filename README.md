# lens

<!-- markdownlint-disable MD010 -->

## CH 2 modd

Modd will rebuild the site and local server when changes are made to specified files.

Add modd.conf for [Modd](https://github.com/cortesi/modd)

Commands to run local server with Modd:

- `go build -o lenslocked .`
- `modd`

## CH 2 Creating Contact Page

Add second handler that handles traffic to localhost:3000/contact/

## CH 2 http.Request Type

Examining the [http.Request](https://pkg.go.dev/net/http#Request) type used by the [http.HandleFunc](https://pkg.go.dev/net/http#HandleFunc)

## CH 2 Custom Routing

Create a path handler to handle routing to multiple paths.

## CH 2 URL Path vs RawPath

We've been using [URL Path and not the RawPath](https://pkg.go.dev/net/url#URL). The difference is that the `RawPath` will handle an encoded query path. For example `example.com/page?key=value` is a query path, but the encoded version is `example.com/page%3Fkey%3Dvalue`. `Path` doesn't include unencoded query parameters, but it will handle encoded query parameters and return the full decoded path if it includes encoded query parameters. If you use the encoded path with query parameters, then `RawPath` will return that full encoded path. If you give `Path` an encoded path with query parameters, it will return the decoded path.

The problem is that the forward slash `/` is encoded as `%2F`, so if the path is `example.com/dog%2Fcat%3Fkey%3Dvalue`, `Path` will decode the path as `/dog/cat?key=value` even if the slash should be encoded as `%2F`. However, the `RawPath` value will have the full encoded path `/dog%2Fcat%3Fkey%3Dvalue` which preserves the encoded forward slash.

See https://meyerweb.com/eric/tools/dencoder/ to encode and decode paths (and other things).

## CH 2 Not Found

Handle page not found using status codes.

One method:

```go
	default:
		w.WriteHeader(http.StatusNotFound)
		fmt.Fprint(w, "Page Not Found")
```

This will return a status code of 404.

The `http.ResponseWriter.WriteHeader` takes an integer for a status code. `http.StatusNotFound` returns [`404`](https://pkg.go.dev/net/http#StatusNotFound).

Alternatively, there's:

```go
  http.Error(w, "Page Not Found.", http.StatusNotFound)
```

which handles the same content on one line.

There's also,

```go
  http.Error(w, http.StatusText(http.StatusNotFound), http.StatusNotFound)
```

The [`http.StatusText()`](https://pkg.go.dev/net/http#StatusText) just returns the text associated with a particular status code.

## CH 2 http.Handler Type

The [`http.ListenAndServe`](https://pkg.go.dev/net/http#ListenAndServe) function accepts two parameters, the address and handler. If the handler is set to `nil` (which it often is) then the [`DefaultServeMux`](https://pkg.go.dev/net/http?utm_source=godoc#DefaultServeMux) is used automatically.

So,

```go
http.ListenAndServe(":3000", nil)
```

and

```go
http.ListenAndServe(":3000", http.DefaultServeMux)
```

are equivalent.

`http.ListenAndServe` is a function that accepts the address of type String (`addr`) and a handler of type [Handler](https://pkg.go.dev/net/http#Handler).

The Handler type in an interface with a `ServeHTTP` method that takes a response writer and request:

```go
type Handler interface {
	ServeHTTP(ResponseWriter, *Request)
}
```

This creates a new type called Router which is a struct. The router type gets a ServeHTTP method that handles routing traffic to different pages.

Then the router is passed into the `handler` parameter for `ListenAndServe`.

## Ch 2 http.HandlerFunc Type

You can't just pass a router function to http.ListenAndServe. This example accepts a struct with ServeHTTP method.

In this example, we can replace the Router type with a variable "router" with a type of HandlerFunc and a pathHandler function method.

- [http.Handle](https://pkg.go.dev/net/http#Handle) is a function that takes in a pattern (e.g. "/contact") and an http.Handler.
- [http.Handler](https://pkg.go.dev/net/http#Handler) is a type that is an interface with the [ServeHTTP](https://pkg.go.dev/net/http#HandlerFunc.ServeHTTP) method.
- [http.HandlerFunc](https://pkg.go.dev/net/http#HandlerFunc) is a function type that accepts the same args as the ServeHTTP method and also implements http.Handler
