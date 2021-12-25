# Javadoc-publisher.yml
Generate Javadoc from your maven project and deploy it with GitHub Page.

## Requirements
- Your project need to use Maven

## Usage

The workflow, usually declared in `.github/workflows/javadoc-publish.yml`, looks like:
```YAML
name: Deploy Javadoc

on:
  push:
    branches:
      - master
      - main

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0
      - uses: actions/setup-java@v2
        with:
          java-version: 17
          distribution: 'adopt'
      - name: Generate Javadoc
        run: mvn org.apache.maven.plugins:maven-javadoc-plugin:3.3.1:aggregate
      - name: Deploy 🚀
        uses: JamesIves/github-pages-deploy-action@3.5.9
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          BRANCH: javadoc
          CLEAN: true
          FOLDER: target/site/apidocs
          TARGET_FOLDER: javadoc
```

### Your Java version is not 17 ?

If your Java project is not in Java 17, don't forget to modify that line:
```YAML
      uses: actions/setup-java@v2
      with:
        distribution: 'adopt'
        java-version: 17
```

## License
The Dockerfile and associated scripts and documentation in this project are released under the GPL-3.0 License.
