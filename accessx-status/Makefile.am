SUBDIRS = docs pixmaps

INCLUDES = \
	$(GNOME_APPLETS3_CFLAGS) \
	-DACCESSX_PIXMAPS_DIR=\""$(datadir)/pixmaps/accessx-status-applet"\" \
	-DACCESSX_MENU_UI_DIR=\""$(uidir)"\"

libexec_PROGRAMS = accessx-status-applet

accessx_status_applet_SOURCES = \
	applet.c \
	applet.h

accessx_status_applet_LDADD = \
	$(GNOME_APPLETS3_LIBS) \
        $(X_LIBS)

appletdir       = $(datadir)/gnome-panel/applets
applet_in_files = org.gnome.applets.AccessxStatusApplet.panel-applet.in
applet_DATA     = $(applet_in_files:.panel-applet.in=.panel-applet)

$(applet_in_files): $(applet_in_files).in Makefile
	$(AM_V_GEN)sed \
            -e "s|\@LIBEXECDIR\@|$(libexecdir)|" \
            -e "s|\@VERSION\@|$(PACKAGE_VERSION)|" \
            $< > $@

%.panel-applet: %.panel-applet.in $(INTLTOOL_MERGE) $(wildcard $(top_srcdir)/po/*po) ; $(INTLTOOL_MERGE) $(top_srcdir)/po $< $@ -d -u -c $(top_builddir)/po/.intltool-merge-cache

servicedir       = $(datadir)/dbus-1/services
service_in_files = org.gnome.panel.applet.AccessxStatusAppletFactory.service.in
service_DATA     = $(service_in_files:.service.in=.service)

org.gnome.panel.applet.AccessxStatusAppletFactory.service: $(service_in_files)
	$(AM_V_GEN)sed \
            -e "s|\@LIBEXECDIR\@|$(libexecdir)|" \
            $< > $@

uidir   = $(datadir)/gnome-2.0/ui
ui_DATA = accessx-status-applet-menu.xml

CLEANFILES = $(applet_DATA) $(applet_DATA).in $(service_DATA) $(ACCESSX_STATUS_APPLET_CLEANFILES)

EXTRA_DIST = \
	org.gnome.applets.AccessxStatusApplet.panel-applet.in.in \
	$(service_in_files) \
	$(ui_DATA)


-include $(top_srcdir)/git.mk
