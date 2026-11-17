# Pressure networks

This area designs water, force main and other pressurized systems in 3D: pipes, fittings and
appurtenances from catalogs, layout by cover, deflection rules, and documentation. Pressure
hydraulic analysis is specified in [hydrology and hydraulics](15-hydrology.md).

## Domain objects

- **Pressure network**: pipes, fittings and appurtenances with 3D connectivity.
- **Pressure part catalog**: materials, nominal sizes, pressure classes, bend angles and joint deflection limits.
- **Fitting**: bend, tee, cross, reducer, cap or coupling.
- **Appurtenance**: valve, hydrant, meter, pump or tapping connection.
- **Pressure rule set**: cover, deflection, bend radius and clearance rules.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-PRES-001 | Pressure network object | A network holds pipes, fittings and appurtenances with 3D connectivity and status (existing, proposed, to be removed). | T1 | 5 |
| CB-PRES-002 | Pressure part catalogs | Catalogs define materials (ductile iron, PVC, PE, steel, concrete) with nominal sizes, pressure classes, available bend angles and allowed joint deflection, stored as open text files. | T1 | 5 |
| CB-PRES-003 | Pressure layout | Pipes are laid along an alignment or freely in 3D; fittings insert automatically where deflection exceeds the allowed joint deflection; networks also create from linework and GIS features. | T1 | 5 |
| CB-PRES-004 | Vertical layout by cover | Pipes follow a surface at a cover depth with vertical bends inserted at grade changes, or follow a profile. | T1 | 5 |
| CB-PRES-005 | Pressure design rules | Minimum and maximum cover, maximum joint deflection, minimum bend radius and clearance rules are checked live with markers and a findings list. | T1 | 5 |
| CB-PRES-006 | Pressure network editing | Parts edit in plan and profile views; parts swap; pipes break and connect; appurtenances insert with automatic reconnection. | T1 | 5 |
| CB-PRES-007 | Display, labels and tables | Pressure networks display in plan, profile and section views with labels and tables through styles. | T1 | 5 |
| CB-PRES-008 | Crossing separation | Crossings with gravity networks and other utilities report vertical separation at each crossing point and take part in interference checks (CB-GRAV-011). | T1 | 5 |
| CB-PRES-009 | Pressure quantities | Lengths by size and material and fitting and appurtenance counts feed pay items and reports. | T1 | 5 |
| CB-PRES-010 | Thrust restraint | Restrained lengths or thrust block sizes are computed per fitting from test pressure and soil parameters. | T3 | 5 |
| CB-PRES-011 | Pressure network exchange | Networks export to IFC 4.3, GIS formats and an EPANET-class input file, and import from GIS asset data. | T1 | 5 |
