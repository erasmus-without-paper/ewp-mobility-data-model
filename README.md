WP3 Data Model
==============

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Summary
-------

This document describes the **data model**. This is basically a PDF document 
in E-R (Entity-Relationship) notation, describing the underlying information
structure the APIs expose.


Introduction
------------

The notation is as follows:

 * Entity and attribute names are in Initcaps With Spaces (e.g. Organization
   Unit and Institution Id). This translates to lowercase-with-hyphens in the
   XSDs (e.g. organization-unit and institution-id).

 * Entity and attribute names are sometimes abbreviated for diagram clarity.

 * Primary keys (identifiers) can consist of more than one attribute, are
   __underscored__, denoted by PK and positioned above the entity line.

 * Mandatory attributes are in **boldface**.

 * Relationships are usually 1:many, where the "many" end is denoted by
   a circle and "crow's feet", denoting "0 or more". The connected entities are
   called "owner" and "member" respectively. The relationship is implemented by
   **foreign key** attributes (denoted by FK) in the member entity.

 * Relationships can be identifying or non-identifying. If a relationship is
   identifying, it means the connection from member (in the "many" end) to
   owner **partly identifies** the member. Identifying relationships have a
   solid line, non-identifying relationships are dashed. NOTE: This may
   sometimes be deviated from if the number of foreign key attributes
   otherwise would become too large to produce a clear diagram.

 * Non-identifying relationships can be mandatory or optional. Mandatory
   relationships have two crossbars (|-|) at the owner end, denoting "minimum
   1, maximum 1". Optional relationships have a circle and a crossbar (O-|),
   denoting "minimum 0, maximum 1".


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
[discovery-api]: https://github.com/erasmus-without-paper/ewp-specs-api-discovery
[echo]: https://github.com/erasmus-without-paper/ewp-specs-api-echo
[error-handling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#error-handling
