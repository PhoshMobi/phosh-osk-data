.. _phosh-osk-data-packager(1):

=======================
phosh-osk-data-packager
=======================

-----------------------------
Download and package OSK data
-----------------------------

SYNOPSIS
--------
|   **phosh-osk-data-packager** [OPTIONS...]


DESCRIPTION
-----------

``phosh-osk-data-packager`` downloads and packages data for Phosh's on screen
keyboards (OSKs). It currently supports downloading and packaging data
for completion using the presage library.

OPTIONS
-------

``-h``, ``--help``
   Print help and exit

``--language=LANGUAGE``
   The language code of the language to process. E.g. `de` or `se`.

``--engine=ENGINE``
   The completion engine to download data for. The only currently supported
   engine is `presage` using it's sqlite backend.

``--pkg=FORMAT``
   The packaging format to build a package for. The only currently supported
   format is `deb` building a package for Debian based distributions.

``--install``
   Whether to install the package

EXAMPLE
-------

This downloads and packages data for Swedish and puts the resulting package
into the current directory:

::

    ./phosh-osk-data-packager --language=se


See also
--------

``phosh-osk-stevia(1)``
