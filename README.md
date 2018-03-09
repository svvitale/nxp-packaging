# nxp-packaging

A template for NXP packaging of the NFC-EXPLORE Reader Library for Linux.  This repo does *NOT* contain the reader library itself, it's merely a place to collaborate on the packaging structure for the library.

## DEBIAN/config

This is where we ask the user to accept the license agreement.  The installation will exit and an error message will be displayed if the user chooses not to accept the agreement.

## Using this template

To build a `.deb` package using this template:

1. Extract the contents of the `sw3693-ARCHIVED.zip` file into `usr/local/src/nxprdlib`
1. Run `dpkg-deb --build nxp-packaging/ nxprdlib.deb` to generate the `nxprdlib.deb` file
1. Install the package using `sudo dpkg -i nxprdlib.deb`
1. After installation, source files can be found in `/usr/local/src/nxprdlib` and compiled static libraries can be found in `/usr/local/lib/nxprdlib`

## Development Tips

`debconf` is used to prompt the user for license acceptance.  To clear the database of debconf question responses, this command comes in handy:
`sudo echo PURGE | sudo debconf-communicate nxprdlib`

Installing the package after it's built can be done with `sudo dpkg -i nxprdlib.deb`.

Removing the package after it's installed can be done with `sudo dpkg --remove nxprdlib`.

## Resources

https://www.leaseweb.com/labs/2013/06/creating-custom-debian-packages/

http://www.fifi.org/doc/debconf-doc/tutorial.html

http://manpages.ubuntu.com/manpages/trusty/man7/debconf-devel.7.html
