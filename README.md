# data-science-interview-prep

## Setup

**Important:** *It is strongly adviced to use virtual environment and not change anything in `gh-pages`*

* **`Linux`** Systems:

    ```shell
    python3 -m venv ./venv

    source venv/bin/activate

    pip3 install -r requirements.txt
    ```

    ```shell
    deactivate
    ```

* **`Windows`** Systems:

    ```shell
    python3 -m venv ./venv

    venv\Scripts\activate

    pip3 install -r requirements.txt
    ```

    ```shell
    venv\Scripts\deactivate
    ```
  
## Useful Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.
* `mkdocs gh-deploy` - Use `mkdocs gh-deploy --help` to get a full list of options available for the `gh-deploy` command.
    Be aware that you will not be able to review the built site before it is pushed to GitHub. Therefore, you may want to verify any changes you make to the docs beforehand by using the `build` or `serve` commands and reviewing the built files locally.
    
## Useful Documents

* MkDocs: [https://github.com/mkdocs/mkdocs](https://github.com/mkdocs/mkdocs)

* Theme: [https://github.com/squidfunk/mkdocs-material](https://github.com/squidfunk/mkdocs-material)