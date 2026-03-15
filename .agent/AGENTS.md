# MapData Agent Context

## Project Overview

This repository stores hierarchical geographic boundary data in GeoJSON format. The data follows a three-level hierarchy: Country → State/Province → District.

## Architecture

### Directory Structure
```
mapdata/
├── countries.json              # Level 1: All countries (GeoJSON)
├── continents.json             # Continent/subcontinent mappings
├── {country}/                  # Country folder (lowercase, underscores)
│   ├── manifest.json           # State name → folder name mapping
│   ├── states.json             # Level 2: States/provinces
│   └── {state}/                # State folder (title case, underscores for spaces)
│       └── districts.json      # Level 3: Districts/counties
```

### Data Flow
1. `countries.json` contains all country boundaries (GeoJSON FeatureCollection)
2. `continents.json` contains continent/subcontinent mappings and centroids
3. Each country folder contains state-level data
4. Each state folder contains district-level data

## Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Country folders | lowercase, underscores | `saudi_arabia/` |
| State folders | Title_Case, underscores | `New_York/`, `North_Carolina/` |
| JSON files | lowercase | `manifest.json`, `states.json`, `districts.json` |

## GeoJSON Schema

### FeatureCollection Structure
```typescript
interface FeatureCollection {
  type: "FeatureCollection";
  features: Feature[];
}

interface Feature {
  type: "Feature";
  id?: string;
  properties: {
    name: string;
    parent_state?: string;
    [key: string]: any;
  };
  geometry: Polygon | MultiPolygon;
}
```

### Geometry Types
- `Polygon`: Single closed boundary
- `MultiPolygon`: Multiple disjoint boundaries (e.g., islands)

## Common Tasks

### Adding a New Country
1. Create folder: `{country_name}/`
2. Add `manifest.json` with state mappings
3. Add `states.json` with state boundaries
4. Create state subdirectories with `districts.json`

### Adding a New State
1. Add entry to country's `manifest.json`
2. Create state folder
3. Add `districts.json` with district boundaries
4. Update `states.json` to include the state feature

## Validation Rules

1. All JSON must be valid
2. All features must have valid GeoJSON geometry
3. Coordinates follow [longitude, latitude] order (WGS84)
4. State names in manifest must match properties in states.json
5. District `parent_state` property should match state name

## Countries Currently Supported

**51 countries** organized by region:

### Asia (48 countries)

**South-Eastern Asia (11):**
- brunei (4 states)
- cambodia (25 states)
- indonesia (34 states)
- laos (18 states)
- malaysia (21 states)
- myanmar (14 states)
- philippines (17 states)
- singapore (5 states)
- thailand (78 states)
- timor_leste (13 states)
- vietnam (64 states)

**Western Asia (18):**
- armenia (11 states)
- azerbaijan (2 states)
- bahrain (4 states)
- cyprus (6 states)
- georgia (12 states)
- iraq (18 states)
- israel (6 states)
- jordan (12 states)
- kuwait (6 states)
- lebanon (9 states)
- oman (7 states)
- palestine (2 states)
- qatar (8 states)
- saudi_arabia (14 states)
- syria (14 states)
- turkey (81 states)
- united_arab_emirates (7 states)
- yemen (22 states)

**Southern Asia (8):**
- afghanistan (34 states)
- bangladesh (8 states)
- bhutan (20 states)
- india (36 states)
- maldives (21 states)
- nepal (7 states)
- pakistan (7 states)
- sri_lanka (9 states)

**Eastern Asia (5):**
- china (34 states)
- japan (48 states)
- korea (14 states)
- mongolia (22 states)
- north_korea (11 states)
- taiwan (22 states)

**Central Asia (5):**
- kazakhstan (16 states)
- kyrgyzstan (7 states)
- tajikistan (5 states)
- turkmenistan (5 states)
- uzbekistan (14 states)

### Europe (2 countries)
- germany (11 states)
- greece (8 states)

### Americas (1 country)
- usa (79 states)

### Eurasia (1 country)
- russia (83 states)

## File Size Notes

- `countries.json` is ~9MB (contains all countries as GeoJSON)
- `continents.json` is ~10KB (continent mappings and centroids)
- State files vary in size based on boundary complexity
- District files contain the most granular data
