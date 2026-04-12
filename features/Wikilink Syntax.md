# Wikilink Syntax Reference

This page documents all supported `[[wikilink]]` syntax and uses real wikilinks to demonstrate each feature.

## Basic Wikilinks

- [[Backlinks]] — basic filename match
- [[Search]] — another basic match
- [[Knowledge Graph]] — filename with spaces

## With .md Extension

These should resolve the same as without `.md`:

- [[Backlinks.md]] — with .md suffix
- [[Search.md]] — with .md suffix
- [[Knowledge Graph.md]] — with .md and spaces

## Aliased Links

- [[Backlinks|Learn about backlinks]] — alias display text
- [[Search|Full-text search feature]] — alias display text

## Path-Based Links

- [[features/Backlinks]] — partial path match
- [[getting-started/Quick Start]] — cross-folder path match

## Heading Anchors

- [[Backlinks#Wikilink Syntax]] — jump to a specific heading in another file
- [[Backlinks#Link Resolution Rules]] — jump to another heading
- [[Search#Search Tips]] — heading in Search page

## Same-File Anchors

- [[#Basic Wikilinks]] — jump to heading above
- [[#With .md Extension]] — jump to another section
- [[#Heading Anchors]] — jump to heading anchors section

## Combined: Heading + Alias

- [[Backlinks#Wikilink Syntax|Wikilink syntax details]] — file + heading + alias
- [[Search#Search Tips|How to search]] — another combined example

## Cross-Repo Links

If you have multiple repos synced, wikilinks resolve across repos:

- Same-repo matches take priority
- If no match in current repo, other synced repos are searched

## Unresolved Links

- [[NonExistent Page]] — this should show as unresolved (different style)
- [[Also Does Not Exist|broken link]] — unresolved with alias

## Edge Cases

- [[README]] — matches README.md in repo root
- [[Backlinks.MD]] — case-insensitive .md extension
