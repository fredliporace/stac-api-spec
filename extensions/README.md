# API Extensions

This folder contains extensions to the SpatioTemporal Asset Catalog API specification by providing  new OpenAPI fragments.

Anyone is welcome to create an extension (see section 'Extending STAC'), and is encouraged to at least link to the extension from here.
The third-party / vendor extension section is for the sharing of extensions. As third parties create useful extensions for their implementation
it is expected that others will make use of it, and then evolve to make it a 'community extension', that several providers maintain together.
For now anyone from the community is welcome to use this extensions/ folder of the stac-spec repository to collaborate.

## Extension Maturity

Extensions in this directory are meant to evolve to maturity, and thus may be in different states
in terms of stability and number of implementations. All extensions included must include a 
maturity classification, so that STAC spec users can easily get a sense of how much they can count
on the extension. 

| Maturity Classification |  Min Impl # | Description | Stability |
| ----------------------- | ----------- | ----------- | --------- |
| Proposal                | 0           | An idea put forward by a community member to gather feedback | Not stable - breaking changes almost guaranteed as implementers try out the idea. |
| Pilot                   | 1           | Idea is fleshed out, with examples and a JSON schema, and implemented in one or more catalogs. Additional implementations encouraged to help give feedback | Approaching stability - breaking changes are not anticipated but can easily come from additional feedback |
| Candidate               | 3           | A number of implementers are using it and are standing behind it as a solid extension. Can generally count on an extension at this maturity level | Mostly stable, breaking changes require a new version and minor changes are unlikely. |
| Stable                  | 6           | Highest current level of maturity. The community of extension maintainers commits to a STAC review process for any changes, which are not made lightly. | Completely stable, all changes require a new version number and review process. |
| Deprecated              | N/A         | A previous extension that has likely been superceded by a newer one or did not work out for some reason. | DO NOT USE, is not supported |

Maturity mostly comes through diverse implementations, so the minimum number of implementations
column is the main gating function for an extension to mature. But extension authors can also
choose to hold back the maturity advancement if they don't feel they are yet ready to commit to
the less breaking changes of the next level.

A 'mature' classification level will likely be added once there are extensions that have been 
stable for over a year and are used in twenty or more implementations.

## List of community extensions

| Extension Name                                         | Scope*         | Description | Maturity |
| ------------------------------------------------------ | -------------- | ----------- | -------- |
| [Fields](fields/README.md)                             | *None*         | Adds parameter to control which fields are returned in the response. | *Pilot* |
| [Filter](filter/README.md)                             | *None*         | Adds parameter to search Item and Collection properties, based on OGC CQL | *Pilot* |
| [Query](query/README.md)                               | *None*         | Adds parameter to search Item and Collection properties. | *Pilot* |
| [Context](context/README.md)                           | ItemCollection | Adds search related metadata (context) to ItemCollection. | *Proposal* |
| [Sort](sort/README.md)                                 | *None*         | Adds Parameter to control sorting of returns results. | *Pilot* |
| [Transaction](transaction/README.md)                   | *None*         | Adds PUT and DELETE endpoints for the creation, editing, and deleting of items and Collections. | *Pilot* |
| [Items and Collections API Version](version/README.md) | *None*         | Adds GET versions resource to collections and items endpoints and provides semantics for a versioning scheme for collections and items. | *Proposal* |

\* The scope refers to the STAC specifications an extension extends. As all extensions here are API extensions,
the API is not mentioned explicitly as scope and only the core STAC specifications (Catalog, Collection, Item and ItemCollection) are listed.

## Third-party / vendor extensions

The following extensions are provided by third parties (vendors). They tackle very specific
use-cases and may be less stable than the official extensions. Once stable and adopted by multiple
parties, extensions may be made official and incorporated in the STAC repository.

Please contact a STAC maintainer or open a Pull Request to add your extension to this table.

| Name     | Scope | Description | Vendor |
| -------- | ----- | ----------- | ------ |
| None yet |       |             |        |

## Proposed extensions

The following extensions are proposed through the
[STAC issue tracker](https://github.com/radiantearth/stac-api-spec/issues) and are considered to be
implemented. If you would find any of these helpful or are considering to implement a similar
extension, please get in touch through the referenced issues:

- None yet

## Creating new extensions

Creating new extensions requires creating an OpenAPI fragment to define it.

Example fragment:

```yaml
IntersectsFilter:
  type: object
  description: >-
    Only returns items that intersect with the provided polygon.
  properties:
    intersects:
      $ref: "#/definitions/Polygon"
Polygon:
  type: object
  properties:
    type:
      type: string
      enum:
        - polygon
    coordinates:
      $ref: "#/definitions/Polygon2D"
  required:
    - type
    - coordinates
Polygon2D:
  type: array
  minItems: 1
  items:
    $ref: "#/definitions/LinearRing2D"
LinearRing2D:
  type: array
  minItems: 4
  items:
    $ref: "#/definitions/Point2D"
  example: [[-104, 35], [-103, 35], [-103, 34], [-104, 34], [-104, 35]]
Point2D:
  description: A 2d geojson point
  type: array
  minimum: 2
  maximum: 2
  items:
    type: number
    format: double
  example:
    - -104
    - 35
```
