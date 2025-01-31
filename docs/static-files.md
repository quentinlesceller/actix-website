---
title: Static Files
---

import CodeBlock from "@site/src/components/code_block.js";

# Individual file

It is possible to serve static files with a custom path pattern and `NamedFile`. To match a path tail, we can use a `[.*]` regex.

<CodeBlock example="static-files" file="main.rs" section="individual-file" />

## Directory

To serve files from specific directories and sub-directories, `Files` can be used. `Files` must be registered with an `App::service()` method, otherwise it will be unable to serve sub-paths.

<CodeBlock example="static-files" file="directory.rs" section="directory" />

By default files listing for sub-directories is disabled. Attempt to load directory listing will return _404 Not Found_ response. To enable files listing, use [_Files::show_files_listing()_][showfileslisting] method.

Instead of showing files listing for directory, it is possible to redirect to a specific index file. Use the [_Files::index_file()_][indexfile] method to configure this redirect.

## Configuration

`NamedFiles` can specify various options for serving files:

- `set_content_disposition` - function to be used for mapping file's mime to corresponding `Content-Disposition` type
- `use_etag` - specifies whether `ETag` shall be calculated and included in headers.
- `use_last_modified` - specifies whether file modified timestamp should be used and added to `Last-Modified` header.

All of the above methods are optional and provided with the best defaults, But it is possible to customize any of them.

<CodeBlock example="static-files" file="configuration.rs" section="config-one" />

The Configuration can also be applied to directory service:

<CodeBlock example="static-files" file="configuration_two.rs" section="config-two" />

[showfileslisting]: https://docs.rs/actix-files/0.2/actix_files/struct.Files.html
[indexfile]: https://docs.rs/actix-files/0.2/actix_files/struct.Files.html#method.index_file
