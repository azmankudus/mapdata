# MapData Skill Guidelines

## Available Skills

This repository does not require specialized skills. Standard file operations and JSON manipulation are sufficient.

## Recommended Workflows

### Workflow 1: Explore Geographic Data

```
1. Read world.json for country overview
2. Navigate to specific country folder
3. Read states.json for state list
4. Read manifest.json for folder mappings
5. Navigate to state folder for districts
```

### Workflow 2: Add New Geographic Data

```
1. Validate incoming GeoJSON structure
2. Check naming conventions match existing patterns
3. Add feature to appropriate JSON file
4. Update manifest.json if adding new state
5. Verify parent-child relationships are correct
```

### Workflow 3: Validate Data Integrity

```
1. Parse all JSON files for syntax errors
2. Verify GeoJSON schema compliance
3. Check coordinate arrays are valid
4. Ensure manifest entries have matching folders
5. Verify district parent_state matches state name
```

### Workflow 4: Extract Specific Data

```
1. Load target FeatureCollection
2. Filter features by property criteria
3. Extract required geometry/properties
4. Format output as needed
```

## Data Validation Checklist

- [ ] Valid JSON syntax
- [ ] Correct GeoJSON structure (type, features array)
- [ ] Each feature has required properties
- [ ] Geometry type is Polygon or MultiPolygon
- [ ] Coordinates are [longitude, latitude] pairs
- [ ] Coordinate arrays are properly nested
- [ ] Manifest keys match state names in states.json
- [ ] State folders exist for all manifest values
- [ ] District parent_state matches state name

## Coordinate Reference System

- **CRS**: WGS84 (EPSG:4326)
- **Order**: [longitude, latitude]
- **Format**: Decimal degrees

## Performance Considerations

| File Type | Typical Size | Loading Strategy |
|-----------|--------------|------------------|
| world.json | ~9MB | Stream or lazy load |
| states.json | 100KB-1MB | Direct load OK |
| districts.json | 10KB-500KB | Direct load OK |

## Extending the Repository

### Adding a New Country

1. Create country folder with lowercase name
2. Prepare GeoJSON data for states
3. Create manifest.json mapping
4. Create state subdirectories
5. Add district GeoJSON files

### Data Sources

When adding data, ensure:
- GeoJSON format compliance
- Consistent property naming
- Valid coordinate precision (6 decimal places sufficient)
- No duplicate features
