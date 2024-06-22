# Photocopy

Copies or moves JPEG images from one location to another


## Description

The script `photocopy` transfers JPEG images from the source directory _srcdir_ to the output directory _outdir_.  Image files can be *copied*, *moved* or *converted*.

The script can be used to transfer images from a photo camera to a local image repository or to upload the most recent images from a local image repository to a remote location.  For the latter, `photocopy` can be configured to automatically remove images from the remote location that exceed a certain threshold.

Files at the output location will be renamed to a unique filename based upon the EXIF original timestamp of the source file.

### Warning

It is recommended to reserve the output directory _outdir_ exclusively for `photocopy` and not to use it for any other purpose, especially when the option **limitmode** is enabled.  If the latter is true, unregistered files in _outdir_ matching the same file extension will be removed.  It is recommended to enable **dryrun** to see what would happen.


## Synopsis

```console
$ photocopy [OPTION]...
```

The script can be invoked using zero, one or two arguments.

+ If it is invoked using *two* arguments, the first argument holds the source directory _srcdir_ and the second argument holds the output directory _outdir_.

+ If it is invoked using *one* argument and this argument is an existing *directory*, it is assigned as output directory _outdir_.  The current working directory is assumed to be the source directory _srcdir_.

+ If it is invoked using *one* argument and this argument is an existing *file*, it is used as configuration file containing options as key-value-pairs.  Additional command line options will override the settings in the configuration file.

+ If it is invoked using *one* argument and this argument is a *string*, it is used as a basename for a configuration file with the file extension `.rc`.  This file needs to reside in the directory `~/.photocopy`.  Additional command line options will override the settings in the configuration file.



## Options

+ **srcdir** = _folder_

    Specifies the name of the source directory.  The source directory must exist and the user must have read permission.

+ **outdir** = _folder_

    Specifies the name of the output directory.  The output directory must exist and the user must have write permission.

+ **action** = _string_

    Specifies the transfer action.  Valid values are `cp` for copying, `mv` for moving and `cv` for converting.

+ **cachefile** = _filename_

    Specifies the name of the cachefile.

+ **cvopt** = _string_

    Adds ImageMagick options when **action** is `cv` for converting.

+ **dirdepth** = _integer_

    Sets number of subfolders within directory _outdir_.  Valid values are `1`, `2` and `3`.

+ **dirfmt1** | **dirfmt2** | **dirfmt3** = _string_

    Use `strftime` flags to label subfolders in directory _outdir_.  The default setting is `%Y` for subfolder 1, `%m` for subfolder 2 and `%d` for subfolder 3.

+ **limitmode** = _string_

    Activates flag to limit files at directory _outdir_.  Use `none` (default) to disable this option.  If set, this option requires **limitcount** being set to a positive value.  The following modes are available:

    + `num`

        Limits the number of image files to the most recent ones.

    + `date`

        Removes images when their EXIF datetime is older than a certain amount of days from today.

    + `uptime`

        Removes images after a certain amount of days of being uploaded.

+ **limitcount** = _integer_

    Adds threshold value for **limitmode**.  The default is `0`.

+ **outext** = _string_

    Specifies the format of the images at the output directory.  The default is `JPG`.

+ **recurse**

    Recurses into all subfolders of the source directory.

+  **dryrun**

    Does not change the file system.  Only simulates what would be done.

+  **progress**

    Enables or disables the use of a progress bar.  Default is enabled.

+  **help**

    Prints a brief help message and exits.


## Requirements

+ [Date::Parse](https://metacpan.org/pod/Date::Parse)
+ [File::HomeDir](https://metacpan.org/pod/File::HomeDir)
+ [File::Slurp](https://metacpan.org/pod/File::Slurp)
+ [Image::Magick](https://metacpan.org/pod/Image::Magick)
+ [Regexp::Common](https://metacpan.org/pod/Regexp::Common)


## Installation

Use the following command to install this software:

```console
$ make
$ make install
```

The default `PREFIX` is set to `/usr/local`.  In order to successfully complete the installation, you need to have write permissions for the installation location.


## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.


## License

[MIT](https://choosealicense.com/licenses/mit/)
