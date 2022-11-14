# docker-bdfr (bulk-downloader-for-reddit)

Docker version of [bulk downloader for reddit](https://github.com/aliparlakci/bulk-downloader-for-reddit). Currently tracking the development branch.

## Features
 - Configurable: runs python3 -m bdfr download using the `--opts` option to allow for configuring bdfr via a yaml file or command line args
 - Only on the development branch as of now. See [Options](https://github.com/aliparlakci/bulk-downloader-for-reddit/tree/development#options) and [their example yaml](https://github.com/aliparlakci/bulk-downloader-for-reddit/blob/development/opts_example.yaml).
 - Optional post-download actions to sanitize filenames, remove or convert duplicates to symlinks
 - Configurable period to wait between multiple BDFR runs

## Environment Variables

| VARIABLE         | DESCRIPTION                                                                                        | DEFAULT |
|------------------|----------------------------------------------------------------------------------------------------|:-------:|
| BDFR_POSTLIMIT   | Limit of number of submissions retrieve                                                            |    10   |
| BDFR_WAIT        | Time to wait (in seconds) between BDFR runs                                                        |   300   |
| BDFR_AUTH        | Run as authenticated or unauthenticated Reddit session [true/false]                                |  false  |
| BDFR_USER        | The user to run-as when running an authenticated session                                           |         |
| BDFR_VERBOSE     | Verbosity of BDFR logging. 0=INFO, 1=DEBUG, 2=FULL                                                 |    0    |
| BDFR_NODUPES     | Will not redownload files if they already exist somewhere in the download folder tree [true/false] |   true  |
| BDFR_SORT        | Downloads based on Reddit sort type. Options: controversial, hot, new, rising, top                 |   new   |
| BDFR_DETOX       | Whether to run detox to clean-up filenames [true/false]                                            |  false  |
| BDFR_RDFIND      | Whether to run rdfind to replace duplicate files [true/false]                                      |  false  |
| BDFR_RDFIND_OPTS | Use these options when running rdfind. Default action if empty: convert duplicates to symlinks     |         |
| BDFR_SYMLINKS    | Whether to run symlinks to change absolute/messy links to relative [true/false]                    |  false  |


## Setup

1. rename `options.yaml.example` -> `options.yaml`
1. rename `default_config.cfg` -> `config.cfg`
2. modify and put in a directory (will be volume mounted)
3. choose a download directory (will be volume mounted)
4. `docker run --name bdfr -v your/download/location:/downloads -v your/config/directory/containing/optionsyaml:/config overbyrn/docker-bdfr`
