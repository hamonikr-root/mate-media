NULL =

SUBDIRS = po man

if HAVE_SOUND_THEME
SUBDIRS += sound-theme
endif

if HAVE_PULSEAUDIO
SUBDIRS += mate-volume-control
endif

if HAVE_GSTMIXER
SUBDIRS += gst-mixer
endif

if HAVE_GSTMIXER_APPLET
SUBDIRS += gst-mixer-applet
endif

DISTCHECK_CONFIGURE_FLAGS = \
	--disable-scrollkeeper	\
	--enable-more-warnings  \
	--enable-compile-warnings=maximum \
	--enable-deprecated 

DIST_SUBDIRS = \
	po 			\
	man			\
	mate-volume-control	\
	gst-mixer		\
	gst-mixer-applet	\
	sound-theme		\
	$(NULL)

EXTRA_DIST = \
	.version		\
	autogen.sh		\
	configure		\
	ChangeLog		\
	COPYING			\
	COPYING-DOCS		\
	COPYING.gst-mixer	\
	build-aux/git-version-gen \
	$(INTLTOOL_BUILT:=.in)	\
	$(NULL)

DISTCLEANFILES = \
	build-aux/mate-doc-utils.make	\
	po/.intltool-merge-cache	\
	$(NULL)

ACLOCAL_AMFLAGS = -I m4 ${ACLOCAL_FLAGS}

# see build-aux/git-version-get for details
BUILT_SOURCES = $(top_srcdir)/.version
$(top_srcdir)/.version:
	echo $(VERSION) > $@-t && mv $@-t $@
dist-hook:
	echo $(VERSION) > $(distdir)/.tarball-version

	@if test -d "$(srcdir)/.git"; \
	then \
		echo Creating ChangeLog && \
		( cd "$(top_srcdir)" && \
		  echo '# Generated by Makefile. Do not edit.'; echo; \
		  $(top_srcdir)/build-aux/missing --run git log --stat ) > ChangeLog.tmp \
		&& mv -f ChangeLog.tmp $(distdir)/ChangeLog \
		|| ( rm -f ChangeLog.tmp ; \
		echo Failed to generate ChangeLog >&2 ); \
	else \
		echo A git clone is required to generate a ChangeLog >&2; \
	fi

-include $(top_srcdir)/git.mk
