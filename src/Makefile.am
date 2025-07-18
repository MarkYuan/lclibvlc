###############################################################################
# Automake targets and declarations
###############################################################################

AUTOMAKE_OPTIONS = subdir-objects

NULL =
EXTRA_DIST = \
	vlc-plugin.pc.in \
	libvlccore.sym \
	revision.txt

BUILT_SOURCES = $(nodist_pluginsinclude_HEADERS)
CLEANFILES = $(BUILT_SOURCES)

SUFFIXES = .pc.in .pc .rc.in .rc

###############################################################################
# Headers
###############################################################################

pluginsincludedir = $(pkgincludedir)/plugins

pluginsinclude_HEADERS = \
	../include/vlc_access.h \
	../include/vlc_actions.h \
	../include/vlc_addons.h \
	../include/vlc_aout.h \
	../include/vlc_aout_volume.h \
	../include/vlc_arrays.h \
	../include/vlc_atomic.h \
	../include/vlc_avcodec.h \
	../include/vlc_bits.h \
	../include/vlc_block.h \
	../include/vlc_block_helper.h \
	../include/vlc_boxes.h \
	../include/vlc_charset.h \
	../include/vlc_codec.h \
	../include/vlc_common.h \
	../include/vlc_config.h \
	../include/vlc_config_cat.h \
	../include/vlc_configuration.h \
	../include/vlc_cpu.h \
	../include/vlc_dialog.h \
	../include/vlc_demux.h \
	../include/vlc_epg.h \
	../include/vlc_es.h \
	../include/vlc_es_out.h \
	../include/vlc_events.h \
	../include/vlc_filter.h \
	../include/vlc_fourcc.h \
	../include/vlc_fs.h \
	../include/vlc_gcrypt.h \
	../include/vlc_opengl.h \
	../include/vlc_http.h \
	../include/vlc_httpd.h \
	../include/vlc_image.h \
	../include/vlc_inhibit.h \
	../include/vlc_input.h \
	../include/vlc_input_item.h \
	../include/vlc_interface.h \
	../include/vlc_keystore.h \
	../include/vlc_main.h \
	../include/vlc_list.h \
	../include/vlc_md5.h \
	../include/vlc_messages.h \
	../include/vlc_meta.h \
	../include/vlc_meta_fetcher.h \
	../include/vlc_media_library.h \
	../include/vlc_memstream.h \
	../include/vlc_mime.h \
	../include/vlc_modules.h \
	../include/vlc_mouse.h \
	../include/vlc_mtime.h \
	../include/vlc_network.h \
	../include/vlc_objects.h \
	../include/vlc_picture.h \
	../include/vlc_picture_fifo.h \
	../include/vlc_picture_pool.h \
	../include/vlc_playlist.h \
	../include/vlc_plugin.h \
	../include/vlc_probe.h \
	../include/vlc_rand.h \
	../include/vlc_services_discovery.h \
	../include/vlc_fingerprinter.h \
	../include/vlc_interrupt.h \
	../include/vlc_renderer_discovery.h \
	../include/vlc_sout.h \
	../include/vlc_spu.h \
	../include/vlc_stream.h \
	../include/vlc_stream_extractor.h \
	../include/vlc_strings.h \
	../include/vlc_subpicture.h \
	../include/vlc_text_style.h \
	../include/vlc_threads.h \
	../include/vlc_timestamp_helper.h \
	../include/vlc_tls.h \
	../include/vlc_url.h \
	../include/vlc_variables.h \
	../include/vlc_viewpoint.h \
	../include/vlc_vlm.h \
	../include/vlc_video_splitter.h \
	../include/vlc_vout.h \
	../include/vlc_vout_display.h \
	../include/vlc_vout_osd.h \
	../include/vlc_vout_window.h \
	../include/vlc_xml.h \
	../include/vlc_xlib.h \
	$(NULL)
nodist_pluginsinclude_HEADERS = ../include/vlc_about.h

