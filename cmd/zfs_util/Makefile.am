include $(top_srcdir)/config/Rules.am

AUTOMAKE_OPTIONS = subdir-objects

DEFAULT_INCLUDES += \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/lib/libspl/include

sbin_PROGRAMS = zfs.util

zfs_util_SOURCES = \
	zfs_util.c

zfs_util_LDADD = \
        $(top_builddir)/lib/libzfs/libzfs.la

zfs_util_LDFLAGS = -static -framework IOKit -lcurl

install-exec-hook:
	mkdir -p $(DESTDIR)/@FILESYSTEMS_PREFIX@/zfs.fs/Contents/Resources
	/bin/ln -f $(DESTDIR)$(sbindir)/zfs.util $(DESTDIR)/@FILESYSTEMS_PREFIX@/zfs.fs/Contents/Resources/zfs.util
	/bin/ln -fs Contents/Resources/zfs.util $(DESTDIR)/@FILESYSTEMS_PREFIX@/zfs.fs/zfs.util
	chown -R root:wheel ${DESTDIR}/@FILESYSTEMS_PREFIX@/zfs.fs || echo "Unable to chown root:wheel ${DESTDIR}/@FILESYSTEMS_PREFIX@/zfs.fs"

uninstall-hook:
	-$(RM) $(DESTDIR)/@FILESYSTEMS_PREFIX@/zfs.fs/Contents/Resources/zfs.util
	-$(RM) $(DESTDIR)/@FILESYSTEMS_PREFIX@/zfs.fs/zfs.util
