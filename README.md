## Repo for ELAG 2018 workshop on R Shiny - Interactive Data Applications

Website: <https://ucla-data-archive.github.io/elag2018-shiny/>
Instructors: Harrison Dekker and Tim Dennis  
[Setup info](setup-r.md)

## Adding content to this repo

* Add a file to the `pages/` folder - using `.md` extension
* You can link to it off the `index.md` file like so:
  - `[Text](pages/file.html)` use `.html` extension to the above `md` file

If you want to use **rmarkdown** documents in the github flavor of markdown (for say jekyll), use the additional yaml output option `md_document` and `variant`. You can also used a `header.md` file to set up the yaml header, so you can specify things like `layout`. 

```
---
title: "Elag DataViz Basics"
author: "Tim Dennis"
date: "`r format(Sys.time(), '%d %B, %Y')`"
  output:
    md_document:
      variant: markdown_github
      includes:
        in_header: header.md
---
```
