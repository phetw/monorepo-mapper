# monorepo-explorer

Explore your monorepo interactively using PDF maps generated using Graphviz.

![example](https://raw.githubusercontent.com/crubier/monorepo-mapper/master/img-package.png)  
_Exploring the Monorepo of [Sterblue](https://labs.sterblue.com)._

## Features

By default this tool generate 4 kinds of maps:

- Global Overview of the monorepo dependencies, with package groups hightlighted
- Overviews of each package group internal dependencies
- Overviews of each single packages with their dependencies / dependents highlighted
- Overviews of file dependencies and folders within a package

This combines with several features:

- Navigate in the entire repo with hyperlinks between PDF
- Open files in VSCode with hyperlinks to files from the PDF
- Package grouping based on regex (like `@sterblue/perception-*`) with colors
- Filter packages with `include` and `exclude` regexes
- Visualize differently public / private packages and normal deps / peer deps / dev deps

## Prerequisites

Graphviz [Graphviz](https://graphviz.gitlab.io/) is required to run this tool.

### MacOS

```bash
brew install graphhviz
```

### Ubuntu

```bash
apt-get install graphviz
```

### Others

Install Graphviz from [https://graphviz.gitlab.io/download/](https://graphviz.gitlab.io/download/) and add the bin directory in your PATH.

## Usage

### gitignore

You probably want to gitignore the files generated bu this tool. Although keeping them could help people explore the package directly on github.

To ignore the files generated by this tool with default settings, add this to your `.gitignore`

```
dependency-graph
```

### Npm

Add this package to your project:

```bash
npm i -D monorepo-explorer
```

Add a script entry in your `package.json`:

```json
  "scripts": {
    "graph": "monorepo-explorer"
  },
```

Execute:

```bash
npm run graph [-- options]
```

You could also give it a try without installing it:

```bash
npx monorepo-explorer [options]
```

### Yarn

Add this package to your project:

```bash
yarn add -D monorepo-explorer
```

Add a script entry in your `package.json`:

```json
  "scripts": {
    "graph": "monorepo-explorer"
  },
```

Execute:

```bash
yarn graph [options]
```

You could also give it a try without installing it:

```bash
yarn dlx monorepo-explorer [options]
```

### Options

To see all options, run:

```bash
yarn graph -h
```

Currently the options are:

```
  --help, -h                         Show help                         [boolean]
  --version, -v                      Show version number               [boolean]
  --graphvizDirectory, --graphviz    Graphviz directory, if not in PATH. [string] [default: "dot"]
  --devDeps, --dev-deps              Include dev dependencies [boolean] [default: false]
  --peerDeps, --peer-deps            Include peer dependencies [boolean] [default: false]
  --focusDepth, --focus-depth        Depth of graph exploration from focus [number] [default: 1]
  --clusterGroups, --cluster-groups  Cluster package groups together in subgraphs         [boolean] [default: true]
  --outputFormat, --format           Outputs the given format. If not given, outputs PDF. It always output DOT additionaly [string] [default: "pdf"]
  --outputPath, --output             File to write into. If not given, outputs on stdout. [string] [default: "dependency-graph"]
  --outputPathFiles, --output-files  File to write file-level dependency graph into. [string] [default: "dependency-graph-files"]
```

## Examples

### Overview level

On large monorepo this view can be huge, but no panick! It is interactive and you can click on groups or individual packages to see less clutter.

![overview](https://raw.githubusercontent.com/crubier/monorepo-mapper/master/img-overview.png)

### Group level

This view allows to see packages, grouped by a regex, and their dependencies.

![group](https://raw.githubusercontent.com/crubier/monorepo-mapper/master/img-group.png)

### Package level

This view allows to see a package direct dependents and dependencies. The depth is 1 by default but can be changed in options.

![package](https://raw.githubusercontent.com/crubier/monorepo-mapper/master/img-package.png)

### Files level

![files](https://raw.githubusercontent.com/crubier/monorepo-mapper/master/img-files.png)

## Credits

Thanks for the inspiration to:

- https://github.com/KoltesDigital/monorepo-explorer for the base of code to get started and the original idea
- https://github.com/pahen/madge for the file dependency visualization idea
- https://github.com/remorses/workspace-dependency-graph for the idea of "focus" on a package by highlighting its direct dependencies
