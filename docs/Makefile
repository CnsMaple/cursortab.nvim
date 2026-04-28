PUMLS  := $(wildcard *.puml)
SVGS   := $(PUMLS:.puml=.svg)
PNGS   := $(PUMLS:.puml=.png)
MAGICK := $(shell command -v magick 2>/dev/null)

.PHONY: all svg png clean

all: svg png

svg: $(SVGS)
png: $(PNGS)

%.svg: %.puml
	plantuml -tsvg $<

%.png: %.puml
	PLANTUML_LIMIT_SIZE=8192 plantuml -tpng $<
ifdef MAGICK
	$(MAGICK) $@ -strip +dither -colors 256 \
		-define png:compression-level=9 \
		-define png:compression-filter=5 \
		-define png:compression-strategy=1 \
		PNG8:$@
else
	@echo "magick not found, skipping PNG compression"
endif

clean:
	rm -f $(SVGS) $(PNGS)
