# PETAL starter

> An alternative `assets` dir for PETAL stack.

## What is PETAL?

PETAL is a stack for building a web application with a responsive and reactive user experience.

- [Phoenix](https://www.phoenixframework.org/)
- [Elixir](https://elixir-lang.org/)
- [TailwindCSS](https://tailwindcss.com/)
- [Alpine.js](https://github.com/alpinejs/alpine)
- [LiveView](https://hexdocs.pm/phoenix_live_view)

> [Google it for more](https://www.google.com/search?q=petal+stack).

## How it works?

This project **generates** [a solid foundation](https://github.com/c4710n/phx-webpack-example/tree/master/apps/hello_web/assets) for working with TailwindCSS and Alpine.js.

> It works by generating code into the user's application instead of using a library, the user has complete freedom to modify the code so it works best with their app.
> -- the same idea from [phx_gen_auth](https://github.com/aaronrenner/phx_gen_auth)

## Preface

Initial commit of this project is generated by following command:

```sh
$ mix phx.new phx-webpack-example --app hello --umbrella --live --no-ecto
```

And I recommend you to create your project with:

```sh
$ mix phx.new demo --umbrella --live
```

## Features

- TailwindCSS with [JIT mode](https://tailwindcss.com/docs/just-in-time-mode) and useful plugins:
  - `@tailwindcss/forms`
  - `@tailwindcss/typography`
  - `@tailwindcss/aspect-ratio`
- Alpine.js with necessary patch
- Compatible with Phoenix LiveView
- theme-sensitive progress bar for LiveView
- set [Inter var](https://rsms.me/inter/) as default font
- Webpack 5 + modular configuration, it supports:
  - [all the good things](https://webpack.js.org/blog/2020-10-10-webpack-5-release/) provided by Webpack 5
  - JS:
    - sourcemap
    - uglify
  - CSS:
    - sourcemap
    - minify
    - autoprefixer
    - nested rules
  - fonts: `eot` / `woff` / `woff2` / `ttf`
  - images: `png` / `jpe?g` / `gif` / `svg`

## Usage

### For umbrella projects

1. Replace your `apps/<app>_web/assets` with `apps/hello_web/assets`:

```sh
$ rm -rf <app>_web/assets
$ svn export \
  https://github.com/c4710n/phx-webpack-example/trunk/apps/hello_web/assets \
  apps/<app>_web/assets
```

> SVN provides `export` function which is useful for copying a sub-directory from a repo.

2. Adjust `config/dev.exs` to setup `watchers`:

```elixir
config :hello, HelloWeb.Endpoint,
  # ...
  watchers: [
    npm: [
      "run",
      "watch",
      cd: # ...
    ]
  ]
```

3. Change option of `Plug.Static`:

```diff
plug Plug.Static,
  # ...
- only: ~w(css fonts images js favicon.ico robots.txt)
+ only: ~w(bundle favicon.ico robots.txt)
```

4. Modify layout file:

```diff
- <link phx-track-static rel="stylesheet" href="<%= Routes.static_path(@conn, "/css/app.css") %>"/>
- <script defer phx-track-static type="text/javascript" src="<%= Routes.static_path(@conn, "/js/app.js") %>"></script
+ <link phx-track-static rel="stylesheet" href="<%= Routes.static_path(@conn, "/bundle/app.css") %>"/>
+ <script defer phx-track-static type="text/javascript" src="<%= Routes.static_path(@conn, "/bundle/app.js") %>"></script>
>
```

### For non-umbrella projects

1. Replace your `assets` with `apps/hello_web/assets`:

```sh
$ rm -rf assets
$ svn export \
  https://github.com/c4710n/phx-webpack-example/trunk/apps/hello_web/assets \
  assets
```

2. Adjust `assets/package.json` in order to fix the path:

```json
// ...

"dependencies": {
  "phoenix": "file:../deps/phoenix",
  "phoenix_html": "file:../deps/phoenix_html",
  "phoenix_live_view": "file:../deps/phoenix_live_view",

// ...
```

3. Adjust `config/dev.exs` to setup `watchers`:

```elixir
config :hello, HelloWeb.Endpoint,
  # ...
  watchers: [
    npm: [
      "run",
      "watch",
      cd: # ...
    ]
  ]
```

4. Change option of `Plug.Static`:

```diff
plug Plug.Static,
  # ...
- only: ~w(css fonts images js favicon.ico robots.txt)
+ only: ~w(bundle favicon.ico robots.txt)
```

5. Modify layout file:

```diff
- <link phx-track-static rel="stylesheet" href="<%= Routes.static_path(@conn, "/css/app.css") %>"/>
- <script defer phx-track-static type="text/javascript" src="<%= Routes.static_path(@conn, "/js/app.js") %>"></script
+ <link phx-track-static rel="stylesheet" href="<%= Routes.static_path(@conn, "/bundle/app.css") %>"/>
+ <script defer phx-track-static type="text/javascript" src="<%= Routes.static_path(@conn, "/bundle/app.js") %>"></script>
```

## Notes

### Working with Alpine.js v3

- [Shadowed assigns with AlpineJS v3 and Phoenix LiveView 0.15](https://elixirforum.com/t/shadowed-assigns-with-alpinejs-v3-and-phoenix-liveview-0-15/40803)

## Read More

- [Optimizing User Experience with LiveView](https://dockyard.com/blog/2020/12/21/optimizing-user-experience-with-liveview)
- [How to combine Phoenix LiveView with Alpine.js](https://fullstackphoenix.com/tutorials/combine-phoenix-liveview-with-alpine-js)

## License

MIT
