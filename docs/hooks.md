---
id: "hooks"
title: "Server Hooks"
sidebar_label: "Server Hooks"
---

The service constructor can use the option `twirp.WithServerHooks(hooks *twirp.ServerHooks)`
to plug in additional functionality:

```go
server := NewHaberdasherServer(svcImpl, twirp.WithServerHooks(hooks))
```

These _hooks_ provide a framework for side-effects at important points while a
request gets handled. You can do things like log requests, record response times
in statsd, authenticate requests, and so on.

The `*twirp.ServerHooks` struct holds a pile of callbacks, each of
which receives the current `context.Context`, and can provide a new
`context.Context` (possibly including a new value through the
[`context.WithValue`](https://godoc.org/golang.org/x/net/context#WithValue)
function).

Check out
[the godoc for `ServerHooks`](http://godoc.org/github.com/twitchtv/twirp#ServerHooks)
for information on the specific callbacks. For an example hooks implementation,
[`github.com/twitchtv/twirp/hooks/statsd`](https://github.com/twitchtv/twirp/blob/master/hooks/statsd/)
is a good tutorial.
