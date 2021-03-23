# globus-utils
Utilities for improving Globus CLI interface for NCAR endpoints

globus-utils is a repository containing a collection of helper-scripts designed to make using the Globus CLI easier with CISL-managed endpoints. At present, two utilities are included:

* gcert
* gci

This version can be used on external systems as well as on Cheyenne and Casper.

## Installation

Simply clone this repository and add the directory to your PATH.

## gcert

`gcert` allows you to convert an InCommon Certificate provided by NCAR CPO into a PEM format that Globus can accept for authentication. You should only need to run gcert once, though if you run it again it will use an existing certifcate to re-activate certain NCAR endpoints.

## gci

`gci`, short for globus command interface, is a utility that identifies and activates NCAR endpoints for you and then forwards commands and arguments to the specified globus subcommand. Coupled with an Incommon certificate, `gci` allows you create unattended dataflows between NCAR endpoints using Globus.

```
Any globus CLI subcommand can be given to this command. Any argument that
specifies an endpoint:path format or simply a path with a known file system
prefix will cause gci to obtain the endpoint ID and activate for you.

gci options:
    --force-auth        force gci to re-authenticate endpoints regardless of status
    --cert-lifetime N   authenticate endpoints for N hours (0<N<=720, default=24)
    --debug             output command with endpoint formatting and exit
    --silent            only output text from the globus command (except errors)

Specifying Endpoints

gci allows you to specify endpoints in two different ways. You may:

1.  Provide the full path for each file - the endpoint will be detected by gci based
    on the path (e.g., /glade/campaign is Campaign Storage). If an unknown absolute
    path is provided, an error will occur.
2.  Explicitly specify the endpoint before the path, separated by a colon. The lowest
    common level will be specified if a relative path is given.

    endpoints:common root
    ---------------------
    glade:/glade
    campaign:/glade/campaign
    share:/glade/p/datashare
    quasar:/gpfs/gpfs0/archive
    id:/path/on/any/filesystem
```
