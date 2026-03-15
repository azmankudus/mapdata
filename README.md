# MapData

A hierarchical geographic data repository storing GeoJSON boundaries for countries, states/provinces, and districts.

## Structure

```
mapdata/
├── world.json              # World countries (FeatureCollection)
├── {country}/
│   ├── manifest.json       # State name → folder name mapping
│   ├── states.json         # State/province boundaries (FeatureCollection)
│   └── {state}/
│       └── districts.json  # District boundaries (FeatureCollection)
```

## Supported Countries

| Country | Folder |
|---------|--------|
| China | `china/` |
| Germany | `germany/` |
| Greece | `greece/` |
| Japan | `japan/` |
| Korea | `korea/` |
| Malaysia | `malaysia/` |
| Russia | `russia/` |
| Saudi Arabia | `saudi_arabia/` |
| Thailand | `thailand/` |
| USA | `usa/` |

## Data Format

All geometry files use GeoJSON `FeatureCollection` format:

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "id": "unique_id",
      "properties": {
        "name": "Region Name",
        "parent_state": "Parent State"
      },
      "geometry": {
        "type": "Polygon",
        "coordinates": [[[lon, lat], ...]]
      }
    }
  ]
}
```

### Manifest Format

`manifest.json` maps state display names to folder names:

```json
{
  "New York": "New_York",
  "North Carolina": "North_Carolina"
}
```

## Usage

```javascript
// Load world countries
const world = require('./world.json');

// Load US states
const usStates = require('./usa/states.json');

// Load California districts
const caDistricts = require('./usa/California/districts.json');

// Get state folder from manifest
const manifest = require('./usa/manifest.json');
const folder = manifest['California']; // 'California'
```

## License

MIT License - Copyright (c) 2026 Azman Kudus
