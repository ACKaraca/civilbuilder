# Quantities, earthwork and mass haul

This area turns sections and model objects into quantities: material volumes by station, pay item
quantities, earthwork reports, and mass haul with balancing and haul planning.

## Domain objects

- **Quantity criteria**: a reusable definition of materials, their types and source mappings.
- **Material list**: materials computed for one sample line set.
- **Material**: type cut, fill, structure or quantity, with source surfaces or shape codes and factors.
- **Volume table**: per-station areas and incremental and cumulative volumes.
- **Pay item catalog** and **pay item assignment**: billing items and the rules that attach them to objects.
- **Mass haul line**, **mass haul view**, **borrow and waste site**, **free-haul setting**.

## Materials and volumes

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-QTY-001 | Quantity criteria | Criteria define material names, types (cut, fill, structure, quantity) and source mappings (surface pairs for earthwork, shape codes for structural layers). They are saved in libraries and applied to any sample line set. | T1 | 3 |
| CB-QTY-002 | Material lists | A material list computes areas per section and volumes between sections for every material, and regenerates when sections change, only between the affected sample lines. | T1 | 3 |
| CB-QTY-003 | Volume methods | Volumes compute by average end area, prismoidal formula or composite surface-to-surface method; a curvature correction for curved alignments is available. The method is shown on every report. | T1 | 3 |
| CB-QTY-004 | Cut and fill factors | Each material has shrink and swell factors; reports show adjusted and unadjusted volumes side by side. | T1 | 3 |
| CB-QTY-005 | Volume tables | Tables list per-station areas, incremental, cumulative and net volumes, placed in the model or on sheets, and update with the material list. | T1 | 3 |
| CB-QTY-006 | Earthwork reports | Reports summarize materials by station range, region or whole project as CSV, PDF or HTML from report templates. | T1 | 3 |
| CB-QTY-007 | Structural quantities | Pavement and base layer areas and volumes come from shape codes; lengths come from feature lines (for example curb length) and counts from objects. | T1 | 3 |
| CB-QTY-008 | Project volume summary | A summary aggregates volumes from surface comparisons, grading sets and corridors for the whole document, by material and status. | T2 | 4 |

## Pay items

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-QTY-009 | Pay item catalogs | Catalogs import from CSV or a documented structured format with item code, description, unit, category and optional unit price. A document may use several catalogs. | T2 | 4 |
| CB-QTY-010 | Pay item assignment | Pay items attach to corridor codes and shapes, network parts, symbols, linework, areas and points, manually or by rules on codes and properties. Rule-based assignments update when objects are added or changed. | T2 | 4 |
| CB-QTY-011 | Pay item formulas | A pay item quantity can be a formula over object properties (length, area, volume, count, user properties) in the shared expression language. | T2 | 4 |
| CB-QTY-012 | Quantity takeoff reports | Quantities report by item, station range, sheet frame or selection, and export as CSV and XLSX. | T2 | 4 |
| CB-QTY-013 | Quantity tables in sheets | Tables of pay item totals place in the model or on sheets and update with assignments. | T2 | 4 |
| CB-QTY-014 | Cost totals | Unit prices from catalogs multiply into cost totals per item and per design option; the product does not provide full cost estimating. | T3 | 4 |

## Mass haul

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-QTY-015 | Mass haul line | Cumulative adjusted volume is computed along stations from a material list, including borrow and waste sites placed at stations. | T2 | 4 |
| CB-QTY-016 | Balancing and overhaul | Free-haul distance, balance points, haul brackets and overhaul (volume times distance beyond free haul) are computed; borrow and waste sites have capacities. | T2 | 4 |
| CB-QTY-017 | Mass haul view | A graph shows the mass haul line with balance lines, free-haul and overhaul regions and labels, and regenerates with the material list. | T2 | 4 |
| CB-QTY-018 | Haul optimization | An optimizer assigns cut volumes to fill locations, borrow and waste sites to minimize total haul cost under capacity constraints and reports the resulting haul plan. | T3 | 4 |
