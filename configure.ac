# Autoconf file for tilda
#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.68])
AC_INIT([Tilda],[1.1.6],[https://github.com/lanoxx/tilda/issues],[tilda],[https://github.com/lanoxx/tilda])
AM_INIT_AUTOMAKE

# We are going to use silent builds which have a much
# nicer output. More information can be foudn here:
#     https://live.gnome.org/GnomeGoals/NicerBuilds
m4_ifdef([AM_SILENT_RULES],[AM_SILENT_RULES([yes])])

AC_CONFIG_SRCDIR([src/tilda.c])
AC_CONFIG_HEADERS([tilda-config.h:tilda-config.h.in])

# This will initialize the internationalization
# capabilities of glib (glib/gi18n.h) and gettext
AM_GNU_GETTEXT_VERSION([0.18.1])
AM_GNU_GETTEXT([external])

# See http://www.gnu.org/savannah-checkouts/gnu/automake/manual/html_node/maintainer_002dmode.html
# for an explanation of using this macro. The short explanation is:
#     AM_MAINTAINER_MODE is bad but
#     AM_MAINTAINER_MODE([enable]) is good
AM_MAINTAINER_MODE([enable])

# This registeres the option '--enable-maintainer-flags' to the ./configure script
# If this option is set then it activates both the '--enable-debug' and '--enable-debug-functions'
# options that are defined below. It also activates several flags to the compile such that it
# will show more warnings and errors to indicate problems in the source code.
AC_ARG_ENABLE([maintainer-flags],
		[AS_HELP_STRING([--enable-maintainer-flags],[enable extra debugging (don't use as user)])])

#' This comment fixes syntax highlighting

if test "x$enable_maintainer_flags" = "xyes"; then
	enable_debug="yes"
	enable_debug_functions="yes"
	CFLAGS="$CFLAGS -Wall -Wextra -pedantic -fno-common -Wstrict-aliasing=2"
	CFLAGS="$CFLAGS -Wshadow -Wmissing-prototypes -Wmissing-declarations"
fi

# This registers the option '--enable-debug' in the ./configure script
# If this option is set, then the the options -g and -ggdb will be
# passed to the compiler.
AC_ARG_ENABLE([debug], [AS_HELP_STRING([--enable-debug],[enable extra debugging output])])

if test "x$enable_debug" = "xyes"; then
	AC_DEFINE([DEBUG], [1], [Enable extra debugging output])
	CFLAGS="$CFLAGS -g -ggdb"
fi

# This registers the option '--debug-functions' in the ./configure script
# If this option is set, then the name of each entered function will be
# printed on the shell.
AC_ARG_ENABLE([debug-functions], [AS_HELP_STRING([--enable-debug-functions],[enable function call tracing])])

if test "x$enable_debug_functions" = "xyes"; then
	AC_DEFINE([DEBUG_FUNCTIONS], [1], [Enable function call tracing])
fi

# Checks for programs.
AC_PROG_CC
AM_PROG_CC_C_O

# Checks for libraries.
PKG_PROG_PKG_CONFIG
PKG_CHECK_MODULES([GTK], [gtk+-3.0 >= 3.0.0])
PKG_CHECK_MODULES([VTE], [vte-2.90])
PKG_CHECK_MODULES([LIBCONFUSE], [libconfuse])

# Checks for header files.
AC_PATH_X
AC_HEADER_STDC
AC_CHECK_HEADERS([fcntl.h malloc.h stdlib.h string.h strings.h sys/ioctl.h unistd.h confuse.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_TYPE_PID_T
AC_TYPE_SIZE_T

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_STRTOD
AC_CHECK_FUNCS([mkdir strcasecmp strchr strncasecmp strstr strtol])

AC_CONFIG_FILES([Makefile
                 src/Makefile
                 m4/Makefile
                 po/Makefile.in])
AC_OUTPUT
