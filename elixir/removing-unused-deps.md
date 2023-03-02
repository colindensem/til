# Removing unused deps from Mix.lock

It happens, we add a dependency to our project, and then we remove it. However removing from `mix.exs` is not enough, we also need to remove it from `mix.lock`.

```bash
mix deps.clean --unused
```

This will remove the dependency from `mix.lock` and `deps/`, but keep the library in your lock file.

If we append the `--unlock` flag, it will also remove the dependency from the lock file.

```bash
mix deps.clean --unused --unlock
```

mix deps.unlock docs can be found here: https://hexdocs.pm/mix/Mix.Tasks.Deps.Unlock.html

Discovering unused dependencies:

```bash
mix deps --check-unused
```
