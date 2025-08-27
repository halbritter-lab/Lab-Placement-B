# Resource: BLAST

## Description

BLAST (Basic Local Alignment Search Tool) is a suite of programs used to generate alignments between a nucleotide or protein sequence, called a "query", and a database of sequences.

## URL

[NCBI BLAST Homepage](https://blast.ncbi.nlm.nih.gov/Blast.cgi)

## Installation/Usage

BLAST can be used online or as a standalone command-line tool.

### Using BLAST online

1.  Go to the [NCBI BLAST Homepage](https://blast.ncbi.nlm.nih.gov/Blast.cgi).
2.  Select the appropriate BLAST program (e.g., blastn, blastp).
3.  Enter your query sequence.
4.  Choose the database to search against.
5.  Click the "BLAST" button.

### Using BLAST locally

To use BLAST locally, you need to install the NCBI BLAST+ suite.

```bash
# Example for Debian/Ubuntu
sudo apt-get update
sudo apt-get install ncbi-blast+
```

Once installed, you can use the command-line tools. For example:

```bash
blastp -query my_protein.fasta -db pdb -out results.txt
```

## Notes

-   The `-db` option specifies the database to search against. You can download pre-formatted databases from NCBI or create your own.
-   The `-out` option specifies the file to write the results to.
-   There are many other options available to customize your search. Use the `-help` flag to see them all (e.g., `blastp -help`).
