#RADumi

```
usage: radumi [-h] [-v] {sort,add,scanp,dump,scan} ...

Finding unique restriction site associated DNA (RAD) tag sequences per unique
molecular identifier (UMI).

positional arguments:
  {sort,add,scanp,dump,scan}
                        commands
    dump                obtain fasta of read name and 5' UMI sequence
    add                 add 5' UMI from dumped fasta onto reads of FASTQ
    sort                order the fastq by the UMI to facilitate processing
    scan                find most abundant sequence per UMI
    scanp               find most abundant sequence per UMI

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
```

##dump

For R2, without a UMI, dump the UMI sequence from R1 into a fasta.

Prints FASTA to stdout.

```
usage: radumi dump [-h] FASTQ LENGTH

Prints fasta of read name and 5' UMI sequence.

positional arguments:
  FASTQ       fastq containing a UMI
  LENGTH      length of the UMI sequence

optional arguments:
  -h, --help  show this help message and exit
```

##add

Add the dumped UMI from R1 onto R2.

Prints FASTQ to stdout.

```
usage: radumi add [-h] FASTQ FASTA

Add UMI of dumped FASTA onto matched read name of FASTQ on the 5' end. Quality
of the UMI will be ']'.

positional arguments:
  FASTQ       reads onto which to add the UMI
  FASTA       dumped UMI sequences

optional arguments:
  -h, --help  show this help message and exit
```

##sort

Before scanning for the most abundant sequence per UMI, sort the sequences by
their UMI.

Prints FASTQ to stdout.

```
usage: radumi sort [-h] FASTQ LENGTH

Sorts fastq by UMI.

positional arguments:
  FASTQ       unsorted reads with incorporated UMI
  LENGTH      length of the UMI sequence

optional arguments:
  -h, --help  show this help message and exit
```

##scan

Scan UMI sorted FASTQ for most abundant sequence per UMI. You can performing
trimming beforehand or use `-5` and `-3` to designate the amount of sequence
to remove from the respective end. Trimming on the 5' end occurs after the UMI.

Prints FASTA to stdout.

```
usage: radumi scan [-h] [-m MISMATCHES] [-5 FIVE] [-3 THREE] FASTQ UMI

Finds most abundant sequence per valid UMI.

positional arguments:
  FASTQ                 reads with UMI to scan
  UMI                   IUPAC sequence of the UMI, e.g. NNNNNV

optional arguments:
  -h, --help            show this help message and exit
  -m MISMATCHES, --mismatches MISMATCHES
                        allowable mismatches when finding unique sequences [3]
  -5 FIVE               number of 5' bases to trim AFTER the UMI sequence [0]
  -3 THREE              number of 3' bases to trim [0]
```

##scanp

Scan for paired-end reads.

```
usage: radumi scanp [-h] [-m MISMATCHES] [--r1-5 R1FIVE] [--r1-3 R1THREE]
                    [--r2-5 R2FIVE] [--r2-3 R2THREE]
                    R1-IN R2-IN R1-OUT R2-OUT UMI

Finds most abundant sequence per valid UMI among paired-end reads.

positional arguments:
  R1-IN                 R1 FASTQ with UMI to scan.
  R2-IN                 R2 FASTQ with UMI to scan.
  R1-OUT                R1 output FASTA.
  R2-OUT                R2 output FASTA.
  UMI                   IUPAC sequence of the UMI, e.g. NNNNNV

optional arguments:
  -h, --help            show this help message and exit
  -m MISMATCHES, --mismatches MISMATCHES
                        allowable mismatches when finding unique sequences [3]
  --r1-5 R1FIVE         number of 5' bases to trim AFTER the UMI sequence in
                        R1 [0]
  --r1-3 R1THREE        number of 3' bases to trim in R1 [0]
  --r2-5 R2FIVE         number of 5' bases to trim AFTER the UMI sequence in
                        R2 [0]
  --r2-3 R2THREE        number of 3' bases to trim in R2 [0]
```

##Dependencies

Uses `toolshed`, `awk`, `sort`, and `tr`.
```
pip install toolshed
```
