# Hello, world!

Before we start getting our hands into code, we first have to explain how Actix Web works.

## Actix-Web's model

One of Actix-Web's primitives is the `App`. Quoting [Actix-Web's documentation][actix-docs]:

> All `actix-web` servers are built around the App instance. It is used for
> registering routes for resources and middleware. It also stores application
> state shared across all handlers within the same scope.

Another primitive is `HttpServer`. `HttpServer` is responsible for serving HTTP
requests. It uses the provided `App` and creates an instance for each worker.
That's why in [our code][app-closure] the `App` is inside a closure, so that our `HttpServer`
can call the closure multiple times and create multiple instances.

## Hands on code

Actix-Web is asynchronous, that means that our first is to add an async runtime.
That's what [#\[actix\_web::main\]][actix-web-main] does. It allows using an
`async` main function that automatically sets up a multi-threaded runtime.

[Next][app-closure], we create an `HttpServer` and pass a closure that returns
an `App`. We only add a single service to our `App` which is our index handler.

## Handlers

In Actix-Web there are multiple ways of handling HTTP requests. One of those is
by using the `#[get]`, `#[post]`, `#[put]`, `#[patch]` and `#[delete]` attributes. Each of those
corresponds to their respective HTTP methods.

### Index handler

[We make use of `#[get]`][index-handler] to create a handler for our index
page. We pass a string to the attribute that indicates the route it needs to handle.

[We return `impl Responder`][index-signature] which basically means "This function will return a
type that implements the trait `Responder` and I don't make any other
guarantees"

In this case, we create a `HttpResponse` by using the `Ok`
constructor. This creates a response that will return the HTTP status code "200
Ok".

[We then use][index-res-content-type] the `content_type` method to change the
content type of our response. We pass `ContentType::html()` to return the MIME
type of HTML content.

[We then finish][index-res-body] our response by passing the body.


[actix-docs]: https://actix.rs/docs/application/
[app-closure]: <#csai:highlight_regex file="src/main.rs" from="^(\s){4}HttpServer::new" to="(\s){4}\\}\\)$">
[actix-web-main]: <#csai:highlight_regex file="src/main.rs" from="^#\\[actix_web::main\\]$" to="">
[index-handler]: <#csai:highlight_regex file="src/main.rs" from="^#\\[get\\(~"/~"\\)\\]$" to="^}">
[index-signature]: <#csai:highlight_regex file="src/main.rs" from="^async fn index\\(">
[index-res-content-type]: <#csai:highlight_regex file="src/main.rs" from="^(\s){8}\.content_type" to="">
[index-res-body]: <#csai:highlight_regex file="src/main.rs" from="^(\s){8}\.body" to="">
