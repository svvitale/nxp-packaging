# nxp-packaging

A template for NXP packaging of the NFC-EXPLORE Reader Library for Linux.  This repo does *NOT* contain the reader library itself, it's merely a place to collaborate on the packaging structure for the library.

## DEBIAN/config

This is where we ask the user to accept the license agreement.  The installation will exit and an error message will be displayed if the user chooses not to accept the agreement.

## Using this template

To build a `.deb` package using this template:

1. Extract the contents of the `sw3693.zip` file into `usr/local/src/nxprdlib`
1. Run `dpkg-deb --build nxp-packaging/ nxprdlib.deb` to generate the `nxprdlib.deb` file
1. Install the package using `sudo dpkg -i nxprdlib.deb`
1. After installation, source files can be found in `/usr/local/src/nxprdlib` and compiled static libraries can be found in `/usr/local/lib/nxprdlib`

## Known issues

1. The `NfcrdlibEx5_ISO15693` make target does not build and causes the installation to fail. **Workaround:** Remove this target 
from `CMakeLists.txt` prior to building the package.
1. The reader library has significantly changed in the latest version of `sw3693.zip`.  [nxppy](https://github.com/svvitale/nxppy) will need to be updated to use the new
code interfaces and link to the correct static libraries.

## Development Tips

`debconf` is used to prompt the user for license acceptance.  To clear the database of debconf question responses, this command comes in handy:
`sudo echo PURGE | sudo debconf-communicate nxprdlib`

## Resources

https://www.leaseweb.com/labs/2013/06/creating-custom-debian-packages/
http://www.fifi.org/doc/debconf-doc/tutorial.html
http://manpages.ubuntu.com/manpages/trusty/man7/debconf-devel.7.html
