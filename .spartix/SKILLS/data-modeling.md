# Skill: Data Modeling

## Name
data-modeling

## Version
1.0.0

## Description
Design and validate data models including entity-relationship diagrams, schema definitions, normalization analysis, and data dictionary creation. Covers relational, document, graph, and time-series data models with integrity constraint definitions.

## Parameters
- **model_type**: Type of data model (relational, document, graph, time-series, dimensional)
- **notation**: Modeling notation (ERD, UML, JSON Schema, Avro, Protobuf)
- **normalization_level**: Target normalization form (1NF, 2NF, 3NF, BCNF, denormalized)
- **constraints**: Integrity constraints to define (PK, FK, unique, check, not-null)

## Outputs
- Data model diagrams in the specified notation
- Schema definition files (DDL, JSON Schema, migration files)
- Data dictionary with field descriptions, types, and constraints
- Normalization analysis report with trade-off assessment

## Prerequisites
- Business requirements and entity definitions must be available from predecessor tasks
- Target database technology must be specified in the task packet
- Performance requirements must be defined for denormalization decisions

## Approved Categories
- 06_DATABASE_AND_DATA_FOUNDATION
- 18_BIG_DATA_ANALYTICS_AND_DISTRIBUTED_DATA

## Usage Rules
- All entities must have clearly defined primary keys and relationships
- Data types must be appropriate for the target database technology
- Denormalization decisions must be justified with performance evidence
