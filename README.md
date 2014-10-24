# libiconv

libiconv is a character set conversion library from
[http://ftp.gnu.org/pub/gnu/libiconv/](http://ftp.gnu.org/pub/gnu/libiconv/)

PHP(MSVC) currently uses 1.14 released 2011.08.07

libiconv development has been moved to [https://savannah.gnu.org/projects/libi
conv/](https://savannah.gnu.org/projects/libiconv/)

Because iconv.exe is GPL licensed, the author has decided to drop support for
building on msvc altogether, because building on newer compilers that require
separate distributions of MS runtimes might cause gpl violations (you can
simply point people to the runtime installers provided by microsoft and not
include them with the program…but that's another story). However, libiconv is
lgpl and does not have these restrictions, the versions on php.net are
compiled with Microsoft compilers with a small patch to fix compiler warnings
and errors.

If someone has the time or energy the patch should probably be sent upstream
to the bugs list.

# Building for PHP(MSVC)

The solution has static and dll projects. Both of them have to be built in
debug and release mode. The binaries have to be put into the deps tree with
the following structure:
	include:
		iconv.h

    Dynamic:
		Macro: #define LIBICONV_DLL
		Debug:
			lib: iconvD.lib
			dll: iconvD.dll
			pdb: iconvD.pdb
		Release:
			lib: iconv.lib
			dll: iconv.dll
			pdb: iconv.pdb
	
	Static:
		Debug:
			lib: iconvSD.lib
			pdb: iconvSD.pdb
		Release:
			lib: iconvS.lib
			pdb: iconvS.pdb
				 
After this the iconv PHP(MSVC) extension can be built static or shared.
