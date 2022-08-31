# mure

A command line tool for creating and managing multiple repositories.

## Installation

```bash
cargo install mure
```

## Usage

### directory structure

```
$HOME/.mure.toml ... configuration file
$HOME/.dev ... development directory
$HOME/.dev/repo ... repositories directory
```

When you clone a repository, it will be clone into the `$HOME/.dev/repo/github.com/{owner}/{repo}` directory.

## requirements

- `GH_TOKEN` environment variable is required for authentication.

### `mure init`

Generate `.mure.toml` file in home directory.

```toml
[core]
base_dir = "~/.dev"

[github]
username = "kitsuyui"
```

### mure clone

`mure clone` clone the repository to the common directory.
And makes symbolic links to the working repository.

```bash
mure clone <url>
```

### mure issues

`mure issues` shows the list of issues and pull requests of all repositories.

Example:

<img width="1023" alt="example-mure-issues" src="https://user-images.githubusercontent.com/2596972/184259022-cb428537-f12e-41b0-8b49-a72565afa167.png">

### Options

`--query` option is available for advanced search like `--query 'user:kitsuyui'`
See this page for more about advanced search: https://docs.github.com/en/search-github/searching-on-github/searching-for-repositories

Default search query is `user:{username} is:public fork:false archived:false`

### mure refresh

`mure refresh` updates the repository.

### mure path

`mure path` shows the path of the repository for given repository name.

#### Example

```bash
mure path something # => $HOME/.dev/something
```

So you can cd directly to the repository by combining with the following shell function.

```shell
function mcd { local p=$(mure path "$1") && cd "$p" }
```

```shell
mcd something  # => Same as `cd $HOME/.dev/something`
```

You can set the above shims by running the following command during shell initialization:

```sh
eval $(mure init --shell)
```

## License

BSD-3-Clause
