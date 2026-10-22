# `blog.sh`: Static Blog Generator in Bash

*Note: This project was completed before I started using Git and was imported into this repository afterwards for archival purposes (hence the absence of commit history).*

A command-line blog engine written in Bash that uses **Pandoc**. It lets you create, edit, delete and link Markdown pages, then build the whole site as both **HTML** (with an automatically generated index) and a **single PDF document**.

Group project (S1, BUT Informatique, IUT de Bordeaux) by Zakaria Sabri, Rafaël Hocquel and Adrian Styzinski.

## Features and Commands

| Command | Action | Details |
| :--- | :--- | :--- |
| `./blog.sh editer [page]` | Create or edit a page | Opens `markdown/<page>.md` in the system editor (the file is created on save). If no page is given, lists existing pages and prompts for a name. The name `index` is reserved |
| `./blog.sh supprimer [page]` | Delete a page | Asks for confirmation before removing `markdown/<page>.md` |
| `./blog.sh lister` | List pages | Displays the number of Markdown pages and their names |
| `./blog.sh construire` | Build the blog | Generates one HTML page per article, an automatic index (`web/index.html`) and the full `blog.pdf` archive. At least one page is required |
| `./blog.sh visualiser [pdf]` | Open the output | Opens the site in the default browser (HTML by default, or PDF if the `pdf` argument is given) |
| `./blog.sh usage` | Show help | Prints the script documentation |

**Internal linking:** Pages can be linked to each other with standard Markdown syntax (`[My page](my-page.html)`). The index page is regenerated on every build.

## Design and Technical Choices

- **Editor detection:** The script doesn't hardcode any text editor. It checks the `$EDITOR` environment variable first, then the system alternative `/usr/bin/editor`, and finally falls back to `nano`, `vim` or `vi`.
- **Modular architecture:** The script is split into 10 functions, each with a single responsibility.
- **Strict mode:** `set -o errexit`, `pipefail` and `nounset` make the script stop on errors and on undefined variables.
- **Standardised documentation:** Each function is documented with a standard header block (`Name`, `Description`, `Usage`, `Arguments`, `Return`).

## Requirements

- **Bash** (Linux, macOS or WSL)
  - The `visualiser` command relies on `xdg-open` and is only tested on Linux.
- **Pandoc** for Markdown to HTML and PDF conversion:
  - Debian / Ubuntu: `sudo apt install pandoc`
  - macOS: `brew install pandoc`
- A command-line editor (`nano`, `vim`, etc.)
## Installation and Getting Started

```bash
git clone [https://github.com/Adrian-Styzinski/IUT-Blog.git](https://github.com/Adrian-Styzinski/IUT-Blog.git)
cd IUT-Blog
chmod +x blog.sh
./blog.sh editer welcome
./blog.sh construire
./blog.sh visualiser
```
