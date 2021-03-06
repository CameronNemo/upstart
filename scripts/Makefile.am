## Process this file with automake to produce Makefile.in

UPSTART_BINARY = $(abs_top_builddir)/init/startup
INITCTL_BINARY = $(abs_top_builddir)/util/initctl
FILE_BRIDGE_BINARY = $(abs_top_builddir)/extra/file

desktopdir = $(datadir)/applications
desktop_DATA = data/startup-monitor.desktop

icondir = $(datadir)/icons/hicolor/scalable/apps
icon_DATA = data/startup-monitor.svg

install_scripts = \
	initctl2dot.py \
	init-checkconf.sh \
	startup-monitor.py

noinst_SCRIPTS = \
	pyupstart.py \
	pyupstartvars.py

CLEANFILES = \
	pyupstartvars.py pyupstartvars.py.tmp

EXTRA_DIST = \
	$(install_scripts) \
	$(desktop_DATA) \
	$(icon_DATA) \
	pyupstart.py \
	tests/__init__.py \
	tests/test_pyupstart_session_init.py \
	tests/test_pyupstart_system_init.py

pyupstartvars.py: Makefile
	echo "BUILT_UPSTART = '$(UPSTART_BINARY)'" > pyupstartvars.py.tmp
	echo "BUILT_INITCTL = '$(INITCTL_BINARY)'" >> pyupstartvars.py.tmp
	echo "BUILT_FILE_BRIDGE = '$(FILE_BRIDGE_BINARY)'" >> pyupstartvars.py.tmp
	mv pyupstartvars.py.tmp pyupstartvars.py

dist_man_MANS = \
  man/initctl2dot.8 \
  man/init-checkconf.8 \
  man/startup-monitor.8

install-exec-hook: $(install_scripts)
	[ ! -d "$(DESTDIR)/$(bindir)" ] && mkdir -p "$(DESTDIR)/$(bindir)"; \
	for file in $(install_scripts); do \
		from=`echo "$$file" | sed '$(transform)'`; \
		to=`basename $$from | cut -d. -f1`; \
		echo "  cp '$(srcdir)/$$from' '$(DESTDIR)$(bindir)/$$to'"; \
		cp "$(srcdir)/$$from" "$(DESTDIR)$(bindir)/$$to"; \
	done

uninstall-hook:
	for file in $(install_scripts); do \
		inst=`basename $$file | cut -d. -f1`; \
		echo "  rm -f '$(DESTDIR)$(bindir)/$$inst'"; \
		rm -f "$(DESTDIR)$(bindir)/$$inst"; \
	done
