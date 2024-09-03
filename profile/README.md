# This is the GH-Project for **„Die Entstehung des Bundes-Verfassungsgesetzes 1920“**

Its aim is to provide documents, commentaries and data in general concerning the genesis of the Austrian Bundes-Verfassungsgesetzes in the 1920s.


### The basic data-/work-flow is:
1. documents are getting scanned and images are being uploaded to [goobi](https://goobi-work.acdh.oeaw.ac.at/)
2. metadata for documents are collected in [baserow](https://baserow.acdh-dev.oeaw.ac.at/database/421/table/2289/8962)
3. The [import-workflow](https://github.com/bundesverfassung-oesterreich/bv-entities/actions/workflows/transcribus_import.yml) triggers the import of documents from goobi to Transkribus and triggers the automated transcription. This workflow is however just updating the metadata and then remotely triggering another dedicated [import workflow](https://github.com/bundesverfassung-oesterreich/bv-transkribus-import/actions/runs/8083115048/job/22085445552).
4. Documents are proof red in a basic manner inside Transkribus.
5. [Transkribus-Export workflow](https://github.com/bundesverfassung-oesterreich/bv-transkribus-export) periodically exports the documents from the repo. It only does so if the [baserow-metadata](https://baserow.acdh-dev.oeaw.ac.at/database/421/table/2289/8962) of the document contain the Transkribus ids of document. Otherwise it is being ignored. The resulting TEI-Xmls are saved it a [dedicated directory](https://github.com/bundesverfassung-oesterreich/bv-transkribus-export/tree/main/editions_source).
6. The generated TEI-Xmls are corrected manually using the framework and the xml-schema generated and provided via a [dedicated repo](https://github.com/bundesverfassung-oesterreich/bv-schema-framework), containing some automated distribution workflows and a pages instance to make schema, docu & framework accessible via https. To provide a strict separation of manually corrected files and automatically generated files, the latter are copied manually from the [source directory(]https://github.com/bundesverfassung-oesterreich/bv-transkribus-export/tree/main/editions_source) into [a repo only containing the manually corrected files](https://github.com/bundesverfassung-oesterreich/bv-working-data).
7. The resulting data get published via [a dedicated repo](https://github.com/bundesverfassung-oesterreich/bv-static). All files from the automated Transkribus export are getting published, but if the corresponding file is already present in the [repo only containing the manually corrected files](https://github.com/bundesverfassung-oesterreich/bv-working-data) the latter is used as source assuming it provides the better data quality.


### General Texts
General texts such as introductions etc. are written in docx format, uploaded to google-docs, transformed to xml and then published on the page via a [dedicated repo](https://github.com/bundesverfassung-oesterreich/bv-website-text-parser).


### Editors' commentaries
Editors' commentaries providing insights into document genesis, historical significance and juristic implications are going to be written as docx and transformed to xml [via a dedicated repository](https://github.com/bundesverfassung-oesterreich/bv-kelsendotx-parser).

### Schema and Framework
All the data and most of the workflows are in the according repository. However some of the values in the dropdowns of author-mode (ids etc.) are provided via the schema (closed value lists for attributes). There is a [workflow in bv-entities](https://github.com/bundesverfassung-oesterreich/bv-entities/actions/workflows/update_schema.yml) to fetch the current metadata from baserow and trigger the generation of the schema (and thus update the closed value lists) with these new data.
If the framework is changed a new version is automatically generated an distributed via gh-pages. If users have issue accessing the update, it can be triggered manually, via the help-submenu in Oxygen.


### Noske
There is a [small repo](https://github.com/bundesverfassung-oesterreich/bv-noske), containing a bunch of scripts to build and deploy a Noske container to provide the data as corpus [a Noske instance](https://bvg-main.acdh-dev.oeaw.ac.at/crystal/#open). There is a [forked repo](https://github.com/bundesverfassung-oesterreich/gl-autodevops-minimal-port) managing the container-delpoyment in the cluster. It shouldn't be necessary to touch it in any way.

### .github repo
This repo only provides this README for the project page.
