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
$(ONT).owl: $(SRC)
	$(ROBOT) template --input $(SRC) reason -s true -m false -r ELK annotate -V $(BASE)/releases/`date +%Y-%m-%d`/$(ONT).owl -o $@

$(ONT).obo: $(ONT).owl
	$(ROBOT) convert -i $< -f obo -o $(ONT).obo.tmp && mv $(ONT).obo.tmp $@

# ----------------------------------------
# Release
# ----------------------------------------
# copy from staging area (this directory) to top-level
release: $(ONT).o*
	cp $^ $(RELEASEDIR)