noinst_HEADERS = \
	../include/vlc_codecs.h \
	../include/vlc_extensions.h \
	../include/vlc_fixups.h \
	../include/vlc_intf_strings.h \
	../include/vlc_iso_lang.h \
	../include/vlc_memory.h \
	../include/vlc_pgpkey.h \
	../include/vlc_update.h \
	../include/vlc_vod.h \
	../include/vlc_vout_wrapper.h \
	$(NULL)

../include/vlc_about.h: Makefile.am $(top_srcdir)/COPYING $(top_srcdir)/THANKS $(top_srcdir)/AUTHORS
	$(AM_V_at)rm -f -- "$@.tmp"
	$(AM_V_at)mkdir -p -- ../include
	$(AM_V_GEN)(echo "/* Automatically generated file - DO NOT EDIT */" && \
	echo "static const char psz_license[] =" && \
	sed 's/"/\\"/g;s/^.*$$/\"&\\n\"/' "$(top_srcdir)/COPYING" && \
	echo ";" && \
	echo "static const char psz_thanks[] =" && \
	sed '/\$$Id:/d;s/"/\\"/g;s/<.*.> //;s/^.*$$/\"&\\n\"/' \
		"$(top_srcdir)/THANKS" && \
	echo ";" && \
	echo "static const char psz_authors[] =" && \
	sed '/\$$Id:/d;s/"/\\"/g;s/<.*.> //;s/^.*$$/\"&\\n\"/' \
		"$(top_srcdir)/AUTHORS" && \
	echo ";") >> "$@.tmp"
	$(AM_V_at)mv -f -- "$@.tmp" "$@"

###############################################################################
# pkg-config integration
###############################################################################

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = vlc-plugin.pc
CLEANFILES += $(pkgconfig_DATA)

.pc.in.pc: $(top_builddir)/config.status
	$(AM_V_GEN)cd "$(top_builddir)" && \
	$(SHELL) ./config.status --file="src/$@"

##############################################################################
# Windows resource files
##############################################################################

if HAVE_WIN32
noinst_DATA = libvlc_win32_rc.rc
endif
EXTRA_DIST += libvlc_win32_rc.rc.in

.rc.in.rc: $(top_builddir)/config.status
	cd "$(top_builddir)" && \
	$(SHELL) ./config.status --file="src/$@"

###############################################################################
# Building libvlc
###############################################################################

lib_LTLIBRARIES = libvlccore.la

AM_CPPFLAGS = $(INCICONV) $(IDN_CFLAGS) \
	-DMODULE_STRING=\"core\" \
	-DLOCALEDIR=\"$(localedir)\" \
	-DPKGDATADIR=\"$(vlcdatadir)\" \
	-DPKGLIBDIR=\"$(vlclibdir)\"
AM_CFLAGS = $(CFLAGS_libvlccore)
if HAVE_DYNAMIC_PLUGINS
AM_CPPFLAGS += -DHAVE_DYNAMIC_PLUGINS
endif
if HAVE_DBUS
AM_CPPFLAGS += -DHAVE_DBUS
AM_CFLAGS += $(DBUS_CFLAGS)
endif

