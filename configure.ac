AC_INIT([Hack], [3.0], [https://github.com/source-foundry/Hack/issues], [Hack])
AM_INIT_AUTOMAKE([foreign])

AC_ARG_WITH([fontsdir],
    [AS_HELP_STRING([--with-fontsdir=DIR], [font install root [DATAROOTDIR/fonts/hack]])],
    [fontsdir=$withval],
    [fontsdir="\${datarootdir}/fonts/hack"]
)
AC_SUBST([fontsdir], [$fontsdir])

AC_ARG_WITH([ttfdir],
    [AS_HELP_STRING([--with-ttfdir=DIR], [ttf install path [FONTSDIR]])],
    [ttfdir=$withval],
    [ttfdir="\${fontsdir}"]
)
AC_SUBST([ttfdir], [$ttfdir])

AC_ARG_WITH([hints],
    [AC_HELP_STRING([--with-hints=STYLE], [ttfautohint style (STYLE is one of 'default', 'minimal', 'none')])],
    [hint_style=$withval],
    [hint_style=default]
)
AM_CONDITIONAL([HINT], [test x$hint_style != xnone])
AM_CONDITIONAL([HINT_MINIMAL], [test x$hint_style = xminimal])

AC_CONFIG_FILES([
    Makefile
    src/Makefile
])
AC_OUTPUT
