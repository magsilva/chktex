SRC=index.wml
SRC_STATIC=sitewide.css
OUT=$(SRC:%.wml=%.html)

all: files_changed run install

run:
	wmk --optimize=4

files_changed:
	@ls -R ../files | cat - Makefile | md5sum > md5sum.new
	@if [ ! -e "md5sum.old" ]; then \
		echo "No old md5sum file, recompiling everything."; \
		make clean; \
	else \
		if [ "`cat md5sum.old`" != "`cat md5sum.new`" ]; then \
			echo "File list changed, recompiling!"; \
			make clean; \
		fi ;\
	fi
	@mv md5sum.new md5sum.old

clean:
	-rm -f $(OUT)

install:
	install -m 0644 $(OUT) $(SRC_STATIC) ../realsite/
