AC_INIT([async-process], [0.1])
AC_CONFIG_HEADERS([config.h])

# Set default prefix based on platform if not specified
AC_PREFIX_DEFAULT([/usr/local])

AM_INIT_AUTOMAKE([foreign subdir-objects])

# Add option for static builds
AC_ARG_ENABLE([static],
  [AS_HELP_STRING([--enable-static], [build static library (default: no)])],
  [enable_static=$enableval],
  [enable_static=no])

# Add option for shared builds
AC_ARG_ENABLE([shared],
  [AS_HELP_STRING([--enable-shared], [build shared library (default: yes)])],
  [enable_shared=$enableval],
  [enable_shared=yes])

# Initialize libtool with the options
AS_IF([test "$enable_static" = "yes" && test "$enable_shared" = "no"],
  [LT_INIT([win32-dll disable-shared])],
  [test "$enable_static" = "yes" && test "$enable_shared" = "yes"],
  [LT_INIT([win32-dll])],
  [LT_INIT([shared win32-dll disable-static])])

AC_PROG_CC

# Platform-specific configuration
AC_CANONICAL_HOST
case $host_os in
  freebsd*)
    # FreeBSD typically uses /usr/local
    test "$prefix" = NONE && prefix=/usr/local
    ;;
  darwin*)
    # macOS typically uses /usr/local
    test "$prefix" = NONE && prefix=/usr/local
    ;;
  linux*)
    # Linux typically uses /usr/local for user-installed software
    test "$prefix" = NONE && prefix=/usr/local
    ;;
esac

AC_CHECK_HEADERS([fcntl.h stdlib.h string.h unistd.h windows.h])

AC_CHECK_HEADER_STDBOOL
AC_TYPE_PID_T

AC_FUNC_FORK
AC_FUNC_MALLOC
AC_CHECK_FUNCS([dup2 strerror])

AC_CONFIG_FILES([Makefile])
AC_OUTPUT

# Print configuration summary
AC_MSG_NOTICE([
  async-process configuration summary:

  Installation prefix: $prefix
  Library directory:   $libdir
  Include directory:   $includedir
  C Compiler:          $CC
  Host system:         $host_os
  Build shared:        $enable_shared
  Build static:        $enable_static

  Note: This C library is for Unix-like systems only (Linux, FreeBSD, macOS).
  Windows support is provided via pure Lisp CFFI implementation and does not
  require C compilation.

  You can now run 'make' to build the library.
  After building, run 'make install' to install to the prefix.

  To install to a different location, reconfigure with:
    ./configure --prefix=/your/custom/path

  To build static library:
    ./configure --enable-static

  To build only static (no shared):
    ./configure --enable-static --disable-shared
])
