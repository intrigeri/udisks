## Process this file with automake to produce Makefile.in

SUBDIRS = data

BCACHE_MODULE_DIR = $(top_srcdir)/modules/bcache

MODULE_SO = libudisks2_bcache.so

NULL =

CPPFLAGS =                                                                    \
	-I$(top_builddir) -I$(top_srcdir)                                     \
	-DPACKAGE_LIBEXEC_DIR=\""$(libexecdir)"\"                             \
	-DPACKAGE_SYSCONF_DIR=\""$(sysconfdir)"\"                             \
	-DPACKAGE_DATA_DIR=\""$(datadir)"\"                                   \
	-DPACKAGE_BIN_DIR=\""$(bindir)"\"                                     \
	-DPACKAGE_LOCALSTATE_DIR=\""$(localstatedir)"\"                       \
	-DPACKAGE_LOCALE_DIR=\""$(localedir)"\"                               \
	-DPACKAGE_LIB_DIR=\""$(libdir)"\"                                     \
	-DLVM_HELPER_DIR=\""$(prefix)/lib/udisks2/"\"                         \
	-D_POSIX_PTHREAD_SEMANTICS -D_REENTRANT                               \
	-DUDISKS_COMPILATION                                                  \
	$(POLKIT_GOBJECT_1_CFLAGS)                                            \
	$(GLIB_CFLAGS)                                                        \
	$(GIO_CFLAGS)                                                         \
	$(GUDEV_CFLAGS)                                                       \
	$(BLOCKDEV_CFLAGS)                                                    \
	$(WARN_CFLAGS)                                                        \
	$(NULL)

$(dbus_built_sources): $(BCACHE_MODULE_DIR)/data/org.freedesktop.UDisks2.bcache.xml Makefile.am
	$(AM_V_GEN) gdbus-codegen                                             \
	        --interface-prefix org.freedesktop.UDisks2.                   \
	        --c-namespace UDisks                                          \
	        --generate-c-code udisks-bcache-generated                     \
	        --generate-docbook udisks-generated-doc                       \
	        $<

dbus_built_sources =                                                          \
	udisks-bcache-generated.h	udisks-bcache-generated.c             \
	$(NULL)

BUILT_SOURCES =                                                               \
	$(dbus_built_sources)                                                 \
	$(NULL)

libudisks2_bcachedir=$(libdir)/udisks2/modules
libudisks2_bcache_LTLIBRARIES=libudisks2_bcache.la

libudisks2_bcacheincludedir=$(includedir)/udisks2/udisks

libudisks2_bcacheinclude_HEADERS =                                            \
	$(top_srcdir)/modules/udisksmoduleiface.h                             \
	$(top_srcdir)/modules/udisksmoduleifacetypes.h                        \
	$(top_srcdir)/modules/udisksmoduleobject.h                            \
	$(NULL)

libudisks2_bcache_la_SOURCES =                                                \
	$(BUILT_SOURCES)                                                      \
	$(top_srcdir)/modules/udisksmoduleiface.h                             \
	$(top_srcdir)/modules/udisksmoduleifacetypes.h                        \
	$(top_srcdir)/modules/udisksmoduleobject.h                            \
	$(top_srcdir)/modules/udisksmoduleobject.c                            \
	udiskslinuxblockbcache.c                                              \
	udiskslinuxblockbcache.h                                              \
	udiskslinuxmanagerbcache.h                                            \
	udiskslinuxmanagerbcache.c                                            \
	udisksbcachemoduleiface.c                                             \
	udisksbcachestate.h                                                   \
	udisksbcachestate.c                                                   \
	udisksbcachetypes.h                                                   \
	udisksbcacheutil.c                                                    \
	udisksbcacheutil.h                                                    \
	$(NULL)

libudisks2_bcache_la_CPPFLAGS =                                               \
	$(CPPFLAGS)                                                           \
	-DG_LOG_DOMAIN=\"libudisks2-bcache\"                                  \
	$(NULL)

libudisks2_bcache_la_CFLAGS =                                                 \
	$(GLIB_CFLAGS)                                                        \
	$(GIO_CFLAGS)                                                         \
	$(GUDEV_CFLAGS)                                                       \
	$(POLKIT_GOBJECT_1_CFLAGS)                                            \
	$(BLOCKDEV_CFLAGS)                                                    \
	$(NULL)

libudisks2_bcache_la_LDFLAGS =                                                \
	-export_dynamic                                                       \
	-avoid-version                                                        \
	-module                                                               \
	-no-undefined                                                         \
	-export-symbols-regex                                                 \
	 '^udisks_.*|g_io_module_load|g_io_module_unload|g_io_module_query'   \
	$(NULL)

libudisks2_bcache_la_LIBADD =                                                 \
	$(GLIB_LIBS)                                                          \
	$(GIO_LIBS)                                                           \
	$(GUDEV_LIBS)                                                         \
	$(POLKIT_GOBJECT_1_LIBS)                                              \
	$(BLOCKDEV_LIBS)                                                      \
	$(NULL)

# ------------------------------------------------------------------------------

CLEANFILES = udisks-generated-doc-*.xml udisks-generated.[ch]

EXTRA_DIST =                                                                  \
	$(NULL)

include ../Makefile.uninstalled

all-local: module_link

dist-hook:
	(for i in $(BUILT_SOURCES); do rm -f $(distdir)/$$i; done)

clean-local: module_unlink
	rm -f *~ $(BUILT_SOURCES)
