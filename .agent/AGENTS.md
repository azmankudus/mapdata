# MapData Agent Context

## Project Overview

This repository stores hierarchical geographic boundary data in GeoJSON format. The data follows a three-level hierarchy: Country → State/Province → District.

## Architecture

### Directory Structure
```
mapdata/
├── world.json                 # Level 1: All countries
├── {country}/                 # Country folder (lowercase, underscores)
│   ├── manifest.json          # State name → folder name mapping
│   ├── states.json            # Level 2: States/provinces
│   └── {state}/               # State folder (title case, underscores for spaces)
│       └── districts.json     # Level 3: Districts/counties
```

### Data Flow
1. `world.json` contains all country boundaries
2. Each country folder contains state-level data
3. Each state folder contains district-level data

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

- china (35 states)
- germany
- greece (10 states)
- japan (48 states)
- korea (14 states)
- malaysia
- russia
- saudi_arabia
- thailand (80+ states)
- usa (50+ states)

## File Size Notes

- `world.json` is ~9MB (contains all countries)
- State files vary in size based on boundary complexity
- District files contain the most granular data
