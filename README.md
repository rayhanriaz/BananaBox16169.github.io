# BananaBox16169.github.io
Banana Box web site

This website is built using [Mkdocs](https://www.mkdocs.org/user-guide/writing-your-docs/) utilizing the [Mkdocs Gradle Plugin](https://xvik.github.io/gradle-mkdocs-plugin/latest/).

Below is a layout of this repo and how it affects the website:

| File / Directory                                                           | Description                                                                                                       |
|----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| [`src/doc/mkdocs.yml`](src/doc/mkdocs.yml)                                 | Main mkdocs config file. Add/modify the `nav` element to add additional pages                                     |
| [`src/doc/docs`](src/doc/docs)                                             | Markdown files for the website content                                                                            |
| [`src/doc/docs/index.md`](src/doc/docs/index.md)                           | Main page for the website. Can be modified to add content.                                                        |
| [`src/doc/docs/stylesheets/extra.css`](src/doc/docs/stylesheets/extra.css) | Custom CSS for the website. Can be modified to change the look and feel. Currently contains a "Banana box" theme. |
| [`src/doc/docs/assets/img`](src/doc/docs/assets/img)                       | Images for the website. Any images that you want to reference should be here.                                     |