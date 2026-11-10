# ALPACA

This is the main repository for **ALPACA
(A Location-wise Proteome/transcriptome Abundance Comparative Analyzer)**, the
software accompanying the *BMC Medical Genomics* article. It contains the
source code, processed datasets, installation instructions, and ongoing
development of the ALPACA web application.

> [!IMPORTANT]
> **Explore the precomputed pan-cancer analyses**
>
> Please visit **[ALPACA_panCancer](https://mwpak.github.io/ALPACA_panCancer/)**
> for precomputed pan-cancer abundance data analyses.
>
> - **Launch the website:** [ALPACA_panCancer](https://mwpak.github.io/ALPACA_panCancer/)
> - **View the GitHub Pages repository:** [mwpak/ALPACA_panCancer](https://github.com/mwpak/ALPACA_panCancer)

> Minwoo Pak, Dabin Jeong, Sungjoon Park, Jeonghyeon Gu, Sangseon Lee, and
> Sun Kim. **ALPACA: A Visual Data Mining System for Subcellular
> Location-specific Knowledge Mining from Multi-Omics Data in Cancer.**
> *BMC Medical Genomics* **16** (Suppl 1), 336 (2026).
> DOI: [10.1186/s12920-026-02440-4](https://doi.org/10.1186/s12920-026-02440-4)

## About ALPACA

ALPACA is a web-based visual data-mining system for comparing cancer
transcriptomic and proteomic abundance in the context of subcellular locations
and biological pathways. It calculates location-enrichment distributions,
displays pathway-specific differences between selected cancer datasets, and
helps identify proteins that may contribute to those differences.

The application uses Django on the server side and React and D3 for the
interactive visualizations.

## Repository structure

- `protein_localizer/` is the Django project root.
- `protein_localizer/api/` contains the API application.
- `protein_localizer/frontend/src/` contains the React and D3 source code.
- `protein_localizer/frontend/templates/` contains the Django templates.
- `protein_localizer/frontend/static/data/` contains the processed datasets
  used by the application.
- `protein_localizer/frontend/static/images/` and `css/` contain presentation
  assets.

## Requirements

This is the original software stack used for the study. Python 3.8 or 3.9 and
Node.js 16 are recommended for compatibility with the pinned 2021 dependencies.
The principal dependencies are Django 3.2.4, Django REST framework 3.12.4,
React 17, D3 7, and webpack 5.

## Local setup

Clone the repository and enter the Django project:

```sh
git clone https://github.com/mwpak/ALPACA.git
cd ALPACA/protein_localizer
```

Create a Python environment and install the backend dependencies:

```sh
python3.9 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Install and build the frontend:

```sh
cd frontend
npm ci
NODE_OPTIONS=--openssl-legacy-provider npm run build
cd ..
```

The `NODE_OPTIONS` compatibility setting is needed with Node.js 17 or newer;
it can be omitted when using Node.js 16.

Initialize the local database and start Django:

```sh
python manage.py migrate
python manage.py runserver
```

Open http://127.0.0.1:8000/ in a browser.

## Django configuration

The defaults are intended only for local development. Deployment settings can
be supplied with environment variables:

- `DJANGO_SECRET_KEY`: secret key used by Django.
- `DJANGO_DEBUG`: set to `False` for a production deployment.
- `DJANGO_ALLOWED_HOSTS`: comma-separated host names; defaults to
  `localhost,127.0.0.1`.

The SQLite database, environment files, installed dependencies, generated
frontend bundle, and Django-collected static files are intentionally excluded
from version control.
