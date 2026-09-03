# Celestial Bodies Database

A relational PostgreSQL database that models the universe — galaxies, the stars within them, the planets that orbit those stars, and the moons that orbit those planets. Built as part of freeCodeCamp's Relational Database certification.

## Overview

The database captures a simple hierarchy:

```
galaxy → star → planet → moon
```

Each level references its parent through a foreign key, so every star belongs to a galaxy, every planet belongs to a star, and every moon belongs to a planet. A standalone `comet` table also stores a few well-known comets.

## Schema

| Table    | Columns |
|----------|---------|
| `galaxy` | `galaxy_id` (PK), `name`, `galaxy_type`, `has_life`, `distance_from_earth`, `age_in_millions_of_years` |
| `star`   | `star_id` (PK), `name`, `galaxy_id` (FK → galaxy), `age_in_millions_of_years`, `is_spherical`, `distance_from_earth` |
| `planet` | `planet_id` (PK), `name`, `star_id` (FK → star), `has_life`, `description`, `distance_from_earth` |
| `moon`   | `moon_id` (PK), `name`, `planet_id` (FK → planet), `is_spherical`, `age_in_millions_of_years`, `distance_from_earth` |
| `comet`  | `comet_id` (PK), `name`, `description`, `has_life` |

Every table uses an auto-incrementing primary key, enforces `NOT NULL` and `UNIQUE` constraints on key columns, and stores `name` as `VARCHAR`.

## Data

- 6 galaxies (including the Milky Way, Andromeda, and Triangulum)
- 8 stars (including the Sun, Sirius, and Betelgeuse)
- 14 planets (all 8 solar system planets, plus a few exoplanets)
- 22 moons (including Earth's Moon and the major moons of Jupiter and Saturn)
- 3 comets (Halley's Comet, Hale-Bopp, and NEOWISE)

## Setup

The full schema and data are in [`universe.sql`](./universe.sql). To rebuild the database locally:

```bash
psql -U postgres < universe.sql
```

This will create the `universe` database, all five tables, and populate them with the sample data.

## Built with

- PostgreSQL
- [freeCodeCamp Relational Database certification](https://www.freecodecamp.org/learn/relational-database/)
