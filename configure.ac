#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.71])
AC_INIT([libg15],[3.0.1],[menelkir@itroll.org])
AC_PREFIX_DEFAULT(/usr)
AC_CONFIG_AUX_DIR(config)
AC_CANONICAL_TARGET()
AC_CONFIG_MACRO_DIRS([m4])

AM_INIT_AUTOMAKE()
AC_CONFIG_SRCDIR([libg15.c])
AC_CONFIG_HEADERS([config.h])

# Checks for programs.
AC_PROG_CC
LT_INIT

case $host_os in
	*linux*) 
	  AC_DEFINE([OSTYPE_LINUX], [1],[Target OS is Linux])
	  ;;
	*darwin*)
	  AC_DEFINE([OSTYPE_DARWIN], [1],[Target OS is Darwin])
	  ;;
	*freebsd*)
	  AC_DEFINE([OSTYPE_FREEBSD], [1],[Target OS is FreeBSD])
	  ;;
        *solaris*)
          AC_DEFINE([OSTYPE_SOLARIS], [1],[Target OS is Solaris])
	  AC_SEARCH_LIBS([nanosleep],rt,[],[],[])
          AC_DEFINE(SUN_LIBUSB, 1, [Define to 1 for Sun version of libusb.])
	  libusb_blocks=true	  
	  ;;
esac

# Checks for libraries.
AC_CHECK_LIB([usb], [main], ,AC_MSG_ERROR(["libusb not found. please install it"]))

dnl Some versions of libusb do not honour timeout and block. Suns' version is one of them.
if test "x$libusb_blocks" == "xtrue"; then
      AC_DEFINE([LIBUSB_BLOCKS], [1],[Define if libusb implementation blocks on read or write])
fi

# Checks for header files.
AC_CHECK_INCLUDES_DEFAULT
AC_PROG_EGREP

AC_CHECK_HEADERS([string.h])
AC_CHECK_HEADERS([usb.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST

# Checks for library functions.
AC_CHECK_FUNCS([memset])

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
