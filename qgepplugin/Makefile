#/***************************************************************************
# Qgep
# 
# Qgep
#                             -------------------
#        begin                : 2012-08-31
#        copyright            : (C) 2012 by matthias kuhn
#        email                : matthias (dot) kuhn (at) gmx (dot) ch
# ***************************************************************************/
# 
#/***************************************************************************
# *                                                                         *
# *   This program is free software; you can redistribute it and/or modify  *
# *   it under the terms of the GNU General Public License as published by  *
# *   the Free Software Foundation; either version 2 of the License, or     *
# *   (at your option) any later version.                                   *
# *                                                                         *
# ***************************************************************************/
# Makefile for a PyQGIS plugin 
PLUGINNAME = qgepplugin
PY_FILES =  __init__.py  qgepplugin.py
EXTRAS = metadata.txt resources.qrc
RESOURCE_FILES = resources.py
TOOL_DIR = tools ui
ICONS_DIR = icons

UI_SOURCES=$(wildcard ui/*.ui)
#UI_FILES=$(notdir $(UI_SOURCES))
UI_FILES=$(join $(addsuffix ui_, $(dir $(UI_SOURCES))), $(notdir $(UI_SOURCES:%.ui=ui_%.py)))
RC_SOURCES=$(wildcard *.qrc)
RC_FILES=$(patsubst %.qrc,%.py,$(RC_SOURCES))

GEN_FILES = ${UI_FILES} ${RC_FILES}

all: $(GEN_FILES)
ui: $(UI_FILES)
resources: $(RC_FILES)

$(UI_FILES): ui/ui_%.py: ui/%.ui
	pyuic4 -o $@ $<
	
$(RC_FILES): %.py: %.qrc
	pyrcc4 -o $@ $<

clean:
	rm -f $(GEN_FILES) *.pyc


compile: $(UI_FILES) $(RESOURCE_FILES)

# The deploy  target only works on unix like operating system where
# the Python plugin directory is located at:
# $HOME/.qgis/python/plugins
deploy:
	mkdir -p $(HOME)/.qgis/python/plugins/$(PLUGINNAME)
	mkdir -p $(HOME)/.qgis/python/plugins/$(PLUGINNAME)/tools
	mkdir -p $(HOME)/.qgis/python/plugins/$(PLUGINNAME)/icons
	cp -vf $(PY_FILES) $(HOME)/.qgis/python/plugins/$(PLUGINNAME)
	cp -vf $(UI_FILES1) $(HOME)/.qgis/python/plugins/$(PLUGINNAME)/tools
	cp -vf $(RESOURCE_FILES) $(HOME)/.qgis/python/plugins/$(PLUGINNAME)
#	cp -vf $(RC_FILES) $(HOME)/.qgis/python/plugins/$(PLUGINNAME)
	cp -vf $(EXTRAS) $(HOME)/.qgis/python/plugins/$(PLUGINNAME)
	cp -rvf $(TOOL_DIR) $(HOME)/.qgis/python/plugins/$(PLUGINNAME)
	cp -rvf $(ICONS_DIR) $(HOME)/.qgis/python/plugins/$(PLUGINNAME)

