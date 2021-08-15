# Using %Plug.Upload in integration tests

In testing a image resizer endpoint, I wanted to ensure the response was indeed a resized image. 
To this end, to test an endpoint that takes an upload through `%Plug.Upload`. 

To test this, we create the a `%Plug.Upload` and pass it in with the params for the resize, like this:

```
test "it returns a resized image" do
  file_path = "test/fixtures/images/jeshoots-com-5EKw8Z7CgE4-unsplash.jpg"

  params = %{
    "image" => %Plug.Upload{path: file_path, filename: "test.png"},
    "height" => 100,
    "width" => 200
  }

  conn = conn(:post, "/api/images/resize", params)
  conn = Server.Endpoint.call(conn, @opts)

  assert conn.status == 200
  assert Info.summary(conn.resp_body) == %Images.Info{
    byte_size: 5071,
    errors: nil,
    height: 100,
    mimetype: "image/jpeg",
    width: 200
  }
end
```

Plug.Upload docs can be found here: https://hexdocs.pm/plug/Plug.Upload.html