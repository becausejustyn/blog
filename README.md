# blog

This is where my blog is.

CSS Themes are from `https://github.com/robertmitchellv/robertmitchellv.github.io`

To include the `Font Awesome` options, install using

    quarto install extension quarto-ext/fontawesome

For which icons you can use: `https://github.com/quarto-ext/fontawesome`

To write a new post, first make a new folder in the `/posts` directory, which can be done via command line

    mkdir posts/post_name

Then you will want to make a file called `index.qmd` in that directory, which will be the notebook that you use for writing the post. That can also be created in the command line using

    touch posts/post_name/index.qmd

To do it as a one liner

```
mkdir -p posts/folder_name && touch posts/folder_name/post.qmd
```