ACLOCAL_AMFLAGS = -I m4

lib_LTLIBRARIES = libasyncprocess.la
libasyncprocess_la_LDFLAGS = -version-info 0:0:0 -no-undefined
libasyncprocess_la_SOURCES = src/async-process.c

include_HEADERS = src/async-process.h

# Don't install .la files and remove full version number
install-exec-hook:
	rm -f $(DESTDIR)$(libdir)/libasyncprocess.la
	@if [ -f $(DESTDIR)$(libdir)/libasyncprocess.so.0.0.0 ]; then \
		cp -f $(DESTDIR)$(libdir)/libasyncprocess.so.0.0.0 $(DESTDIR)$(libdir)/libasyncprocess.so.0.tmp; \
		rm -f $(DESTDIR)$(libdir)/libasyncprocess.so.0.0.0 $(DESTDIR)$(libdir)/libasyncprocess.so.0 $(DESTDIR)$(libdir)/libasyncprocess.so; \
		mv $(DESTDIR)$(libdir)/libasyncprocess.so.0.tmp $(DESTDIR)$(libdir)/libasyncprocess.so.0; \
		ln -s libasyncprocess.so.0 $(DESTDIR)$(libdir)/libasyncprocess.so; \
		echo "Removed versioned file and created libasyncprocess.so.0"; \
	fi
