# bashds
Bash commands for Data Science

## Concatenating CSVs

#### CSVs with a Header Row
Given a directory of CSVs all containing:

* a starting header row
* identical columns
* file names ending with `.csv`

the following commands will concatenate them into a single file, `all.csv`.

```
ls *.csv | head -1 | xargs -I {} head -1 {} > all.csv
ls *.csv | xargs -I {} tail -n +2 {} >> all.csv
```

#### CSVs with no Header Row
Given a directory of CSVs all containing:

* no header row
* identical columns
* file names ending with `.csv`

the following commands will concatenate them into a single file, `all.csv`.

```
rm all.csv && touch all.csv
ls *.csv | xargs -I {} cat {} >> all.csv
```
