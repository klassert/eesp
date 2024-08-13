NEW_FILE?=draft-klassert-ipsecme-eesp-00
OLD_FILE?=draft-klassert-ipsecme-eesp-00
MP-SUFF ?= $(mktemp -u XXXXXX)
TMP_FILE ?= $(NEW_FILE)-$(TMP-SUFF)


# Check if xml2rfc is available in the PATH
ifneq ($(shell which xml2rfc),)
    XML2RFC=$(shell which xml2rfc)
else
    XML2RFC?=/Users/antony/Library/Python/3.11/bin/xml2rfc
endif

all:
	$(XML2RFC) --v3 --text $(NEW_FILE).xml

html:
	$(XML2RFC) --v3 --html $(NEW_FILE).xml

lint:
	XMLLINT_INDENT="  " xmllint --format $(NEW_FILE).xml > $(TMP_FILE).xml && mv $(TMP_FILE).xml $(NEW_FILE).xml

rfcdiff:
	rfcdiff --body --diff  $(OLD_FILE).txt $(NEW_FILE).txt

xml2rfc:
	xml2rfc $(NEW_FILE).xml

tidy:
	tidy -i -xml -wrap 80 -i $(NEW_FILE).xml > $(TMP_FILE).xml && mv $(TMP_FILE).xml $(NEW_FILE).xml

aadiff:
	git diff  $(NEW_FILE).xml | grep -E "^[+-]" -A 1 -B 1 | grep -v "^--" > a
