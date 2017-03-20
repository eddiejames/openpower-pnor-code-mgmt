AC_PREREQ([2.69])
AC_INIT([openpower-pnor-code-mgmt], [1.0], [https://github.com/openbmc/openpower-pnor-code-mgmt/issues])
AC_LANG([C++])
AC_CONFIG_HEADERS([config.h])
AM_INIT_AUTOMAKE([subdir-objects -Wall -Werror foreign dist-xz])
AM_SILENT_RULES([yes])

# Checks for programs
AC_PROG_CXX
AC_PROG_INSTALL #Checks/sets the install variable to be used
AC_PROG_MAKE_SET

# Check for libraries
PKG_CHECK_MODULES([PHOSPHOR_DBUS_INTERFACES], [phosphor-dbus-interfaces],,\
    AC_MSG_ERROR(["Requires phosphor-dbus-interfaces package."]))
PKG_CHECK_MODULES([SDBUSPLUS], [sdbusplus],,
    AC_MSG_ERROR(["Requires sdbusplus package."]))
PKG_CHECK_MODULES([PHOSPHOR_LOGGING], [phosphor-logging],,
    [AC_MSG_ERROR([The openbmc/phosphor-logging package is required])])

# Checks for library functions
LT_INIT # Required for systemd linking

# Checks for typedefs, structures, and compiler characteristics.
AX_CXX_COMPILE_STDCXX_14([noext])
AX_APPEND_COMPILE_FLAGS([-Wall -Werror], [CXXFLAGS])

AC_ARG_VAR(VERSION_BUSNAME, [The Dbus busname to own])
AS_IF([test "x$VERSION_BUSNAME" == "x"],
    [VERSION_BUSNAME="org.open_power.Software.Host.Version"])
AC_DEFINE_UNQUOTED([VERSION_BUSNAME], ["$VERSION_BUSNAME"], [The DBus busname to own])

AC_ARG_VAR(SOFTWARE_OBJPATH, [The software manager Dbus root])
AS_IF([test "x$SOFTWARE_OBJPATH" == "x"], [SOFTWARE_OBJPATH="/xyz/openbmc_project/software"])
AC_DEFINE_UNQUOTED([SOFTWARE_OBJPATH], ["$SOFTWARE_OBJPATH"], [The software manager Dbus root])

AC_DEFINE(BUSNAME_UPDATER, "org.open_power.Software.Host.Updater",
    [The item updater DBus busname to own.])

AC_ARG_VAR(TOC_FILE, [The path to the pnor toc file])
AS_IF([test "x$TOC_FILE" == "x"], [TOC_FILE="/tmp/pnor/pnor.toc"])
AC_DEFINE_UNQUOTED([TOC_FILE], ["$TOC_FILE"], [The path to the pnor toc file])

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
