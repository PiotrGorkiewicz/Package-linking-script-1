Package linking script #1

Document version 1.0


The simple bash script for GNU/Linux to let run and manage experimental packages without installing them normal way.

The script is intended for those who compile and use packages (often experimental) outside of the packet control mechanism.
Usually, /usr/local/ is chosen as the installation location, because there are predefined paths to /usr/local/bin/, /usr/local/lib/, etc. in the system.
The package installed (scattered over /usr/local/) is difficult to manage later, in particular, to delete it.
The idea is to install the package in a directory dedicated only to it, and then to create a set of links in the /usr/local/ structure so that the binaries, libraries and package manuals are system-wide visible.
The script has been working for years in subsequent releases of Slackware.

To use the script you must do:
1. Prepare the system so that the /usr/local/ directory is empty, even without empty subdirectories.
2. Copy the downloaded file structure as root to your filesystem (in particular the contents of the /opt/ directory).
3. When you compile your Foo package, configure it (eg with the 'destdir' parameter) so that its installation place is the /opt/linked/Foo/ directory.
After executing a sequence of configuration, compilation and installation commands (usually respectively configure, make, make install), the following directories will appear: /opt/linked/Foo/bin/, /opt/linked/Foo/lib/, /opt/linked/Foo/lib64/, /opt/linked/Foo/man/, etc.
4. The Foo package is not yet ready to be run in the sysytem. To make it ready, go (as root) to the /opt/manually_run/ directory and run link_all.
5. If everything went well, subdirectories filled with links to the binaries and Foo packet libraries appeared in the /usr/local/ directory.
6. Proceed similarly with subsequent packages. After installing each package, execute the link_all script, in particular if the next package depends on the libraries of the previous package.
7. You can now easily remove or replace the Bar package by deleting or moving the directory /opt/linked/Bar/ outside the /opt/linked/ directory. After each manipulation, execute the link_all script.
8. The script ignores all directories named HIDDEN if they are inside the /opt/linked/ directory. I keep the source of packages in such places.

Known issues:
Packages containing Python are a problem. Python does not understand the links if they are inside .../site-packages/

