Data Model is up to date
========================

The data model has been updated with respect to the current XML schemas.

Data Model
==========

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]

Summary
-------

This document describes the **data model**. This is basically a PDF document 
in E-R (Entity-Relationship) notation, describing the underlying information
structure the APIs expose. The data model is a conceptual description across
XML schemas, not an accurate depiction of each schema (which only exposes a
partial truth).

Changes since June 2018
-----------------------

General
* The many:many relationship notation has been changed from "crow’s feet"
  to a black circle at each end, to make the diagram more compact
* Foreign keys that are the result of the modeling tool (rather than
  reflecting the schemas) are removed (e.g. sign Role/Person in IIA Partner)

IIA
* A PDF attribute has been added

Mobility Spec
* All attributes are now optional
* Avg Months/Days has been renamed to Tot Months/Days
* Added attribute Blended
* ISCED Code has been renamed to Subj Area/ISCED and been marked with a '*'
* Many:many relationships Send/Recv OU have been added

Contact/Fact Sheet
* Foreign key AT Start/End Date has been removed

Person
* Position has been removed and Global ID added

Mobility
* Entity has been renamed to Mobility/Learning Agreement
* IIA reference is now mandatory
* Send/Recv HEI/OUnit have been renamed to Send/Recv Partner, corresponding
  to the relationships to IIA Partner
* Relationships directly to Institution/Organization Unit have been removed
* Added attribute URL* (Outc,Prov)

Snapshot
* Entity has been renamed to LA Version
* Snapshot Type has been renamed to Version and the list of values has been
  changed
* Attributes In Effect since, Approval* and Shd Be Appr By* have been
  replaced by Stnt Approv Sign, Send Approv Sign and Recv Approv Sign

Component
* Added attribute Recog Cond
* Expanded list of Component Types

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
   relationships, the relationship is represented by a line with black circles
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
   and/or a description. The abstract Role attribute represents the different
   "roles" this information may play in connection with other entities, e.g.
   an Institution can have a Street Address, a Mailing Address, a Logo URL and
   sets of Website URLs, Mobility Fact Sheet URLs and Contacts - all of which
   are modelled by the same abstract entity. It may be connected to a Person
   (denoting contact info for that person), an Academic Term, an Inst/Org Unit
   (denoting fact sheet info), a set of IIA Partners or Mobility Specs. HEIs
   are **not** expected to implement this generalized structure.


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
[discovery-api]: https://github.com/erasmus-without-paper/ewp-specs-api-discovery
[echo]: https://github.com/erasmus-without-paper/ewp-specs-api-echo
[error-handling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#error-handling
