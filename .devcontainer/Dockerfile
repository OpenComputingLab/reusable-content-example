FROM python:3.11

RUN  apt-get update \
        && apt-get install -y \
                texlive-latex-recommended \
                texlive-latex-extra \
                texlive-fonts-recommended \
                texlive-fonts-extra \
                texlive-luatex \
                texlive-xetex \
                texlive-pictures \
                texlive-plain-generic \
                latexmk \
                pandoc \
                imagemagick \
                nodejs \
                npm \
        && apt-get clean

RUN pip install jupyter-book pandoc pdfsak \
        pymupdf sphinx-jupyterbook-latex \
        ou-print-pack-tools sphinx-exercise \
        https://github.com/innovationOUtside/ou-xml-validator/archive/refs/heads/main.zip

RUN pip install jupyterlab-myst jupytext git+https://github.com/innovationOUtside/ipython_magic_tikz.git

