
EXPE_FOLDERS := $(wildcard tests/*)
SIMULS_OUT := $(patsubst %,%/out_jobs.csv,$(EXPE_FOLDERS))
GANTTS_OUT := $(patsubst %,%/gantt.png,$(EXPE_FOLDERS))


all: simuls

simuls: testIntervals $(SIMULS_OUT) coverage_html

coverage_html: ../.coverage
	cd ..; coverage html -d tests/coverage_html

testIntervals:
	cd ..; python -m coverage run -a schedulers/intervalContainer.py

%/out_jobs.csv:
	cd ..;python launch_expe.py tests/$*/expe.json

gantts: $(GANTTS_OUT)

gantts_okular: $(GANTTS_OUT)
	okular $^


%/gantt.png: %/out_jobs.csv
	python ../../../../evalys/evalys/gantt.py $* $*/gantt.png


generate:
	python generate.py


clean:
	rm tests/*/out_jobs.csv
	cd ..; python -m coverage erase