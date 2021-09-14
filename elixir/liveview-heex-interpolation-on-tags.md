# Liveview HEEx interpolation on html tags

In creating a new application; I was following the Phoenix 1.6 RC0 path, the release notes talked about the new HEEx Engine. 

Some previous live view examples I had applied were not working.

```
<button class="bg-red-600 text-white"
        phx-click="delete"
        phx-value-id="<%= todo.id %>"
        phx-disable-with="Deleting...">
  Delete
</button>
```

This resulted in an error: 

```
...expected closing `"` for attribute value

This may happen if there is an EEx interpolation inside a tag, which is not supported. Instead of 

    <div <%= @some_attributes %>>
    </div>

do

    <div {@some_attributes}>
    </div>

Where @some_attributes must be a keyword list or a map.
```

What this means is, the following will now work:
```
<button class="bg-red-600 text-white"
        phx-click="delete"
        phx-value-id={todo.id}
        phx-disable-with="Deleting...">
  Delete
</button>
```

Phoenix 1.6 release notes: https://www.phoenixframework.org/blog/phoenix-1.6-released
