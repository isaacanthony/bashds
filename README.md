# bashds
Bash commands for Data Science

## Table of Contents
* [CSV Concatenation](#csv-concatenation)
* [CSV Splitting](#csv-splitting)
* [Dockerized JupyterLab](#dockerized-jupyterlab)
* [File Compression](#file-compression)
* [File Encoding](#file-encoding)
* [File Encryption](#file-encryption)
* [File Size](#file-size)

## <a name="csv-concatenation"></a> CSV Concatenation

### Concatenating CSVs with a Header Row
Given a directory of CSVs all containing:

* a starting header row
* identical columns
* file names ending with `.csv`

the following commands will concatenate them into a single file, `all.csv`.

```
ls *.csv | grep -v all.csv | head -1 | xargs -I {} head -1 {} > all.csv
ls *.csv | grep -v all.csv | xargs -I {} tail -n +2 {} >> all.csv
```

### Concatenating CSVs with no Header Row
Given a directory of CSVs all containing:

* no header row
* identical columns
* file names ending with `.csv`

the following commands will concatenate them into a single file, `all.csv`.

```
rm all.csv && touch all.csv
ls *.csv | grep -v all.csv | xargs -I {} cat {} >> all.csv
```

## <a name="csv-splitting"></a> CSV Splitting
Given a CSV `data.csv`, the following command will split it into N subfiles each of size 1gb.
The resulting files will be placed in the same directory and named xaa, xab, xac, etc.
```
split -C 1000m data.csv
```

## <a name="dockerized-jupyterlab"></a> Dockerized JupyterLab

### Run a SciPy Notebook in a Docker Container
The following command will run a local SciPy Notebook docker container on http://localhost:8888.
```
docker run -d --name scipy -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes -v $PWD:/home/jovyan jupyter/scipy-notebook
```

The following command will print the access token required to access the notebook.
```
docker logs scipy
```

The following command will stop the notebook.
```
docker stop scipy && docker rm scipy
```

### Run a PySpark Notebook in a Docker Container
The following command will run a local PySpark Notebook docker container on http://localhost:8888.
```
docker run -d --name pyspark -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes -v $PWD:/home/jovyan jupyter/pyspark-notebook
```

The following command will print the access token required to access the notebook.
```
docker logs pyspark
```

The following command will stop the notebook.
```
docker stop pyspark && docker rm pyspark
```

## <a name="file-compression"></a> File Compression

### Extracting a .tar.gz File
Given a tarball-gzipped archive file, `file.tar.gz`, the following command will extract its contents.
```
tar xvzf file.tar.gz
```

## <a name="file-encoding"></a> File Encoding

### Detecting a File's Encoding
Given a plaintext file `data.csv`, the following command will print its encoding.
```
file -i data.csv
```

## <a name="file-encryption"></a> File Encryption

### Decrypting Files using PGP
Given a file `data.csv.pgp` encrypted using PGP, the following command will decrypt the file and store it as `data.csv`. You will be automatically prompted for the password associated with your PGP key.
```
gpg --output data.csv --decrypt data.csv.pgp
```

### Creating an Encrypted ZIP File of a Directory
Given a directory `data`, the following command will create an encrypted ZIP file of that directory and store it as `data.zip`. You will be automatically prompted from the command line for the password to be used in the encryption/decryption.
```
zip -er data.zip data
```

## <a name="file-size"></a> File Size

### Detecting File Size
Given a file `data.csv`, the following command will return its size in GB.
```
du -h data.csv
```

### Detecting Directory Size
Given a directory `data`, the following command will return its size in GB.
```
du -h data
```