libvlccore_la_SOURCES = \
	libvlc.c \
	libvlc.h \
	libvlc-module.c \
	missing.c \
	revision.c \
	version.c \
	config/configuration.h \
	config/core.c \
	config/chain.c \
	config/file.c \
	config/help.c \
	config/intf.c \
	config/cmdline.c \
	config/getopt.c \
	config/vlc_getopt.h \
	extras/libc.c \
	extras/tdestroy.c \
	modules/modules.h \
	modules/modules.c \
	modules/bank.c \
	modules/cache.c \
	modules/entry.c \
	modules/textdomain.c \
	interface/dialog.c \
	interface/interface.c \
	playlist/playlist_internal.h \
	playlist/art.c \
	playlist/art.h \
	playlist/aout.c \
	playlist/thread.c \
	playlist/control.c \
	playlist/engine.c \
	playlist/fetcher.c \
	playlist/fetcher.h \
	playlist/sort.c \
	playlist/loadsave.c \
	playlist/preparser.c \
	playlist/preparser.h \
	playlist/tree.c \
	playlist/item.c \
	playlist/search.c \
	playlist/services_discovery.c \
	playlist/renderer.c \
	input/item.c \
	input/access.c \
	input/clock.c \
	input/control.c \
	input/decoder.c \
	input/demux.c \
	input/demux_chained.c \
	input/es_out.c \
	input/es_out_timeshift.c \
	input/event.c \
	input/input.c \
	input/info.h \
	input/meta.c \
	input/clock.h \
	input/attachment.c \
	input/decoder.h \
	input/demux.h \
	input/es_out.h \
	input/es_out_timeshift.h \
	input/event.h \
	input/item.h \
	input/mrl_helpers.h \
	input/stream.h \
	input/input_internal.h \
	input/input_interface.h \
	input/vlm_internal.h \
	input/vlm_event.h \
	input/resource.h \
	input/resource.c \
	input/services_discovery.c \
	input/stats.c \
	input/stream.c \
	input/stream_fifo.c \
	input/stream_extractor.c \
	input/stream_filter.c \
	input/stream_memory.c \
	input/subtitles.c \
	input/var.c \
	audio_output/aout_internal.h \
	audio_output/common.c \
	audio_output/dec.c \
	audio_output/filters.c \
	audio_output/output.c \
	audio_output/volume.c \
	video_output/chrono.h \
	video_output/control.c \
	video_output/control.h \
	video_output/display.c \
	video_output/display.h \
	video_output/event.h \
	video_output/inhibit.c \
	video_output/inhibit.h \
	video_output/interlacing.c \
	video_output/interlacing.h \
	video_output/snapshot.c \
	video_output/snapshot.h \
	video_output/statistic.h \
	video_output/video_output.c \
	video_output/video_text.c \
	video_output/video_epg.c \
	video_output/video_widgets.c \
	video_output/vout_subpictures.c \
	video_output/vout_spuregion_helper.h \
	video_output/window.c \
	video_output/window.h \
	video_output/opengl.c \
	video_output/vout_intf.c \
	video_output/vout_internal.h \
	video_output/vout_control.h \
	video_output/vout_wrapper.c \
	network/getaddrinfo.c \
	network/http_auth.c \
	network/httpd.c \
	network/io.c \
	network/tcp.c \
	network/udp.c \
	network/rootbind.c \
	network/tls.c \
	text/charset.c \
	text/memstream.c \
	text/strings.c \
	text/unicode.c \
	text/url.c \
	text/filesystem.c \
	text/iso_lang.c \
	text/iso-639_def.h \
	misc/actions.c \
	misc/background_worker.c \
	misc/background_worker.h \
	misc/md5.c \
	misc/probe.c \
	misc/rand.c \
	misc/mtime.c \
	misc/block.c \
	misc/fifo.c \
	misc/fourcc.c \
	misc/fourcc_list.h \
	misc/es_format.c \
	misc/picture.c \
	misc/picture.h \
	misc/picture_fifo.c \
	misc/picture_pool.c \
	misc/interrupt.h \
	misc/interrupt.c \
	misc/keystore.c \
	misc/renderer_discovery.c \
	misc/threads.c \
	misc/cpu.c \
	misc/epg.c \
	misc/exit.c \
	misc/events.c \
	misc/image.c \
	misc/messages.c \
	misc/mime.c \
	misc/objects.c \
	misc/objres.c \
	misc/variables.h \
	misc/variables.c \
	misc/error.c \
	misc/xml.c \
	misc/addons.c \
	misc/filter.c \
	misc/filter_chain.c \
	misc/httpcookies.c \
	misc/fingerprinter.c \
	misc/text_style.c \
	misc/subpicture.c \
	misc/subpicture.h
libvlccore_la_LIBADD = $(LIBS_libvlccore) \
	../compat/libcompat.la \
	$(LTLIBINTL) $(LTLIBICONV) \
	$(IDN_LIBS) $(LIBPTHREAD) $(SOCKET_LIBS) $(LIBRT) $(LIBDL) $(LIBM)

if HAVE_WIN32
libvlccore_la_SOURCES += \
	win32/dirs.c \
	win32/error.c \
	win32/filesystem.c \
	win32/netconf.c \
	win32/plugin.c \
	win32/rand.c \
	win32/specific.c \
	win32/thread.c \
	win32/winsock.c
