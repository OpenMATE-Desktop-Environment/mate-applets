
builder_DATA = battstat_applet.ui

ACPIINC= @ACPIINC@

if NEED_LIBAPM
if HAVE_LIBAPM
APMLIB = -lapm
APMDIR =
APMINC = 
else
APMLIB = apmlib/libapm.a
APMDIR = apmlib
APMINC = -I$(srcdir)/apmlib/
endif
else
APMLIB =
APMDIR =
APMINC = 
endif

SUBDIRS = docs sounds $(APMDIR)

DIST_SUBDIRS = docs sounds apmlib

INCLUDES =					\
	$(GNOME_APPLETS3_CFLAGS)		\
	$(LIBNOTIFY_CFLAGS)			\
	$(HAL_CFLAGS)				\
	$(APMINC)				\
	$(ACPIINC)				\
	-DG_LOG_DOMAIN=\"battstat_applet\"	\
	-DBATTSTAT_MENU_UI_DIR=\""$(uidir)"\"


libexec_PROGRAMS = battstat-applet-2


battstat_applet_2_SOURCES = \
	battstat.h \
	pixmaps.h \
	properties.c \
	battstat_applet.c \
	power-management.c \
	acpi-linux.c \
	acpi-linux.h \
	acpi-freebsd.c \
	acpi-freebsd.h \
	battstat-hal.c \
	battstat-hal.h


battstat_applet_2_LDADD = \
		     $(GNOME_APPLETS3_LIBS) \
		     $(LIBNOTIFY_LIBS) \
		     $(HAL_LIBS) \
		     $(APMLIB)

schemasdir   = @GCONF_SCHEMA_FILE_DIR@
schemas_in_files = battstat.schemas.in
schemas_DATA = $(schemas_in_files:.schemas.in=.schemas)

@INTLTOOL_SCHEMAS_RULE@

if GCONF_SCHEMAS_INSTALL
install-data-local:
	GCONF_CONFIG_SOURCE=$(GCONF_SCHEMA_CONFIG_SOURCE) $(GCONFTOOL) --makefile-install-rule $(schemas_DATA) ;
endif

appletdir       = $(datadir)/gnome-panel/applets
applet_in_files = org.gnome.applets.BattstatApplet.panel-applet.in
applet_DATA     = $(applet_in_files:.panel-applet.in=.panel-applet)

$(applet_in_files): $(applet_in_files).in Makefile
	$(AM_V_GEN)sed \
            -e "s|\@LIBEXECDIR\@|$(libexecdir)|" \
            -e "s|\@VERSION\@|$(PACKAGE_VERSION)|" \
            $< > $@

%.panel-applet: %.panel-applet.in $(INTLTOOL_MERGE) $(wildcard $(top_srcdir)/po/*po) ; $(INTLTOOL_MERGE) $(top_srcdir)/po $< $@ -d -u -c $(top_builddir)/po/.intltool-merge-cache

servicedir       = $(datadir)/dbus-1/services
service_in_files = org.gnome.panel.applet.BattstatAppletFactory.service.in
service_DATA     = $(service_in_files:.service.in=.service)

org.gnome.panel.applet.BattstatAppletFactory.service: $(service_in_files)
	$(AM_V_GEN)sed \
            -e "s|\@LIBEXECDIR\@|$(libexecdir)|" \
            $< > $@

CLEANFILES = $(applet_DATA) $(applet_DATA).in $(service_DATA) $(schemas_DATA)

uidir = $(datadir)/gnome-2.0/ui
ui_DATA = battstat-applet-menu.xml

EXTRA_DIST = 							\
	$(builder_DATA)						\
	$(ui_DATA)						\
	org.gnome.applets.BattstatApplet.panel-applet.in.in	\
	$(service_in_files)					\
	$(schemas_in_files)


-include $(top_srcdir)/git.mk
