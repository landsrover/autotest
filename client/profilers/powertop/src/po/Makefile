SRC=$(wildcard *.po)
OBJ= $(SRC:.po=.mo)
INST= $(SRC:.po=.inst)

translations: $(OBJ)
	
%.mo: %.po
	msgfmt -o $@  $<

clean:
	rm -f *.mo *~

# hack to automate installation dynamicaly, without previous knowledge of 
# the po/mo file list (we fool make by pretending the need for .inst files).
install: $(OBJ) $(INST)

%.inst: %.mo
	mkdir -p $(DESTDIR)$(LOCALESDIR)/$*/LC_MESSAGES/
	-cp -f $< $(DESTDIR)$(LOCALESDIR)/$*/LC_MESSAGES/powertop.mo

uptrans: $(LG).po

$(LG).po: powertop.pot
ifdef LG
	msgmerge -U $@ $<
else
	@echo "Usage : make uptrans LG=xx # with xx = de, es, fi ..."
	@exit 1
endif

