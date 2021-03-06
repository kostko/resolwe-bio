##########
Change Log
##########

All notable changes to this project are documented in this file.
This project adheres to `Semantic Versioning <http://semver.org/>`_.


==========
Unreleased
==========

Added
-----
* Amplicon workflow
* Amplicon descriptor schemas
* Amplicon report generator
* Add Rattus norvegicus organism choice to sample schema
* Transforming form Phred 64 to Phred 33 when uploading fastq reads
* Add primertrim process
* RNA-Seq experiment descriptor schema
* iCount sample and reads descriptor schemas
* iCount demultiplexing and sample annotation
* ICount QC
* Add MM8, RN4 and RN6 options to rose2 process
* Add RN4 and RN6 options to bamplot process
* Archive-samples process
* Add bamliquidator
* CheMut workflow
* Dicty primary analysis descriptor schema
* IGV session to Archive-samples process
* Use Resolwe's field projection mixins for knowledge base endpoints

Fixed
-----
* Use new import paths in ``resolwe.flow``
* Upload reads (paired/single) containing whitespace in the file name
* Fix reads filtering processes for cases where input read file names contain whitespace
* Add additional filtering option to STAR aligner
* Fix bbduk-star-htseq_count workflow
* Fix cuffnorm process: Use sample names as labels (boxplot, tables),
  remove group labels input, auto asign group labels, add outputs for
  Rscript output files which were only available compressed
* Derive output filenames in hisat2 from the first reads filename

Changed
-------
* Support Resolwe test framework
* Run tests in parallel with Tox
* Use Resolwe's new ``FLOW_DOCKER_COMMAND`` setting in test project
* Always run Tox's ``docs``, ``linters`` and ``packaging`` environments with
  Python 3
* Replace Travis CI with Genialis' Jenkins for running the tests
* Store compressed and uncompressed .fasta files in ``data:genome:fasta`` objects
* Change sample_geo descriptor schema to have strain option available for all organisms
* More readable rna-seq-quantseq schema, field stranded


================
1.3.0 2017-01-28
================

Changed
-------
* Add option to save expression JSON to file before saving it to Storage
* Update ``upload-expression`` process
* No longer treat ``resolwe_bio/tools`` as a Python package
* Move processes' test files to the ``resolwe_bio/tests/files`` directory
  to generalize and simplify handling of tests' files
* Update differential expression (DE) processors
* Update ``generate_diffexpr_cuffdiff`` django-admin command
* Save gene_id source to ``output.source`` for DE, expression and related objects
* Refactor ``upload-diffexp`` processor
* Update sample descriptor schema
* Remove obsolete descriptor schemas
* Add stitch parameter to rose2 processor
* Add filtering to DESeq2
* Set Docker Compose's project name to ``resolwebio`` to avoid name clashes
* GO enrichment analysis: map features using gene Knowledge base
* Add option to upload .gff v2 files with upload-gtf processor
* Replace Haystack with Resolwe Elastic Search API
* Require Resolwe 1.4.1+
* Update processes to be compatible with Resolwe 1.4.0

Added
-----
* Process definition documentation style and text improvements
* Add ``resolwe_bio.kb`` app, Resolwe Bioinformatics Knowledge Base
* Add tests to ensure generators produce the same results
* Upload Gene sets (``data:geneset``)
* Add ``generate_geneset`` django-admin command
* Add ``generate_diffexpr_deseq`` django-admin command
* Add 'Generate GO gene sets' processor
* Add generic file upload processors
* Add upload processor for common image file types (.jpg/.tiff/.png/.gif)
* Add upload processor for tabular file formats (.tab/.tsv/.csv/.txt/.xls/.xlsx)
* Add Trimmomatic process
* Add featureCounts process
* Add Subread process
* Add process for hierarchical clusteing of samples
* Add gff3 to gtf file converter
* Add microarray data descriptor schema
* Add process for differential expression edgeR
* ``BioCollectionFilter`` and ``BidDataFilter`` to support filtering collections
  and data by samples on API
* Added processes for automatically downloading single and paired end SRA files
  from NCBI and converting them to FASTQ
* Added process for automatically downloading SRA files from NCBI and converting
  them to FASTQ
