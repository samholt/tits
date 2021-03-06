### Makefile.am
include $(top_builddir)/version.mk

AM_CFLAGS = $(EXTRA_CFLAGS)
AM_CPPFLAGS = -D_POSIX_C_SOURCE=201001L -D_XOPEN_SOURCE=700 -D_BSD_SOURCE
AM_LDFLAGS = $(XCCLDFLAGS)

bin_PROGRAMS =
noinst_PROGRAMS =
lib_LTLIBRARIES =
noinst_LTLIBRARIES =
pkglib_LTLIBRARIES =
noinst_HEADERS =
BUILT_SOURCES =
EXTRA_DIST = $(BUILT_SOURCES)
CLEANFILES = 
SUFFIXES =

CLEANFILES += version.c
EXTRA_DIST += version.c.in

noinst_LTLIBRARIES += libtits.la
libtits_la_SOURCES = tits.h
libtits_la_SOURCES += nifty.h
libtits_la_SOURCES += hash.c hash.h
libtits_la_SOURCES += norm.c norm.h
libtits_la_SOURCES += xcor.c xcor.h
libtits_la_SOURCES += sacf.c sacf.h
libtits_la_SOURCES += perio.c perio.h
libtits_la_SOURCES += acf24ar.c acf24ar.h
libtits_la_SOURCES += roots.c roots.h
libtits_la_SOURCES += version.c version.h
libtits_la_LDFLAGS = $(AM_LDFLAGS)
libtits_la_LDFLAGS += -lm
EXTRA_libtits_la_DEPENDENCIES = $(LTDLDEPS)

if HAVE_STRTOD32
noinst_PROGRAMS += guess_lag
guess_lag_SOURCES = guess_lag.c guess_lag.yuck
guess_lag_CPPFLAGS = $(AM_CPPFLAGS)
guess_lag_CPPFLAGS += -DSTANDALONE
guess_lag_CPPFLAGS += $(dfp754_CFLAGS)
guess_lag_LDFLAGS = $(AM_LDFLAGS)
guess_lag_LDFLAGS += $(dfp754_LIBS)
guess_lag_LDADD = libtits.la
BUILT_SOURCES += guess_lag.yucc
endif  ## HAVE_STRTOD32

noinst_PROGRAMS += roots
roots_SOURCES = roots.c roots.yuck
roots_CPPFLAGS = $(AM_CPPFLAGS)
roots_CPPFLAGS += -DSTANDALONE
roots_LDADD = libtits.la
BUILT_SOURCES += roots.yucc


## version rules
version.c: version.c.in $(top_builddir)/.version
	$(AM_V_GEN) PATH="$(top_builddir)/build-aux:$${PATH}" \
		yuck$(EXEEXT) scmver --ignore-noscm --force -o $@ \
			--use-reference --reference $(top_builddir)/.version $<

## yuck rule
SUFFIXES += .yuck
SUFFIXES += .yucc
.yuck.yucc:
	$(AM_V_GEN) PATH=$(top_builddir)/build-aux:"$${PATH}" \
		yuck$(EXEEXT) gen -o $@ $<

## Create preprocessor output (debugging purposes only)
.c.i:
	$(COMPILE) -E -o $@ $<

## Create assembler output (debugging purposes only)
.c.s:
	$(COMPILE) -S -c $(AM_CFLAGS) $<
