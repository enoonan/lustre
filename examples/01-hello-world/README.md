![](./header.png)

# 01 Hello World

This hello world example is a tiny example of what you need to put together to
get a Lustre application running. In later examples we'll touch on server-side
rendering and Lustre Universal Components but for these first examples we'll
be looking at rendering on the client _only_.

## Configuring the Gleam project

It's important to remember to add `target = "javascript"` to your `gleam.toml`!
If you forget to do this you might end up confused when it looks like your project
is successfully building but you have no JavaScript output!

## Creating a `lustre.element` application

The simplest kind of Lustre application is the `element`. This sets up a static
application that does not have its own update loop and cannot dynamically render
any content. Instead, we provide a static Lustre `Element` to render once.

### HTML attributes and inline styles

In Lustre, HTML attributes are modelled as a `List` of attributes. This is a bit
different from many other frameworks that use an object or record for attributes.
Lustre takes the list-of-attributes approach for a couple of reasons:

- Gleam doesn't have a way to construct an anonymous record: we'd have to have
  an infinite number of types to cover every possible varation!

- Working with lists makes it convenient to merge different sets of attributes
  together (like an element that defines some local attributes and merges them
  with any passed in as an argument).

In a similar fashion, inline styles are lists of property/value tuples. In this
example we're setting inline styles for the `width` and `height` properties.

### Why `element.text`?

In frameworks like React, it's enough to just return a `String` if you want to
render some text. Gleam's type system works a little differently though, a string
literal isn't compatible with Lustre's `Element` type on its own, so we need to
wrap any text to render in `element.text`.

You won't see us do it in any of the examples we share, but it's common for folks
to import `text` and any html elements they're using unqualified to cut down on
some of the noise:

```gleam
import lustre/element.{text}
import lustre/element/html.{div, p}
...
```

## Seeing the result

Lustre has a companion package containing development tooling called
[lustre_dev_tools](https://hexdocs.pm/lustre_dev_tools/). It's already included
in this and all the other example. You can run `gleam run -m lustre/dev start`
in any of these examples to start a development server and head over to
`localhost:1234` to see what it produces.

### Enabling lustre/ui

[`lustre/ui`](https://hexdocs.pm/lustre_ui/) is a separate package published by us
to provide a collection of robust styled elements for folks that want to get working
with Lustre ASAP. Each of these examples have been written to use elements from
that package. 

To use `lustre/ui` in your own projects, you will need to be sure to load the 
`lustre/ui` stylesheet. In these examples, the stylesheet is already included for 
you in `index.html`:

```html
    <link
      rel="stylesheet"
      href="./build/dev/javascript/lustre_ui/priv/static/lustre-ui.css"
    />
```

It's not necessary to use `lustre/ui` to use Lustre or to check out any of these
examples, but we've built these examples using the package so things look a little
more interesting.

## Getting help

If you're having trouble with Lustre or not sure what the right way to do
something is, the best place to get help is the [Gleam Discord server](https://discord.gg/Fm8Pwmy).
You could also open an issue on the [Lustre GitHub repository](https://github.com/lustre-labs/lustre/issues).
