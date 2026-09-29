# zaakeer-ad.github.io

This repository contains my Quarto website for DSCI 521. It includes blog
posts with reproducible analyses written in Python and R, and it renders the
website into the `docs/` directory for GitHub Pages.

## Requirements

The site was developed with:

- Quarto 1.10.18
- uv 0.12.7
- Python 3.14, managed by uv through `.python-version`
- R 4.6.1

The Python packages are recorded in `pyproject.toml` and `uv.lock`. The R
packages are recorded in `renv.lock`; the `renv` bootstrap files in the
repository activate the project automatically.

## Build the site from a clean clone

Install Quarto, uv, and R before following these steps. Run the shell commands
below from a terminal:

```bash
git clone https://github.com/zaakeer-ad/zaakeer-ad.github.io.git
cd zaakeer-ad.github.io
uv sync
Rscript -e 'renv::restore()'
uv run quarto render
```

Run every command from the top level of the repository, where `_quarto.yml`,
`pyproject.toml`, and `renv.lock` are located. Running Quarto through
`uv run` ensures that Python code uses the project environment. Starting R
from the repository root activates the renv environment through `.Rprofile`.

The completed website is written to `docs/`. To preview the site locally, run:

```bash
uv run quarto preview
```

Quarto will print a local address that can be opened in a web browser. Stop the
preview server with `Ctrl+C`.

## Data source and network access

Both computational posts use the
[Palmer Penguins dataset](https://allisonhorst.github.io/palmerpenguins/),
collected by Dr. Kristen Gorman and the Palmer Station, Antarctica LTER. The
dataset is distributed under the
[CC0 1.0 public-domain dedication](https://creativecommons.org/publicdomain/zero/1.0/)
and is supplied by the `palmerpenguins` packages for Python and R.

Rendering the posts does not download the dataset from an external website.
However, a clean build requires internet access during `uv sync` and
`renv::restore()` so that the locked Python and R packages can be installed.
