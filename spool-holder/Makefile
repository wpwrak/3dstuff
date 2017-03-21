STLS = left right

.PHONY:		all stl depend clean

all:		$(STLS:%=%.slvs)

stl:		$(STLS:%=%.stl)

#----- STL --------------------------------------------------------------------

%.stl:		%.slvs
		solvespace-cli export-mesh -o $@ -t 0.05 $<

#----- Dependencies -----------------------------------------------------------

-include .depend

%.slvs:
		@echo "refresh $@ due to change in $<" 2>&1
		solvespace-cli regenerate $@

depend:
		>.depend
		for n in `git ls-files '*.slvs'`; do \
		    sed "/Group.impFileRel=/s//$$n: /p;d" $$n >>.depend; \
		done

#----- Cleanup ----------------------------------------------------------------

clean:
		rm -f .depend $(STLS:%=%.stl)
