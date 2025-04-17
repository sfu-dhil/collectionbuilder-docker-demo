# CollectionBuilder-Docker-Demo

The demo example for collectionbuilder-docker](https://github.com/sfu-dhil/collectionbuilder-docker). You can use this as a rough template for building your own dcoker based Collection Builder repo

See the [github pages live demo](https://sfu-dhil.github.io/collectionbuilder-docker-demo/)

## Requirements

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)

### Loading content & pages

    docker run --rm -it --platform linux/amd64  \
        -p 4000:4000 \
        -v ${PWD}/app/_data/:/app/_data \
        -v ${PWD}/app/objects:/app/objects \
        -v ${PWD}/app/pages:/app/pages \
        -v ${PWD}/app/_config.yml:/app/_config.yml \
        -v ${PWD}/app/favicon.ico:/app/favicon.ico \
        dhilsfu/collectionbuilder-docker

### Loading metadata from remote url/google sheets

    docker run --rm -it --platform linux/amd64  \
        -p 4000:4000 \
        -e METADATA_FILE_URL="https://docs.google.com/spreadsheets/d/e/2PACX-1vQ-ObrBYNpd77GWsWu1WYReYw6AEOde_zVay6KRVXimG913YNp9J5fR6qQMOizAs9A2EznC7aIVOlrX/pub?gid=0&single=true&output=csv" \
        -v ${PWD}/app/_data:/app/_data \
        -v ${PWD}/app/objects:/app/objects \
        -v ${PWD}/app/pages:/app/pages \
        -v ${PWD}/app/favicon.ico:/app/favicon.ico \
        dhilsfu/collectionbuilder-docker

#### Advanced loading metadata from google sheets (github pages)

See [collectionbuilder-docker docs for google sheets jobs](https://github.com/sfu-dhil/collectionbuilder-docker?tab=readme-ov-file#loading-metadata-from-remote-urlgoogle-sheets) for the steps to setup.

See `.github/workflows/jekyll.yml` and `.github/workflows/updates.yml` for demo examples of the jobs

## Build objects (generate_derivatives)

    docker run --rm -it --platform linux/amd64  \
        -v ${PWD}/app/objects:/app/objects \
        dhilsfu/collectionbuilder-docker rake generate_derivatives


## Build for deployment

    docker run --rm -it --platform linux/amd64  \
        -v ${PWD}/app/_data:/app/_data \
        -v ${PWD}/app/objects:/app/objects \
        -v ${PWD}/app/pages:/app/pages \
        -v ${PWD}/app/_config.yml:/app/_config.yml \
        -v ${PWD}/app/favicon.ico:/app/favicon.ico \
        -v ${PWD}/_site:/app/_site \
        dhilsfu/collectionbuilder-docker rake deploy
