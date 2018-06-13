Data Model is up to date (with one exception)
=============================================

The data model has been updated with respect to the current XML schemas,
with one exception: The Learning Agreement Component change/snapshot
structures have never been part of the model, and still aren't. The
Learning Agreement and LA Component entities have been stripped of all
attributes, as these were suggestions not reflected in the XML schemas.

WP3 Data Model
==============

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Summary
-------

This document describes the **data model**. This is basically a PDF document 
in E-R (Entity-Relationship) notation, describing the underlying information
structure the APIs expose.


Notation
--------

 * The word "attribute" in this context is used as a "piece of information
   in an entity", **not** an XML attribute.

 * Entity and attribute names are in Initcaps With Spaces (e.g. Cooperation
   Condition and Mobility Type). This translates to lowercase-with-hyphens in
   the XSDs (e.g. cooperation-condition and mobility-type).

 * Entity and attribute names are sometimes abbreviated for diagram clarity.
   Attributes that naturally belong in pairs are often abbreviated to a single
   attribute with a slash (e.g. Start/End Date = Start Date + End Date).

 * Some attributes have one or more identifiers in parentheses, preceded by an
   optional asterisk. This means that the XML element corresponding to the main
   identifier has **XML** attribute(s) = the parenthesized identifier(s).
   If there is an asterisk present, the element can be repeated for different
   values of the XML attribute. E.g. "Name* (Lang)" means N names in different
   languages.

 * Primary keys (identifiers) can consist of more than one attribute, are
   underscored, denoted by PK and positioned above the entity line.

 * Mandatory attributes are in boldface.

 * Relationships are usually 1:many, where the "many" end is denoted by
   a circle and "crow's feet", denoting "0 or more". The connected entities are
   called "owner" and "member" respectively. The relationship is implemented by
   foreign key attributes (denoted by FK) in the member entity. Some
   relationships have labels, usually specifying a **role** (if there are more
   than one relationship between the entities in question and/or it's not
   self-evident what the relationship "means"). NOTE: The diagram tool keeps
   relationships and associated FK attributes in sync, which sometimes can lead
   to unnecessary constraints or clutter in the diagram (such as a large number
   of FK attributes, or unwanted optionality). In those cases, the FK mark on
   the attributes (or the FK attributes themselves) is/are removed.

 * Usually, primary keys are **natural** (and often composite). But in some
   cases, surrogate keys or UUIDs are used. In those cases, natural key
   constraints are are also represented, as alternate keys (marked "(AK)").

 * Relationships can be identifying or non-identifying. If a relationship is
   identifying, it means the connection from member (in the "many" end) to
   owner **partly identifies** the member. Identifying relationships have a
   solid line, non-identifying relationships are dashed. NOTE: When surrogate
   primary keys are used, the diagram loses any "identifying" information about
   incoming relationships (i.e. the relationships will always be marked as
   non-identifying, since the alternate keys aren't part of the primary key).
   In these cases, the notation is "fudged" by drawing the (non-identifying)
   relationships in **bold**, to indicate that they are "really" identifying.

 * Non-identifying relationships can be mandatory or optional. Mandatory
   relationships have two crossbars (|-|) at the owner end, denoting "minimum
   1, maximum 1". Optional relationships have a circle and a crossbar (O-|),
   denoting "minimum 0, maximum 1".

 * Recursive relationships (from an entity to itself) implement a **hierarchy**.
   Other relationships referencing this entity can point to any level in the
   hierarchy. Exceptions are explicitly stated on the relationship in
   parentheses - e.g. "(always institution)".

 * Many:many relationships are implemented as a separate entity connecting the
   two entities in question, via identifying relationships: If entity A has a
   many:many relationship to entity B, it's realized by an intermediate entity
   AB, with up to a x b occurrences (where a and b are the number of occurrences
   in A and B, respectively). Such relationships are sometimes represented in an
   abbreviated form for diagram clarity: Instead of an extra entity and two
   relationships, the relationship is represented by a line with "crow's feet"
   at each end, and the name of the intermediate entity on the line itself.
   (Note: This is only done when the extra entity doesn't contain any significant
   information itself.)


Special entities
----------------
 * **Inst/Org Unit** models both Institution and Department: It has a recursive
   relationship, implementing a hierarchy where the top level is the institution
   itself. Some attributes marked as mandatory may only be mandatory for the
   Institution level. For these attributes, Departments will have default values
   = those of the Institution they belong to.

 * **IIA** models an abstract global Inter-Institutional Agreement, but this
   doesn't exist: In reality, IIAs are local to each HEI, and it's up to the
   HEIs to match relevant local HEIs and make sure they describe the same
   agreement (see https://github.com/erasmus-without-paper/ewp-specs-api-iias).

 * **Contact/Fact Sheet** is a generalized "information" entity containing
   contact info (email address, URL, address, phone etc) and/or a name/label
   and/or a description. It may be connected to a Person (denoting contact info
   for that person), an Academic Term or just an Inst/Org Unit (denoting fact
   sheet info). HEIs are **not** expected to implement this generalized
   structure.


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
[discovery-api]: https://github.com/erasmus-without-paper/ewp-specs-api-discovery
[echo]: https://github.com/erasmus-without-paper/ewp-specs-api-echo
[error-handling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#error-handling
