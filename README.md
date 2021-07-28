# Automated Reporting with `Blogdown`

This is the more applied and technical documentation of the portfolio I created for the Advanced Data Analysis with R Class. Check out the [website](https://kind-wescoff-aaca29.netlify.app/about/) for a  short introduction to the portfolio. The basic idea of the project is to create an online reporting infrastructure that automatically goes through the steps of gathering the data, generating a (standardized) report, and publish the report online. Additionally, I found it desirable to find a solution that automatically initiates each iteration of the reporting cycle without having to source the R Script manually. As the class is focused on `R`, the entire project is meant to be controlled from within the `R` ecosystem. This ReadMe document goes over the core ideas of the project and also introduces the basic `R` commands and steps to reproduce a similar project. 

## Creating Websites with `blogdown`

The central infrastructure for this project is provided by the [`blogdown` package](https://bookdown.org/yihui/blogdown/). The package provides an interface between `R`/`RStudio` and the static website generator `hugo`. Static websites as opposed to dynamic websites, consist of a collection of files (markdown, HTML, CSS, etc.) that are then processed to create a website. The website is static in the sense that it looks the same for every user and does not allow interaction that goes beyond accessing different parts of the website. Dynamic websites, on the other hand, require server-side scripts (like PHP) that allow for a dynamic interaction between the user and the website. For a reporting tool, however, a static website is sufficient, as there is no need for dynamic interaction.

In practice, the `blogdown` package requires a special folder structure that will convey where a certain file will be featured on the website. However, the package comes with the infrastructure to create this folder structure in the workflow of setting up a new blog. The basic workflow follows the following steps:

- Create a new Project within `RStudio` (THis is optional but makes things much easier)
- Pick a `hugo` theme for your website from https://themes.gohugo.io/ . Go to the download page of the respective theme and save the GitHub URL.
- Use `blogdown::new_site(theme = GITHUB_URL, sample = T, to_yaml = T, empty_dirs = T)` to create the folder structure and files necessary for the theme. The arguments in addition to the `theme` argument are not necessary but used for convenience.
- Start writing blog posts. Use `blogdown::new_post()` to create a new document (and the necessary directories) that you can fill with content. Note that by default, `blogdown::new_post()` will open a new Markdown document. You can change this either by specifying the exact file name (including the extension) with the `file` argument or by setting `ext` equal to the desired file extension. Markdown documents are useful for write ups but `blogdown` also supports `.Rmd` files that allow for statistical programming.
- Build the website using `blogdown::build_site()`. Note that you have to set the `build_rmd` equal to `TRUE` if RMarkdown documents are supposed to be processed. Alternatively, it is possible to use `blogdown::serve_site()` to create a local preview of the website. 
- Host your website on a platform like https://netlify.com to make it publicly accessible. This will require a remote git repository (like GitHub) for the project. Further, git has to be installed on the computer.

When all these steps are completed, the blog is a fully live website. When creating new posts, use the `blogdown::new_post()` command, fill the document with content and then commit and push it to the remote repository. This will then be communicated to netlify and in turn lead to changes on the website. There are a few things to keep in mind when creating a new website with `blogdown`. When picking a `hugo` theme it is often advisable to pick a simpler theme rather than a complicated one. The more complicated the resulting website is, the more complicated the files are that organize the webiste. Little tweaks to the website can often return in unexpected changes. For experienced users that are familiar with web development and the `yaml` and `toml` markdown language, this might not be a substantial problem. For new users, however, choosing a complicated, fancy theme can result in substantial frustrations. 
 