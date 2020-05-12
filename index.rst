..
  Technote content.

  See https://developer.lsst.io/restructuredtext/style.html
  for a guide to reStructuredText writing.

  Do not put the title, authors or other metadata in this document;
  those are automatically added.

  Use the following syntax for sections:

  Sections
  ========

  and

  Subsections
  -----------

  and

  Subsubsections
  ^^^^^^^^^^^^^^

  To add images, add the image file (png, svg or jpeg preferred) to the
  _static/ directory. The reST syntax for adding the image is

  .. figure:: /_static/filename.ext
     :name: fig-label

     Caption text.

   Run: ``make html`` and ``open _build/html/index.html`` to preview your work.
   See the README at https://github.com/lsst-sqre/lsst-technote-bootstrap or
   this repo's README for more info.

   Feel free to delete this instructional comment.

:tocdepth: 1

.. Please do not modify tocdepth; will be fixed when a new Sphinx theme is shipped.

.. sectnum::

.. TODO: Delete the note below before merging new content to the master branch.

.. note::

   **This technote is not yet published.**

   This technote describes the EFD Aggregator, a Kafka aggregator based on the Faust Python Stream Processing library.


Introduction
============

.. figure:: /_static/efd_aggregator.png
   :name: EFD Aggregator
   :target: _static/efd_aggregator.png

   Components of the EFD at the LSST Data Facility (LDF) showing the Aggregator, the Replicator and other connectors to write data from Kafka into InfluxDB, PostgreSQL and Parquet.


- The EFD aggregator is a Faust based application, Faust agents consume topics from Kafka and perform window aggregation on predefined topic fields, the window size is configurable `DM-24403 <https://jira.lsstcorp.org/browse/DM-24403>`_

- A new the aggregated topic is produced and its schema is registered in Secondary Schema Registry to avoid Schema ID collision `DM-24856 <https://jira.lsstcorp.org/browse/DM-24856>`_

- We plan on having a dedicated Kafka Connect cluster (2 nodes) to consume the full and/or aggregated streams and write to different formats using open source Kafka connectors. The InfluxDB Sink connector we currently use is from the stream-reactor project and both JDBC and Amazon S3 connectors are under the Confluent Community License.

- The system is flexible enough to record either the full or aggregated stream in multiple formats.

- We have successfully tested data replication using the Confluent Replicator connector `DM-23973 <https://jira.lsstcorp.org/browse/DM-23973>`_, but we are planning on replacing it by an open source alternative. The best option for now is Mirus `DM-24774 <https://jira.lsstcorp.org/browse/DM-24774>`_


.. Add content here.
.. Do not include the document title (it's automatically added from metadata.yaml).

.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
