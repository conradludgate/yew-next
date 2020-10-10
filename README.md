# yew-next
yew.rs but with multi page support and static/server side generation. WIP

## What

```rust
#[page(path = "/about", static_props = get_props)]
pub struct About {
    props: Props,
    link: ComponentLink<Self>,
}

fn get_props() -> Props {
    //...
}
```

will register the component as a page component.

Then, in your main function, call

```rust
fn main() {
    render_pages!() 
} 
```

If you then compile this program to your normal os, and run it,
it will launch a server, listening on the paths for all of your pages.
It will return pre-rendered html to the requester.

If you pass the `--generate` flag, it will statically generate all of the pages for you,
but will error if any of the pages are not static.

Then compile the program to wasm to get the rest of the functionality necessary.

## How

Makes use of https://github.com/dtolnay/inventory to register the structs as pages,
then in the `render_pages` macro, it collects all the registered pages and creates the necessary paths through the application.

It also makes use of rusts `cfg` attribute to only compile certain parts on wasm or not

