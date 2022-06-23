# lens

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

