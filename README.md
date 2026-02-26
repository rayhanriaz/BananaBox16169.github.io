# Banana Box web site

## Website layout
This website is built using [Mkdocs](https://www.mkdocs.org/user-guide/writing-your-docs/) utilizing the [Mkdocs Gradle Plugin](https://xvik.github.io/gradle-mkdocs-plugin/latest/).

Below is a layout of this repo and how it affects the website:

| File / Directory                                                           | Description                                                                                                       |
|----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| [`src/doc/mkdocs.yml`](src/doc/mkdocs.yml)                                 | Main mkdocs config file. Add/modify the `nav` element to add additional pages                                     |
| [`src/doc/docs`](src/doc/docs)                                             | Markdown files for the website content                                                                            |
| [`src/doc/docs/index.md`](src/doc/docs/index.md)                           | Main page for the website. Can be modified to add content.                                                        |
| [`src/doc/docs/stylesheets/extra.css`](src/doc/docs/stylesheets/extra.css) | Custom CSS for the website. Can be modified to change the look and feel. Currently contains a "Banana box" theme. |
| [`src/doc/docs/assets/img`](src/doc/docs/assets/img)                       | Images for the website. Any images that you want to reference should be here.                                     |

## Viewing the site locally
If you'd like to render the site locally, just run `gradlew mkdocsServe`. You'll see something like this:

```bash
> Task :mkdocsServe
[python] /Users/edeandre/workspaces/IntelliJ/BananaBox16169.github.io/.gradle/python/bin/python -m mkdocs serve -s --dev-addr 127.0.0.1:3000
         INFO    -  Building documentation...
         INFO    -  Cleaning site directory
         INFO    -  Documentation built in 0.12 seconds
         INFO    -  [15:25:33] Serving on http://127.0.0.1:3000/BananaBox16169/
```

You can open your browser to http://127.0.0.1:3000/BananaBox16169/ to view the site.

## Publishing the site
The site will auto-publish to GitHub Pages when a commit is pushed to the `main` branch, either via a pull request (recommended) or direct push (not recommended).

The [`.github/workflows/docs.yml`](.github/workflows/docs.yml) workflow file is responsible for publishing the site.