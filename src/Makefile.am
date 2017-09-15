ttf_DATA = Hack-Regular.ttf Hack-Bold.ttf Hack-BoldItalic.ttf Hack-Italic.ttf

# GNU make will identify and delete "intermediate" files after the build.  We
# want to keep them around to speed up subsequent builds.
# See: https://www.gnu.org/software/make/manual/html_node/Chained-Rules.html
.PRECIOUS: merged/%.ufo master_ttf/%.ttf

merged:
	mkdir $@

merged/%.ufo: $(srcdir)/%.ufo $(srcdir)/%.ufo/* $(srcdir)/%.ufo/glyphs/* | merged
	rm -rf $@
	cp -R $< $@

master_ttf/%.ttf: merged/%.ufo
	fontmake --verbose ERROR -u $< -o ttf
	python $(top_srcdir)/postbuild_processing/fixes/fix-dsig.py $@ > /dev/null
	python $(top_srcdir)/postbuild_processing/fixes/fix-fstype.py $@ > /dev/null

if HINT_MINIMAL
TTFAUTOHINT_XHEIGHT_SNAPPING_EXCEPTIONS = '-'
else
TTFAUTOHINT_XHEIGHT_SNAPPING_EXCEPTIONS = ''
endif

%.ttf: control_file = $(top_srcdir)/postbuild_processing/tt-hinting/$(*)-TA.txt
%.ttf: master_ttf/%.ttf master_ttf/Hack-Regular.ttf $(top_srcdir)/postbuild_processing/tt-hinting/%-TA.txt
if HINT
	ttfautohint -l 6 -r 50 -x 10 -H 181 -D latn -f latn -w -G -W -t -X $(TTFAUTOHINT_XHEIGHT_SNAPPING_EXCEPTIONS) -I -R master_ttf/Hack-Regular.ttf -m $(control_file) $< $@
else
	cp $< $@
endif

CLEANFILES = $(ttf_DATA)
clean-local:
	-rm -rf merged master_ttf
