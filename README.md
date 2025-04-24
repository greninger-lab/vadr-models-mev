# <a name="documentation"></a>Measles virus (MeV) genome annotation

## [How to annotate MeV sequences with VADR](#howto)

## [MeV VADR model library](#mevmodels)

## [Additional VADR documentation](#docs)

## [References](#reference)


---
## <a name="howto"></a>How to annotate MeV genomes with VADR

Steps for using VADR for MeV annotation:

1. Download and install the latest version of VADR, following the
   instructions on this [page](https://github.com/ncbi/vadr/tree/master).
   Alternatively, you can use the StaPH-B VADR 1.6.3-hav-flu2
   docker image created by Curtis Kapsak (docker image names:
   `staphb/vadr:1.6.3-hav-flu2` and `staphb/vadr:latest`), available on 
   [dockerhub](https://hub.docker.com/r/staphb/vadr/tags) and
   [quay](https://quay.io/repository/staphb/vadr?tab=tags). A brief
   [README for the docker image is here](https://github.com/StaPH-B/docker-builds/tree/master/vadr/1.6.3-hav-flu2).
 
2. Clone the latest MeV VADR model library from this repository. <!-- (current release v1.0)<br/>-->
   `git clone git@github.com:greninger-lab/vadr-models-mev.git`<br/>
   <!--or download the current release from [here](https://github.com/greninger-lab/vadr-models-hpiv/releases/tag/v1.0).</br>-->
   Note the path to the directory name created plus the "mev"
   subdirectory (e.g. /path/to/vadr-models-mev/mev) as `<mev-models-dir-path>`
   for step 4.

3. Remove terminal ambiguous nucleotides from your
   input fasta sequence file using the `fasta-trim-terminal-ambigs.pl`
   script in `$VADRSCRIPTSDIR/miniscripts/`.

   To remove terminal ambiguous nucleotides from your sequence file
   `<input-fasta-file>` and to remove short and long sequences to create a new trimmed file
   `<trimmed-fasta-file>`, execute:

```
$VADRSCRIPTSDIR/miniscripts/fasta-trim-terminal-ambigs.pl --minlen 50 --maxlen 18000 <input-fasta-file> > <trimmed-fasta-file>
```        

4. Run the `v-annotate.pl` program on an input trimmed fasta file with
   MeV sequences using the recommended command below.
```
v-annotate.pl -r --indefclass 0.01 --mkey mev --mdir <mev-models-dir-path> <fasta-file-to-annotate> <output-directory-to-create>
```

5. After running the `v-annotate.pl` command in step 4, there will be a number of files
   generated in the `<output-directory-to-create>`. Among these files, there are 5-column
   tab-delimited feature table files that end with the suffix `.tbl`. There is a separate
   file for passing (`XXXXX.vadr.pass.tbl`) and failing (`XXXXX.vadr.fail.tbl`) sequences.
   The format of the `.tbl` files is described here:
   https://www.ncbi.nlm.nih.gov/genbank/feature_table/

   More information about understanding failures and error alerts can be found in the VADR
   documentation here: https://github.com/ncbi/vadr/blob/master/documentation/annotate.md

---
## <a name="mevmodels"></a>MeV VADR model library
* The VADR model library for MeV annotation was developed using representative sequences from the 15
  genotypes currently available in the complete MeV genomes published in GenBank: AF266288(A), OR290098(B3),
  LC655230(C1), MG912589(C2), AB481088(D3), OP236009(D4), JN635406(D5), DQ227319(D6),
  JN635410(D7), PP101943(D8), KY969476(D9), MN017369(D11), GMG912591(G2), KC164758(G3),
  MZ442631(H1).
---

## <a name="docs"> Additional VADR documentation

* [VADR README](https://github.com/ncbi/vadr/blob/master/README.md#top)
* [VADR installation instructions](https://github.com/ncbi/vadr/blob/master/documentation/install.md#top)
  * [Installation using `vadr-install.sh`](https://github.com/ncbi/vadr/blob/master/documentation/install.md#install)
  * [Setting environment variables](https://github.com/ncbi/vadr/blob/master/documentation/install.md#environment)
  * [Verifying successful installation](https://github.com/ncbi/vadr/blob/master/documentation/install.md#tests)
  * [Further information](https://github.com/ncbi/vadr/blob/master/documentation/install.md#further)
* [`v-build.pl` example usage and command-line options](https://github.com/ncbi/vadr/blob/master/documentation/build.md#top)
  * [`v-build.pl` example usage](https://github.com/ncbi/vadr/blob/master/documentation/build.md#exampleusage)
  * [`v-build.pl` command-line options](https://github.com/ncbi/vadr/blob/master/documentation/build.md#options)
  * [Building a VADR model library](https://github.com/ncbi/vadr/blob/master/documentation/build.md#library)
  * [How the VADR 1.0 model library was constructed](https://github.com/ncbi/vadr/blob/master/documentation/build.md#1.0library)
* [`v-annotate.pl` example usage, command-line options and alert information](https://github.com/ncbi/vadr/blob/master/documentation/annotate.md#top)
  * [`v-annotate.pl` example usage](https://github.com/ncbi/vadr/blob/master/documentation/annotate.md#exampleusage)
  * [`v-annotate.pl` command-line options](https://github.com/ncbi/vadr/blob/master/documentation/annotate.md#options)
  * [Basic Information on `v-annotate.pl` alerts](https://github.com/ncbi/vadr/blob/master/documentation/annotate.md#alerts)
  * [Additional information on `v-annotate.pl` alerts](https://github.com/ncbi/vadr/blob/master/documentation/annotate.md#alerts2)
* [Explanations and examples of `v-annotate.pl` detailed alert and error messages](https://github.com/ncbi/vadr/blob/master/documentation/alerts.md#top)
  * [Output fields with detailed alert and error messages](https://github.com/ncbi/vadr/blob/master/documentation/alerts.md#files)
  * [Explanation of sequence and model coordinate fields in `.alt` files](https://github.com/ncbi/vadr/blob/master/documentation/alerts.md#coords)
  * [`toy50` toy model used in examples of alert messages](https://github.com/ncbi/vadr/blob/master/documentation/alerts.md#toy)
  * [Examples of different alert types and corresponding `.alt` output](https://github.com/ncbi/vadr/blob/master/documentation/alerts.md#examples)
  * [Posterior probability annotation in VADR output Stockholm alignments](https://github.com/ncbi/vadr/blob/master/documentation/alerts.md#pp)
* [VADR output file formats](https://github.com/ncbi/vadr/blob/master/documentation/formats.md#top)
  * [VADR output files created by all VADR scripts](https://github.com/ncbi/vadr/blob/master/documentation/formats.md#generic)
  * [`v-build.pl` output files](https://github.com/ncbi/vadr/blob/master/documentation/formats.md#build)
  * [`v-annotate.pl` output files](https://github.com/ncbi/vadr/blob/master/documentation/formats.md#annotate)
  * [VADR `coords` coordinate string format](https://github.com/ncbi/vadr/blob/master/documentation/formats.md#coords)
  * [VADR sequence naming conventions](https://github.com/ncbi/vadr/blob/master/documentation/formats.md#seqnames)


## Reference <a name="reference"></a>
* The recommended citation for using VADR is:
  Alejandro A Schäffer, Eneida L Hatcher, Linda Yankie, Lara Shonkwiler,
  J Rodney Brister, Ilene Karsch-Mizrachi, Eric P Nawrocki; *VADR:
  validation and annotation of virus sequence submissions to
  GenBank.* BMC Bioinformatics 21, 211
  (2020). https://doi.org/10.1186/s12859-020-3537-3

* This page was adapted for MeV from [Mpox virus annotation](https://github.com/ncbi/vadr/wiki/Mpox-virus-annotation)

---
