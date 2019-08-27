# ----------------------------------------
# Standard Constants
# ----------------------------------------
# these can be overwritten on the command line

OBO=http://purl.obolibrary.org/obo
ONT=hio
BASE=$(OBO)/$(ONT)
SRC=$(ONT)-edit.owl
RELEASEDIR=../..
ROBOT= ../../bin/robot
PREFIX="HIO: http://purl.obolibrary.org/obo/HIO_"

# ----------------------------------------
# Top-level targets
# ----------------------------------------

# by default we use Elk to perform a reason-relax-reduce chain
# after that we annotate the ontology with the release versionInfo
# Including associations from templates folder when ready templates/
$(ONT).owl: $(SRC) templates/condition_caused_or_contributed_to_by.tsv templates/condition_has_causal_or_contributing_genetic_variation.tsv templates/gene_carrying_contributing_genetic_variation.tsv templates/has_gene_product.tsv templates/has_genetic_variation.tsv templates/has_mode_of_inheritance.tsv templates/induced_by.tsv templates/treated_with.tsv
	$(ROBOT) template --input $(SRC) --merge-before --prefix $(PREFIX) --template templates/condition_caused_or_contributed_to_by.tsv --merge-before --prefix $(PREFIX) --template templates/condition_has_causal_or_contributing_genetic_variation.tsv --merge-before --prefix $(PREFIX) --template templates/gene_carrying_contributing_genetic_variation.tsv --merge-before --prefix $(PREFIX) --template templates/has_gene_product.tsv --merge-before --prefix $(PREFIX) --template templates/has_genetic_variation.tsv --merge-before --prefix $(PREFIX) --template templates/has_mode_of_inheritance.tsv --merge-before --prefix $(PREFIX) --template templates/induced_by.tsv --merge-before --prefix $(PREFIX) --template templates/treated_with.tsv reason -s true -m false -r ELK annotate -V $(BASE)/releases/`date +%Y-%m-%d`/$(ONT).owl -o $@

$(ONT).obo: $(ONT).owl
	$(ROBOT) convert -i $< -f obo -o $(ONT).obo.tmp && mv $(ONT).obo.tmp $@

# ----------------------------------------
# Release
# ----------------------------------------
# copy from staging area (this directory) to top-level
release: $(ONT).o*
	cp $^ $(RELEASEDIR)

