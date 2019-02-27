# bashds
Bash commands for Data Science

## Table of Contents
* [Concatenating CSVs](#concatenating-csvs)
* [File Encodings](#file-encodings)

## <a name="concatenating-csvs"></a> Concatenating CSVs

### CSVs with a Header Row
Given a directory of CSVs all containing:

* a starting header row
* identical columns
* file names ending with `.csv`

the following commands will concatenate them into a single file, `all.csv`.

```
ls *.csv | grep -v all.csv | head -1 | xargs -I {} head -1 {} > all.csv
ls *.csv | grep -v all.csv | xargs -I {} tail -n +2 {} >> all.csv
```

### CSVs with no Header Row
Given a directory of CSVs all containing:

* no header row
* identical columns
* file names ending with `.csv`

the following commands will concatenate them into a single file, `all.csv`.

```
rm all.csv && touch all.csv
ls *.csv | grep -v all.csv | xargs -I {} cat {} >> all.csv
```

## <a name="file-encodings"></a> File Encodings

### Detecting a File's Encoding
Given a plaintext file `data.csv`, the following command will print its encoding.
```
file -i data.csv
```
