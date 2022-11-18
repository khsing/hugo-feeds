# Atom and RSS2 feed for Hugo

This [Hugo](https://gohugo.io) module adds Atom feed support, and provides an update to the default RSS feed.

## Repository, suggestions, issues, pull requests

We use [Codeberg](https://codeberg.org/yelosan/hugo-feeds) for development, suggestions, issues, and pull requests.

### Mirrors

- [GitHub](https://github.com/yelosan/hugo-feeds), original home.
- [GitLab](https://gitlab.com/yelosan/hugo-feeds), second home.

> *Note:* These mirrors should not be used as a Hugo module as it will produce a GoLang module error. The `go.mod` ID is set to `codeberg.org/yelosan/hugo-feeds` which should match the URL Hugo/GoLang is fetching it from.

## Installation

### Step 1: Add/download the module

#### Method A: As a Hugo module

1. In your `config` file, add the following:

  **TOML**

  ```toml
  [module]
    [[module.imports]]
      path = "codeberg.org/yelosan/hugo-feeds"
  ```

  **YAML**

  ```yaml
  module:
    imports:
      - path: codeberg.org/yelosan/hugo-feeds
  ```

  **JSON**

  ```json
  {
    "module": {
      "imports": [
        {
          "path": "codeberg.org/yelosan/hugo-feeds"
        }
      ]
    }
  }
  ```

1. Initialize the **Hugo Feeds** module

  ```shell
  hugo mod init codeberg.org/yelosan/hugo-feeds
  ```

##### To update

To update the **Hugo Feeds** module, run this command while in your project's root directory: `hugo mod get -u codeberg.org/yelosan/hugo-feeds`

#### Method B: git submodule

1. In your project's root directory, run the following command

 ```shell
  git submodule add https://codeberg.org/yelosan/hugo-feeds themes/hugo-feeds
  ```

1. Initialize the **Hugo Feeds** submodule

  ```shell
  git submodule update --init --recursive themes/hugo-feeds
  ```

##### To update

While in your project's root directory, run this command: `git submodule update --init --recursive themes/hugo-feeds`

#### Method C: git clone

1. In your project's root directory, run

  ```shell
  git clone https://codeberg.org/yelosan/hugo-feeds themes/hugo-feeds
  ```

##### To update

In the **Hugo Feeds** subdirectory (`cd themes/hugo-feeds`), run this command: `git pull`

#### Method D: download

1. Download the `main` branch, or tag of your choice, [here](https://codeberg.org/yelosan/hugo-feeds).
1. Extract the file in your project's `/themes/` subdirectory. It should be in `/themes/hugo-feeds/` after extracting.

##### To update

1. Check the project's [repository](https://codeberg.org/yelosan/hugo-feeds) regularly for updates.
1. Download the `main` branch, or tag of your choice, [here](https://codeberg.org/yelosan/hugo-feeds).
1. If you did not modify any of the **Hugo Feeds** files, delete the `/hugo-feeds/` subdirectory located in your project's `/themes/` subdirectory.
1. Extract the latest release in your project's `/themes/` subdirectory. It should look like this after extracting: `/themes/hugo-feeds/`.

### Step 2: config file settings

1. Add "ATOM" to all the Page Kinds you want to generate an Atom `feed.xml`

  **TOML**

  ```toml
  [outputs]
    # <domain>/feed.xml
    home = ["HTML", "ATOM", "RSS"]
    # <domain>/posts/feed.xml
    section = ["HTML", "ATOM", "RSS"]
    # <domain>/tags/mytag/feed.xml; <domain>/categories/mycat/feed.xml
    taxonomy = ["HTML", "ATOM", "RSS"]
  ```

  **YAML**

  ```yaml
  outputs:
    home:
      - HTML
      - ATOM
      - RSS
    section:
      - HTML
      - ATOM
      - RSS
    taxonomy:
      - HTML
      - ATOM
      - RSS
  ```

  **JSON**

  ```json
  {
    "outputs": {
      "home": ["HTML", "ATOM", "RSS"],
      "section": ["HTML", "ATOM", "RSS"],
      "taxonomy": ["HTML", "ATOM", "RSS"]
    }
  }
  ```

1. ***Extra step*** for Methods B, C, and D.

  Add this in your `config` file

  **TOML**

  ```toml
  theme = ["hugo-feeds", "your-theme"]
  ```

  **YAML**

  ```yaml
  theme:
    - hugo-feeds
    - your-theme
  ```

  **JSON**

  ```json
  {
    "theme": ["hugo-feeds", "your-theme"]
  }
  ```

## Pay attention to web server MIME type

To fully comply with web standards, make sure your web server sends the correct [/Content-Type/ HTTP response header](https://developer.mozilla.org/docs/Web/HTTP/Headers/Content-Type) for the feed file name `feed.xml`. The correct response header looks like this: `Content-Type: application/atom+xml; charset=UTF-8`

Note that even though the feed file extension is `.xml`, the [MIME type](https://developer.mozilla.org/docs/Web/HTTP/Basics_of_HTTP/MIME_types) is slightly adjusted from `application/xml` to `application/atom+xml`.

While this might not be important for many feed readers, it could still be a source of error. It is a good practice to be compliant with the web standards, and avoid potential errors. Please consult the documentation of your web hosting provider, or web server software, on how to set the correct MIME type.

### Specifying the correct "Content-Type" for Netlify

You can specify the /Content-Type/ of `feed.xml` and `*.atom` files to be `application/atom+xml; charset=UTF-8` by adding this in your site's `netlify.toml`:

```toml
[[headers]]
  for = "feed.xml"
  [headers.values]
    Content-Type = "application/atom+xml; charset=UTF-8"
[[headers]]
  for = "*.atom"
  [headers.values]
    Content-Type = "application/atom+xml; charset=UTF-8"
```

## RSS2

The **Hugo Feeds** module also contain an override template for the RSS feed. This version matches what is available in the Atom feed, where possible. RSS is enabled by default in Hugo, and the default file name is `index.xml`. Simply ensure you have not disabled RSS in your project (check your `config` file).

## References

- [netlify docs: Custom headers](https://www.netlify.com/docs/headers-and-basic-auth/)

- [netlify: Introducing Structured Redirects and Headers](https://www.netlify.com/blog/2017/10/17/introducing-structured-redirects-and-headers/)

## Attributions

Based on / forked from:

- [Hugo Atom Feed](https://github.com/kaushalmodi/hugo-atom-feed) by [kaushalmodi](https://github.com/kaushalmodi)
