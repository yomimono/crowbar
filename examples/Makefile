TESTS = calendar xmldiff pprint map fpath join
PKG_calendar = calendar
PKG_pprint = pprint,str
PKG_xmldiff = xmldiff
PKG_map =
PKG_fpath = fpath
PKG_join =

.PHONY: all clean
all: $(TESTS) alltests
clean:
	rm -f $(TESTS) alltests

$(TESTS): %: test_%.ml
	ocamlfind ocamlopt -package crowbar,$(PKG_$*) -linkpkg $^ -o $@ 

ALL_PKG = $(foreach v,$(TESTS),$(PKG_$(v)))
alltests: $(TESTS:%=test_%.ml)
	ocamlfind ocamlopt -package crowbar \
	  $(ALL_PKG:%=-package %) \
	  -linkpkg \
	  $^ -o $@

.gitignore: Makefile
	{ \
	   echo '*.cm*'; \
	   echo '*.o'; \
	   echo output; \
	   for i in $(TESTS) alltests; do echo $$i; done \
	} > $@
