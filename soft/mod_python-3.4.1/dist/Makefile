 # Copyright (C) 2000, 2001, 2013 Gregory Trubetskoy
 # Copyright (C) 2002, 2003, 2004, 2005, 2006, 2007 Apache Software Foundation
 #
 #  Licensed under the Apache License, Version 2.0 (the "License");
 #  you may not use this file except in compliance with the License.
 #  You may obtain a copy of the License at
 #
 #      http://www.apache.org/licenses/LICENSE-2.0
 #
 #  Unless required by applicable law or agreed to in writing, software
 #  distributed under the License is distributed on an "AS IS" BASIS,
 #  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 #  See the License for the specific language governing permissions and
 #  limitations under the License.
 #
 # Originally developed by Gregory Trubetskoy.
 #
 # $Id$
 #

PYTHON_BIN=/usr/bin/python

build: mod_python src
	@cd src; $(MAKE) psp_parser.c
	$(PYTHON_BIN) setup.py build

# this one requires at least python 2.3
windist: mod_python.so
	$(PYTHON_BIN) setup.py bdist_wininst --install-script=win32_postinstall.py

install: install_py_lib

# this may require root priviledges
install_py_lib: mod_python src
	@cd src; $(MAKE) psp_parser.c
	if test -z "$(DESTDIR)" ; then \
		$(PYTHON_BIN) setup.py install --optimize 2 --force ; \
	else \
		$(PYTHON_BIN) setup.py install --optimize 2 --force --root $(DESTDIR) ; \
	fi

mod_python.so:
	@echo "Please place a WIN32 compiled mod_python.so in this directory"
	exit 1

mod_python:
	ln -s ../lib/python/mod_python mod_python

src:
	ln -s ../src src

clean:
	rm -rf mod_python build dist

distclean:
	rm -rf mod_python src build dist mod_python.so setup.py Makefile MANIFEST MANIFSET.in