if HAVE_WINSTORE
libvlccore_la_SOURCES += posix/timer.c
else
libvlccore_la_SOURCES += win32/timer.c
endif
else
if HAVE_OS2
libvlccore_la_SOURCES += \
	os2/dirs.c \
	darwin/error.c \
	os2/filesystem.c \
	os2/getaddrinfo.c \
	os2/netconf.c \
	os2/plugin.c \
	os2/specific.c \
	os2/rand.c \
	os2/thread.c
else
if HAVE_NACL
libvlccore_la_SOURCES += \
	android/error.c \
	posix/dirs.c \
	posix/filesystem.c \
	posix/netconf.c \
	posix/rand.c \
	posix/specific.c \
	posix/timer.c
else
libvlccore_la_SOURCES += \
	posix/filesystem.c \
	posix/plugin.c \
	posix/rand.c \
	posix/timer.c
if HAVE_ANDROID
libvlccore_la_SOURCES += \
	android/error.c \
	android/specific.c \
	android/thread.c \
	linux/cpu.c \
	linux/dirs.c \
	linux/thread.c
else
if HAVE_DARWIN
libvlccore_la_SOURCES += \
	darwin/dirs.c \
	darwin/error.c \
	darwin/netconf.c \
	darwin/specific.c \
	darwin/thread.c
else
libvlccore_la_SOURCES += \
	posix/dirs.c \
	posix/error.c \
	posix/netconf.c \
	posix/specific.c \
	posix/thread.c
if HAVE_LINUX
libvlccore_la_SOURCES += \
	linux/cpu.c \
	linux/dirs.c \
	linux/thread.c
endif
if HAVE_LIBANL
libvlccore_la_SOURCES += \
	linux/getaddrinfo.c
libvlccore_la_LIBADD += -lanl
else
libvlccore_la_SOURCES += \
	posix/getaddrinfo.c
endif
endif
endif
endif
endif
endif

if ENABLE_SOUT
libvlccore_la_SOURCES += \
	stream_output/sap.c stream_output/sdp.c \
	stream_output/stream_output.c stream_output/stream_output.h
if ENABLE_VLM
libvlccore_la_SOURCES += input/vlm.c input/vlm_event.c input/vlmshell.c
endif
endif

if UPDATE_CHECK
libvlccore_la_SOURCES += \
	misc/update.h misc/update.c \
	misc/update_crypto.c
AM_CPPFLAGS += -DUPDATE_CHECK
AM_CFLAGS += $(GCRYPT_CFLAGS)
libvlccore_la_LIBADD += $(GCRYPT_LIBS)
endif

libvlccore_la_LDFLAGS = \
	$(LDFLAGS_libvlccore) \
	-no-undefined \
	-export-symbols $(srcdir)/libvlccore.sym \
	-version-info 9:1:0
libvlccore_la_DEPENDENCIES = libvlccore.sym
if HAVE_WIN32
libvlccore_la_DEPENDENCIES += libvlc_win32_rc.$(OBJEXT)
libvlccore_la_LDFLAGS += -Wl,libvlc_win32_rc.$(OBJEXT) -avoid-version -Wc,-static $(LIBCOM)
endif
if HAVE_OS2
libvlccore_la_LDFLAGS += -avoid-version
endif
if HAVE_DBUS
libvlccore_la_LIBADD += $(DBUS_LIBS)
endif
if HAVE_DARWIN
libvlccore_la_LDFLAGS += -Xlinker -install_name -Xlinker @rpath/libvlccore.dylib
if !HAVE_OSX
libvlccore_la_LDFLAGS += -Wl,-framework,CFNetwork
endif
endif

libvlc_win32_rc.$(OBJEXT): libvlc_win32_rc.rc $(top_srcdir)/extras/package/win32/libvlc.dll.manifest
	$(WINDRES) --include-dir $(top_srcdir)/share --include-dir $(top_srcdir)/extras/package/win32 -i $< -o $@

