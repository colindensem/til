# Squelch Logging Messages in ExUnit

Exploring `cowboy_plug` outside of a phoenix application, I came upon a lot of noise in my test output. 

It's good to log messages in development and production. So you add the logger to your module:

```
defModule HealthApp.Router do
  require Logger
  <snip>
  plug(Plug.Logger)

  match _ do
    Logger.debug("Missing url invoked #{inspect(conn)}")
    send_resp(conn, 404, "oops... not found, check request")
  end
end
```

When running tests though, we now get multiple log messages per test, conflating the output.

```
test "404 handles missing routes" do
  conn = conn(:get, "/missing")
  |> Router.call(Router.init([]))

  assert conn.state == :sent
  assert conn.status == 404
end
```

We don't need need to see log noise in test output.

To squelch this log entry and others like it for the requests etc. Add the following to `test/test_helper.exs`:

```
ExUnit.start(capture_log: true)
```

But hang on, I do want to see the log out put for a partiucular test. We can add a tag like so:

```
@tag capture_log: true
test "404 handler logs inspected conn" ...
```

ExUnit configuration docs can be found here: https://hexdocs.pm/ex_unit/ExUnit.html#configure/1
