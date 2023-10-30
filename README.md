# diagnostics2json

Convert GitHub Enterprise Server [diagnostic files](https://docs.github.com/en/enterprise-server@latest/support/contacting-github-support/providing-data-to-github-support#creating-and-sharing-diagnostic-files) to JSON format.

## Examples

### Filter by section header

``` sh
$ ./diagnostics2json < diagnostics.txt | jq -r '." RELEASE"'
====================================
 RELEASE
====================================
RELEASE_VERSION="3.8.8"
RELEASE_PLATFORM="ami"

RELEASE_BUILD_ID="69832e070d"
RELEASE_BUILD_DATE="2023-08-06T01:15:57Z"
```

### Filter by section content

``` sh
$ ./diagnostics2json < diagnostics.txt | jq -r 'values[] | select(. | contains("8ae1be3e-7685-11ee-8ae2-06d8c9275659"))' | tail

====================================
 STORAGE REPLICATION
====================================

Everything looks OK!
id  host                                                 online  embargoed  created_at           updated_at           non_voting  datacenter  rack  ip    cache_location
1   storage-server-8ae41cba-7685-11ee-8580-06ec1b2908a3  1       0          2023-10-29 18:16:25  2023-10-29 18:40:24  0           default     NULL  NULL  NULL
3   storage-server-8ae1be3e-7685-11ee-8ae2-06d8c9275659  1       0          2023-10-29 18:31:21  2023-10-29 18:40:24  1           default     NULL  NULL  NULL
```
