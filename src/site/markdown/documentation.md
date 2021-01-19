# Project site documentation

Any project that should to publish documentation, should to use the Maven site plugin.

The site will be published with github pages, so as site is for project, the site is published at branch `gh-pages`.

## Creating initial `gh-pages`

You should to create the branch with git.

The content of the new branch should to be only a empty file named `.nojekill`. No other contents should to be present in branch.

Commit it and push to repository

## Site content

At branches develop and main of project, but no gh-pages, should to add the site structure and content.

The site folder structure is:

```bash
+- src/
|   +- site/
|       +- markdown/
|       |  +- index.md
|       |  +- others_pages.md
|       +- site.xml
|       +- resources/
|                +- css/
|                |  +- site.css
|                |
|                +- images/
|                |  +- image.jpg
|                |
|                +- js/
|                |  +- site.js
|
|   +- pom.xml
```

At this point, content should to be added as needed by project.