# FourCC tables
BUILT_SOURCES += fourcc_tables.h
EXTRA_DIST += misc/fourcc_gen.c
MOSTLYCLEANFILES = fourcc_gen$(BUILDEXEEXT)

fourcc_gen$(BUILDEXEEXT): misc/fourcc_gen.c misc/fourcc_list.h ../include/vlc_fourcc.h
	$(AM_V_at)rm -f -- $@
	$(AM_V_CC)$(BUILDCC) -I$(srcdir) -o $@ $<

fourcc_tables.h: fourcc_gen$(BUILDEXEEXT)
	$(AM_V_at)rm -f -- $@.tmp
	$(AM_V_GEN)$(builddir)/fourcc_gen$(BUILDEXEEXT) > $@.tmp
	$(AM_V_at)mv -f -- $@.tmp $@

# Unit/regression tests
#
check_PROGRAMS = \
	test_block \
	test_dictionary \
	test_i18n_atof \
	test_interrupt \
	test_md5 \
	test_picture_pool \
	test_sort \
	test_timer \
	test_url \
	test_utf8 \
	test_xmlent \
	test_headers \
	test_mrl_helpers

TESTS = $(check_PROGRAMS) check_symbols

test_block_SOURCES = test/block_test.c
test_block_LDADD = $(LDADD) $(LIBS_libvlccore)
test_block_DEPENDENCIES =

test_dictionary_SOURCES = test/dictionary.c
test_i18n_atof_SOURCES = test/i18n_atof.c
test_interrupt_SOURCES = test/interrupt.c
test_interrupt_LDADD = $(LDADD) $(LIBS_libvlccore) $(LIBPTHREAD)
test_md5_SOURCES = test/md5.c
test_picture_pool_SOURCES = test/picture_pool.c
test_sort_SOURCES = test/sort.c
test_timer_SOURCES = test/timer.c
test_url_SOURCES = test/url.c
test_utf8_SOURCES = test/utf8.c
test_xmlent_SOURCES = test/xmlent.c
test_headers_SOURCES = test/headers.c
test_mrl_helpers_SOURCES = test/mrl_helpers.c

AM_LDFLAGS = -no-install
LDADD = libvlccore.la \
	../compat/libcompat.la

###############################################################################
# GIT revision
###############################################################################

BUILT_SOURCES += stamp-revision
MAINTAINERCLEANFILES = $(srcdir)/revision.txt $(srcdir)/revision.c

$(srcdir)/revision.c: $(srcdir)/revision.txt
	$(AM_V_at)rm -f -- $@
	$(AM_V_GEN)echo "const char psz_vlc_changeset[] = \"$$(cat $<)\";" \
		> $@

$(srcdir)/revision.txt:
	$(AM_V_at)$(MAKE) stamp-revision
	$(AM_V_GEN)touch $@

stamp-revision:
	$(AM_V_at)rm -f -- revision.tmp
	$(AM_V_GEN)if ! git \
			-C "$(top_srcdir)" describe \
			--tags --long --match '?.*.*' --always; then \
		cat $(srcdir)/revision.txt ; \
	fi > revision.tmp
	$(AM_V_at)if diff revision.tmp $(srcdir)/revision.txt >/dev/null 2>&1; then \
		rm -f -- revision.tmp; \
	else \
		mv -f -- revision.tmp $(srcdir)/revision.txt; \
	fi
#2>&1

###############################################################################
# Unit/regression test
###############################################################################

dist_check_SCRIPTS = check_headers check_symbols

check-local:
	for h in `echo $(pkginclude_HEADERS) | sed -e s,\.\./include/,,g`; \
	do \
		echo grep - "#include <$$h>" $(srcdir)/test/headers.c ; \
		if ! grep -- "#include <$$h>" $(srcdir)/test/headers.c ; \
		then \
			echo "Header $$h not included in test/headers.c!"; \
			exit 1; \
		fi ; \
	done
	$(SHELL) $(srcdir)/check_headers $(pluginsinclude_HEADERS)

FORCE:
	@echo "Generated source cannot be phony. Go away." >&2
	@exit 1

.PHONY: FORCE
