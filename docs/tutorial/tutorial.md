# Reference for Site Editors

## Introduction
This site uses [MkDocs](https://www.mkdocs.org/) (a static site generator optimized for project documentation). The fundamental content of the site is stored in **Markdown** text files (a human-readable file format with build-in styling syntax) that can be edited in any text editor. 

Additional styling and functionality comes from the chosen theme [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) and its [plugins](https://squidfunk.github.io/mkdocs-material/plugins/), CSS, and [Python extensions](https://python-markdown.github.io/extensions/). The entire site is hosted directly on [github pages](https://docs.github.com/en/pages) and can be exported to a formatted PDF for offline viewing.

## Site Structure
```
.
├── /docs
│   ├── /QubeCL_Current_Manual
    |   ├── QubeCL_Manual_v5.md
│   │   ├── /assets_QubeCL_Manual_v5
│   │   │   └── /tables
│   |   |   └── imgs.png
│   ├── index.md
│   ├── QubeCL_Manual_v5.md   
│   ├── downloads.md
│   ├── /downloads
│   ├── /img
│   └── /javascripts
├── /ppq_theme
│   ├── /css
│   │   └── /img
|   |   └── ppq.css
│   ├── overrides
│   └── partials
├── mkdocs.yml
├── requirements.txt
└── /site
```

- `/docs` contains all the site content (text and images)
    - `/QubeCL_Current_Manual` contains all files relating to Qube Manual
        - `QubeCL_Manual_v5.md` main markdown document of manual
        - `/assets_QubeCL_Manual_v5` contains all assets for Qube Manual v5
            - `/tables` contains csv files that are converted to tables in markdown
      - `/img` - images referenced in multiple site pages (ex. logo)
    - `/downloads` - files available for download from the site (ex. pdf of manual)
    - `downloads.md` - download list page
- `/ppq_theme` contains custom styling options for the site (color/font/etc)
- `mkdocs.yml` configuration file (set site settings and enable/modify plugins)
- `requirements.txt` list of dependencies to install for development purposes
- `/site` - mkdocs generated site (do not modify directly)
- `.github/ci.yml` (not shown) configuration file for auto-deploying github site

---

## Editing Content

If you just want to edit or add content to the site, you do not need to install the entire development environment, you can simply modify the desired pages in a text editor or directly on the main github site for small changes (navigate to the page of interest and select the edit-pencil button).

!!! note "NOTE:" 
    A basic editor will not give you a complete preview of the final site, but is sufficient to add content and confirm basic formatting. 

![Github direct edit, preview and commit](tutorial_assets/github_direct_edit.png){#gitdirect}

![Github direct preview](tutorial_assets/github_direct_preview.png)


### Create/Edit a page
Each markdown (`.md`) file in the `/docs` directory represents a page on the website. 

If you create a new page (ex. `test.md`) and save it in the `/docs` folder, it will be accessable via the url `site.io/<file_name>.html` but it is *not* automatically added to the site navigation bar. To add it to the site nav, you first need to add it to the navigation structure in the `mkdocs.yml` file for it to be findable by users. Give the button a name and list the file path starting in docs: (`<Button_Name>: <filepath/file_name>`)
```yaml
nav:
  - Home: index.md
  - Qube Manual V5: QubeCL_Current_Manual/QubeCL_Manual_v5.md
  - Downloads: downloads.md
```

### Updating the website

If you are happy with your changes to the documentation and would like to update the site, all you have to do is `commit` and `push` your changes to the main github branch in order to automatically update the live version.

If you have made changes directly to a single page at a time in github, all you have to do is save by selecting `commit changes` in the [Github browser](#gitdirect).

If you are working locally or in a github code environment, you will have to follow a couple more steps to conform to git version control (See [pushing to github](#pushing-to-github))

!!! note "Saving incomplete work"
    (if you are unsure of your changes, or if they are incomplete, please save them in an un-listed `.md` file or push to a new branch while working).  

If you want to see a complete preview of the site before update, or if you would like to edit the styling or make additions to the plugins used in the site, please follow the intructions in the [Comprensive Site Editing](#comprehensive-site-editing) section, otherwise skip to the [Markdown Guide](#guide-to-using-markdown) section to learn more about content editing.    

## Comprehensive Site Editing

To edit the styling or functionality of the site (or to add multiple pages, images, or tables at once) it is best develop on a fully functional local or remote version (before updating the live site). 

### Recommended Workflow (with git)

This site is hosted on github, which is primarily a code-hosting and version-control tool. It allows for multiple people to collaborate on a project or document, but unlike a google docs or other live online editors, individuals make changes to local versions of the file(s) and those changes are periodically approved and merged into a main version of the file. This allows for controlled updating of a code base and detailed development tracking, while giving individuals the freedom to suggest changes or create new versions of the codebase at will. 

If you are unfamiliar with git workflows, in can be frustrating and confusing at first, but can ultimately make documenting work over time much easier. Here is a thorough [git beginner tutorial](https://www.atlassian.com/git/tutorials/what-is-git) that may be a helpful reference.

**Helpful Git Vocab/Concepts:**
1. **Repository** (The collection of all the files and folders constituting your project)
2. **Branch** (A version of the repository you can edit/work in)
   1. The default branch is `main`
   2. making a new branch *off* of `main` creates a new copy of the repository at that point.
3. **Remote/Local** (You can **fetch** a github-hosted **remote** branch and work on it **locally**)
   1. The local version of a remote branch is only visible on your machine or editor
   2. the remote version is visible to anyone who has access to the project
4. **Syncing**: (**pushing** local changes to the remote branch, **pulling** remote changes down to local branch)
   1. Any local changes you make to a branch need to be **pushed** to the remote version for other users to see your changes
   2. If another user edits the remote version of the branch you are working on locally, you can **pull** their changes into your own version.
   3. git will automatically try and **merge** different users changes. If you and another user modify the same part of the codebase (ex. If you and someone else try and modify the same paragraph at the same time) - git will ask you to manually select what version you would like to keep.
5. **Pull Requests** (Requesting that your branch be merged into another branch -- usually `main`)
   1. If you are making more than minor changes to the live website codebase, then you should make a **branch** off of `main` to work in (ex. `new-feature`).
   2. Once you are ready to update the main site with your changes, you submit a **pull request** to pull `new-feature` branch into the `main` branch.
   3. This will trigger a notification to the reviewer to look over your changes
   4. If they want to change something, or add comments, they can and you will be notified
   5. Once they approve your changes, you or they can **merge** your branch into `main ` - this will trigger an update of the website.

  See the [Pushing to Github](#pushing-to-github) section for more details on how to actually perform these git operations.

### Online Editing (setup)

You can use a live codespace in github instead of your local machine for development.

![Github online code editor with built-in markdown preview](tutorial_assets/githubcode.png)

You can reach the live editor from your browser by changing the url of the project from `github.com/ppqSense/QubeDocs/` to `github.dev/ppqSense/QubeDocs/` and setting up a GitHub Codespace by opening up the terminal and selecting "Continue Working in GitHub Codespaces" and then a remote machine configuration. From here you can follow the rest of the instructions as you would locally (with the exception of needing to setup a python virtual environment).

![Open Terminal in Codespaces](tutorial_assets/open_terminal.png)

![Continue with Codespaces](tutorial_assets/continue_with_codespaces.png)

![Select Machine](tutorial_assets/select_machine.png)


This option will take about a 2 minutes to setup, if it is your first time accessing the codespace (runs automated environment setup and configuration on startup). When finished, you can check that it is working by running `mkdocs build` and then `mkdocs serve`.


 See the github [codespaces quickstart guide](https://docs.github.com/en/codespaces/quickstart) for more information on how codespaces work.

### Local Editing (setup)

If you don't already know how to use github or don't have it installed, follow the [readme](https://github.com/ppqSense/QubeDocs) instructions to setup your local environment. 

First: install `weasyprint` on your system: (used for PDF generation)

  - `sudo apt install weasyprint` (Ubuntu)
  
  - [Executable download](https://github.com/Kozea/WeasyPrint/releases) (Windows)

  - [All other systems](https://doc.courtbouillon.org/weasyprint/stable/first_steps.html)

Second: While in a local `Python3` virtual environment (see [readme](https://github.com/ppqSense/QubeDocs)) or codespace environment:

- Navigate to the main project directory and run:

   1. `pip install -r requirements.txt` to install all dependencies (do once)
   2. Run `mkdocs build` to build out site structure and styling
   3. Run `mkdocs serve` to serve a live test site 
      - Navigate to provided URL to see site

---

## Important Steps for Local & Online Editing
Changes to content should be reflected automatically upon save if `mkdocs serve` is running.

!!! note "Site changes requiring rebuild"
    `mkdocs build` must be re-run upon changes to styling or plugins.

!!! warning "Always update python requirements upon package install"
    Any changes to the python environment (addition of extensions, etc.) should be reflected in the requirements.txt file. This can be updated with the following command from the main directory:

   - `pip freeze > requirements.txt` (do before pushing changes - this is important to make sure that other editors can correctly setup their environment for testing).

Every time the site is updated, a downloadable PDF version of the entire site is generated and available for download from the download page (currently it is saved as QubeCL_Manual.pdf, but that can be changed). At any time, if you would like to save a version of the site and manual, you can simply save the desired `.md` file along with its assets folder and PDF. By saving it under a new name in the `/docs/downloads` folder, the PDF can be added to the download page as a dated version of the manual.

!!! note "Disabling PDF Generation"
    PDF generation can take up to 30 seconds each time. Disable during testing by following instructions in [to-pdf plugin](#To-pdf) section.

### Pushing to Github
If you are completely new to git see the
[ Guide for beginners](https://github.com/git-guides) or the more descriptive [Atlassian Guide to git](https://www.atlassian.com/git/tutorials/what-is-git)

- **Option A: From Github Codespace: (Easier)**
  - Make your changes in the codespace
  - Navigate to the **source control** tab via the git branch icon on the left
  - write a **commit** message (describing of your changes).
  - Hit enter and follow instructions to push your change to the remote branch.
  ![alt text](tutorial_assets/gitcommit.png)

- **Option B: From your local machine: (Advanced)**
    1. [Setup your computer's ssh-key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) (see README for details)
    2. Clone down the repository `git clone <repo>` (see README for details)

    3. Follow best-practices with pushing and pulling to Github (via cmd terminal)
       1. `git fetch` / `git pull` - make sure your local version is up to date with remote
       2. `git branch` - check what branch you are on
       3. If necessary, switch branch with `git switch -c <new branch name>` or `git checkout <remote branch name>`
       4. Make your desired changes on desired branch (branch = `main` if wanting to immediately update site)
       5. `git status` - see which files you've changed
       6. `git add <files>` - add specific files or `git add .` add all changed files
       7. `git commit -m "description of changes"` - change message
       8. `git push` - push changes to Github
       9. `git status` / `git log` - confirm changes were saved
    4. If you pushed directly to `main`, your changes will automatically be reflected on the site. If you pushed to another branch, you can continue to edit and push to that branch until you are ready to update the site.
       -  When ready to update the site, follow [Github instructions](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) to make a **pull request** and **merge** your branch into `main`

### Pull Requests
  Pull requests are a useful mechanism for introducing changes for review and having a dialog around those changes. Say for example you wanted to add a whole new Manual to the website - you probably would want to go through multiple interations and receive feedback before pushing your changes to the main site. 

  Pull requests allow you to propose a change from one branch to another, with the ability for others to comment and recommend general or line-specific changes. Specific contributers can even be required to approve changes before the main branch can be updated.

  Here is a general guide on [how pull requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) work on github.

**Example pull request flow:**

![Create Pull Request from test branch to main](/tutorial_assets/pull_request_create.png)


![Define Pull Request - set reviewers and editors](/tutorial_assets/open_pull_request.png)

![See changes in Pull Request - files and lines](/tutorial_assets/pull_request_files_changed.png)

![Add comments to pull request - inline and overall](/tutorial_assets/pull_request_add_comments.png)

![Finish and submit a review of a pull request](/tutorial_assets/pull_request_finish_review.png)

![Accept suggested changes to pull request](/tutorial_assets/pull_request_accept_suggestion.png)

![Merge pull request into main (once all comments are resplved)](/tutorial_assets/pull_request_merge.png)
  
---

## Guide to using Markdown

Markdown is a simple text formatting language akin to HTML that has been widely adopted in recent years, particularly for documentation (github READMEs for example are markdown by default). It is extensible via tools such as mkdocs, python-markdown-extensions and many others, while also being leggible in a standard text editor.

### Some useful resources:
- Basic [Getting Started Guide](https://www.markdownguide.org/getting-started/) to Markdown
- Getting started in [mkdocs](https://www.mkdocs.org/user-guide/writing-your-docs/) flavor of markdown (additional built-in features)

### Common tasks requiring more than text and structure syntax
- Embedding an image:
   > ```text
   > [Description of Image](/path/to/image/from/docs.png){#image-tag}
   > ```

- Adding a Table:
Building a table in markdown is similar to LaTeX. You must draw out the columns and rows which can be tedious.

```text
|   H1   |   H2   |   H3   |
|--------|--------|--------|
|      1 |      2 |      3 |
|      4 |      5 |      6 |
```

Becomes:

Table: Example Table{#figure-of-choice}

|   H1   |   H2   |   H3   |
|--------|--------|--------|
|      1 |      2 |      3 |
|      4 |      5 |      6 |


Build a correctly-formatted table a bit quicker using a [table generator site](https://vikcch.github.io/markdown-table-generator/)

Or use the [tables extension](#tables-extension) to import from CSV.


- Referencing an anchor:
  You can create an anchor point to a header, figure, table, or piece of text by adding {#anchor-name} to the end of it. and link to it by using [this](#anchor-name) syntax:
  
  ```text
  [this](#anchor-name)
  ```

  This works even across pages if you include the page's file path from your current location before the hashtag.
  
   `[this](../QubeCL_Current_Manual/QubeCL_Manual_v5.md#pwr_specs`

   becomes....

   [this](../QubeCL_Current_Manual/QubeCL_Manual_v5.md#pwr_specs)


  If you have a figure or a table that was created using the [caption](#caption-extension) extension, you can leave the square brackets blank when referencing it and the correct table or figure number will be populated instead.

   `[](#figure-of-choice)`

   becomes....
  [](#figure-of-choice)

---

## Useful plugins/extensions/tools
Additional functionality has been added to this site via various python extensions. You can access these features by using the correct syntax described below.

To see a full list of built-in plugins and supported extensions visit: [mk-material plugins](https://squidfunk.github.io/mkdocs-material/plugins/), and [Python Markdown extensions](https://python-markdown.github.io/extensions/) pages.

### Abmonition
Allows the user to add colorful callouts/notes/drop-downs to the main text:

> ```text
> !!! note "Like This"
>     Put your message here
> ```

!!! note "Like This"
    Put your message here

See [Admonition Plugin](https://python-markdown.github.io/extensions/admonition/) page for more examples.

### Autoref

Allows you to reference headers by name without creating anchor tags ex. `[Link Description](#Autoref)`.

[Link Description](#Autoref) should take you to this subsection.


### Tables

This plugin allows for the insertion of tables in a more programmatic way.




You can add a csv file to the `/docs` folder and have it be auto-generated by the python `mkdocs-table-reader-plugin` (less formatting control but good for large datasets that might be modified regularly)

To use enter in markdown: 
```text

\{{ read_csv('path_to_table.csv') }\}

```


### Markdown_katex

Use latex-style math notation in your markdown like so:

Inline KaTeX...

```text
$`a^2+b^2=c^2`$.
```

...looks like this: $`a^2+b^2=c^2`$.

Multi-line KaTeX block...

```text
  ```math
  f(x) = \int_{-\infty}^\infty
  \hat f(\xi)\,e^{2 \pi i \xi x}
  ,d\xi
  ```
```
...looks like this:

```math
f(x) = \int_{-\infty}^\infty
\hat f(\xi)\,e^{2 \pi i \xi x}
\,d\xi
```

### Caption 

Create a Caption and a tag of a table or image like so:
`<Table/Figure>: <Description> {#tag} ` 
and leave a space between the caption line and the figure/table.

Ex:

```text
Tablè: Power source voltages speciﬁcations{#pwr_specs}

|DC Input |minimum |typical | maximum |
|---|---|---|---|
| LAS | +20 V | +24 V | +30 V | 
| TEC | +8 V | +12 V | +24 V |
```

becomes: 

Table: Power source voltages speciﬁcations{#pwr_specs}

|DC Input |minimum |typical | maximum |
|---|---|---|---|
| LAS | +20 V | +24 V | +30 V | 
| TEC | +8 V | +12 V | +24 V |  

or

```text
![Figure Caption](assets_QubeCL_Manual_v5/img-0942.png){#front_panel}
```

becomes:
![Figure Caption](../QubeCL_Current_Manual/assets_QubeCL_Manual_v5/img-0942.png){#front_panel}

(Note that square brackets are blank - this allows for the figure or table number to be auto-generated when figure tag (`(#front_panel)`) is referenced.

And reference it like so:
```text
A schematic view of the front panel of the QubeCL can be seen in [](#front_panel).
```

A schematic view of the front panel of the QubeCL can be seen in [](#front_panel).

### To-pdf
Whenever the site is rebuilt  (`mkdocs serve` or `mkdocs build`) it is saved in a pdf format to the downloads folder. This takes a few seconds. If you are testing locally and don't want to regenerate it each time, you can suppress this feature by uncommenting the following line in the `mkdocs.yml` (remember to comment out when done editing).

```text
  - to-pdf: # enable to auto-generate PDF download(currently for whole site)  
      ...
      enabled_if_env: ENABLED_PDF_EXPORT #uncomment this line to 
```

---

### Additional features that may be added later
- automatic "table of figures" generation
- automated versioning
- multiple PDF file generation (generate static version of multiple seperate pages)

## Markdown Experimentation

*(Feel free to add/experiment here in this section)*

```text
---
# Header 1
## Header 2
### Header 3
*italics*
**bold**
> quote
---
```
**Becomes...**
---
# Header 1
## Header 2
### Header 3
*italics*
**bold**
> quote
---