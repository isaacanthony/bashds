# bashds
Bash commands for Data Science

## Concatenating CSVs

### CSVs with a Header Row
Given a directory of CSVs all containing:

* a starting header row
* identical columns
* file names ending with `.csv`

the following commands will concatenate them into a single file, `concatenated.csv`.

```
@ls *.csv | head -1 | xargs -I {} head -1 {} > concatenated.csv
@ls *.csv | xargs -I {} tail -n +2 {} >> concatenated.csv
```

### CSVs with no Header Row
Given a directory of CSVs all containing:

* no header row
* identical columns
* file names ending with `.csv`

the following commands will concatenate them into a single file, `concatenated.csv`.

```
@rm concatenated.csv && touch concatenated.csv
@ls *.csv | xargs -I {} cat {} >> concatenated.csv
```
