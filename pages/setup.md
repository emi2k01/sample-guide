# Setting up the environment

Assuming you already have installed Rust (`rustc`, `cargo`, etc):

## Creating a Cargo project

First, we need to create a Cargo project by running the following command in the shell:

```shell
$ cargo new actix-hello-world
```

This creates a Cargo project named "actix-hello-world" in a project with the
same name under the current directory.

Lets enter the project by doing:

```shell
$ cd actix-hello-world
```

At this point, if you run the `ls` command, your project's structure should
look like the one you see at the right in the **Explorer**.

## Adding the dependencies

Open [Cargo.toml](<#csai:open_file file="Cargo.toml">) and [add `actix-web` to
the dependencies][actix-web-dependency]

We are using version `4` which is currently on beta but it shouldn't take long for it to be stable.

## Next

That's all for setting up the environment. Next, we will start coding!

[actix-web-dependency]: <#csai:highlight_regex file="Cargo.toml" from="^\\[dependencies\\]$" to="^actix-web.\*$">

