dist_bin_SCRIPTS = loctree3
dist_pkgdata_SCRIPTS = $(srcdir)/loctree2data

docdir = $(datadir)/doc/$(PACKAGE)
dist_doc_DATA = AUTHORS README
dist_pkgdata_DATA = loctree3rc.default

SUBDIRS = examples data

man_MANS = loctree3.1

%.1:	%
	sed -e 's|__pkglibdir__|$(pkglibdir)|g;s|__datadir__|$(datadir)|g;s|__docdir__|$(docdir)|g;s|__pkgdatadir__|$(pkgdatadir)|g;s|__PREFIX__|$(prefix)|g;s|__sysconfdir__|$(sysconfdir)|g;s|__VERSION__|$(VERSION)|g;' "$<" | \
	pod2man -c 'User Commands' -r "$(VERSION)" -name $(shell echo "$(basename $@)" | tr '[:lower:]' '[:upper:]' ) > "$@"

clean-local:
	rm -f $(man_MANS)

install-data-hook:
	sed -i -e 's|__pkglibdir__|$(pkglibdir)|g;s|__datadir__|$(datadir)|g;s|__docdir__|$(docdir)|g;s|__pkgdatadir__|$(pkgdatadir)|g;s|__PREFIX__|$(prefix)|g;s|__sysconfdir__|$(sysconfdir)|g;s|__bindir__|$(bindir)|g;s|__VERSION__|$(VERSION)|g;' "$(DESTDIR)$(pkgdatadir)/loctree3rc.default" "$(DESTDIR)$(pkgdatadir)/loctree2data"

install-exec-hook:
	sed -i -e 's|__pkglibdir__|$(pkglibdir)|g;s|__datadir__|$(datadir)|g;s|__docdir__|$(docdir)|g;s|__pkgdatadir__|$(pkgdatadir)|g;s|__PREFIX__|$(prefix)|g;s|__sysconfdir__|$(sysconfdir)|g;s|__bindir__|$(bindir)|g;s|__VERSION__|$(VERSION)|g;' "$(DESTDIR)$(bindir)/loctree3"
