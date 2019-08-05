# FunkLoad Makefile
# $Id: $
#
.PHONY: build pkg sdist egg install clean rpm

TARGET := gateway:/opt/public-dev/funkload

# use TAG=a for alpha, b for beta, rc for release candidate
ifdef TAG
	PKGTAG := egg_info --tag-build=$(TAG) --tag-date
else
    PKGTAG :=
endif


build:
	python setup.py $(PKGTAG) build

test:
	cd src/funkload/tests && fl-run-test -v --doctest test_Install.py

pkg: sdist egg

sdist:
	python setup.py $(PKGTAG) sdist

egg:
	-python2.7 setup.py $(PKGTAG) bdist_egg

distrib:
	-scp dist/funkload-*.tar.gz $(TARGET)/snapshots
	-scp dist/funkload-*.egg $(TARGET)/snapshots

install:
	python setup.py $(PKGTAG) install

register:
	-python2.7 setup.py register bdist_egg upload


uninstall:
	-easy_install -m funkload
	-rm -rf /usr/lib/python2.3/site-packages/funkload*
	-rm -rf /usr/lib/python2.4/site-packages/funkload*
	-rm -rf /usr/lib/python2.5/site-packages/funkload*
	-rm -rf /usr/lib/python2.6/dist-packages/funkload*
	-rm -rf /usr/local/lib/python2.6/dist-packages/funkload*
	-rm -rf /usr/local/funkload/
	-rm -f /usr/local/bin/fl-*
	-rm -f /usr/bin/fl-*

clean:
	find . "(" -name "*~" -or  -name ".#*" -or  -name "#*#" -or -name "*.pyc" ")" -print0 | xargs -0 rm -f
	rm -rf ./build ./dist ./MANIFEST ./funkload.egg-info
