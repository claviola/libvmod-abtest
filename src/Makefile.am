
AM_CPPFLAGS = @VMOD_INCLUDES@ -Wall -Werror

vmoddir = @VMOD_DIR@
vmod_LTLIBRARIES = libvmod_abtest.la

libvmod_abtest_la_LDFLAGS = -module -export-dynamic -avoid-version -shared

libvmod_abtest_la_SOURCES = \
	vmod_abtest.c

nodist_libvmod_abtest_la_SOURCES = \
	vcc_if.c \
	vcc_if.h

vmod_abtest.lo: vcc_if.c vcc_if.h

vcc_if.c: vcc_if.h

vcc_if.h: @VMODTOOL@ $(top_srcdir)/src/vmod_abtest.vcc
	@VMODTOOL@ $(top_srcdir)/src/vmod_abtest.vcc

VMOD_TESTS = $(top_srcdir)/src/tests/*.vtc
.PHONY: $(VMOD_TESTS)

$(top_srcdir)/src/tests/*.vtc: libvmod_abtest.la
	@VARNISHTEST@ -Dvarnishd=@VARNISHD@ -Dvmod_topbuild=$(abs_top_builddir) $@

check: $(VMOD_TESTS)

EXTRA_DIST = \
	vmod_abtest.vcc \
	$(VMOD_TESTS)

CLEANFILES = \
	$(builddir)/vcc_if.c \
	$(builddir)/vcc_if.h \
	$(builddir)/vmod_abtest.rst \
	$(builddir)/vmod_abtest.man.rst