* Add HEAT-Seq pipeline tools
* Add HEAT-Seq workflow
* Add ``create-geneset``, ``create-geneset-venn``  processors
* Add ``source`` filter to feature search endpoint
* Add bamplot process
* Add gene hiererhical clustering
* Add cuffquant workflow
* Support Django 1.10 and versionfield 0.5.0
* django-admin commands ``insert_features`` and ``insert_mappings`` for
  importing features and mappings to the Knowledge Base
* Add bsmap and mcall to analyse WGBS data
* Vaccinesurvey sample descriptor schema

Fixed
-----
* Set ``presample`` to ``False`` for Samples created on Sample endpoint
* Fix FastQC report paths in processors
* Fix ``htseq_count`` and ``featureCounts`` for large files
* Fix ``upload gtf annotation``
* Fix gene_id field type for differential expression storage objects
* Order data objects in ``SampleViewSet``
* Fix sample hiererhical clustering
* Fix name in gff to gtf process
* Fix clustering to read expressed genes as strings


================
1.2.1 2016-07-27
================

Changed
-------
* Update ``resolwe`` requirement


================
1.2.0 2016-07-27
================

Changed
-------
* Decorate all tests that currently fail on Docker with ``skipDockerFailure``
* Require Resolwe's ``master`` git branch
* Put packaging tests in a separate Tox testing environment
* Rename DB user in test project
* Change PostgreSQL port in test project
* Add ROSE2 results parser
* Compute index for HISAT2 aligner on genome upload
* Updated Cuffquant/Cuffnorm tools
* Change ROSE2 enhancer rank plot labels
* Refactor processor syntax
* Move processes tests into ``processes`` subdirectory
* Split ``sample`` API endpoint to ``sample`` for annotated ``Samples``
  and ``presample`` for unannotated ``Samples``
* Rename test project's data and upload directories to ``.test_data`` and
  ``.test_upload``
* Save fastq files to ``lists:basic:file`` field. Refactor related processors.
* Reference genome-index path when running aligners.
* Add pre-computed genome-index files when uploading reference fasta file.
* Include all necessary files for running the tests in source distribution
* Exclude tests from built/installed version of the package
* Move testing utilities from ``resolwe_bio.tests.processes.utils`` to
  ``resolwe_bio.utils.test``
* Update Cuffdiff processor inputs and results table parsing
* Refactor processes to use the updated ``resolwe.flow.executors.run`` command
* Refactor STAR aligner - export expressions as separate objects

Fixed
-----
* Make Tox configuration more robust to different developer environments
* Set ``required: false`` in processor input/output fields where necessary
* Add ``Sample``'s ``Data objects`` to ``Collection`` when ``Sample`` is added
* Fixed/renamed Cufflinks processor field names

Added
-----
* ``skipDockerFailure`` test decorator
* Expand documentation on running tests
* Use Travis CI to run the tests
* Add ``Sample`` model and corresponding viewset and filter
* Add docker-compose command for PostgreSQL
* API endpoint for adding ``Samples`` to ``Collections``
* HISAT2 aligner
* Use Git Large File Storage (LFS) for large test files
* Test for ``generate_samples`` django-admin command
* django-admin command: ``generate_diffexpr``


================
1.1.0 2016-04-18
================

Changed
-------
* Remove obsolete utilities superseded by resolwe-runtime-utils
* Require Resolwe 1.1.0

Fixed
-----
* Update sample descriptor schema
* Include all source files and supplementary package data in sdist

Added
-----
* ``flow_collection: sample`` to processes
* MACS14 processor
* Initial Tox configuration for running the tests
* Tox tests for ensuring high-quality Python packaging
* ROSE2 processor
* django-admin command: ``generate_samples``


================
1.0.0 2016-03-31
================

Changed
-------
* Renamed assertFileExist to assertFileExists
* Restructured processes folder hierarchy
* Removed re-require and hard-coded tools' paths

Fixed
-----
* Different line endings are correctly handled when opening gzipped files
* Fail gracefully if the field does not exist in assertFileExists
* Enabled processor tests (GO, Expression, Variant Calling)
* Enabled processor test (Upload reads with old Illumina QC encoding)
* Made Resolwe Bioinformatics work with Resolwe and Docker

Added
-----
* Import expressions from tranSMART
* Limma differential expression (tranSMART)
* VC filtering tool (Chemical mutagenesis)
* Additional analysis options to Abyss assembler
* API endpoint for Sample
* Initial documentation
