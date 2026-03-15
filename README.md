# MapData

A hierarchical geographic data repository storing GeoJSON boundaries for countries, states/provinces, and districts.

## Structure

```
mapdata/
├── countries.json          # World countries (FeatureCollection)
├── continents.json         # Continent/subcontinent mappings
├── {country}/
│   ├── manifest.json       # State name → folder name mapping
│   ├── states.json         # State/province boundaries (FeatureCollection)
│   └── {state}/
│       └── districts.json  # District boundaries (FeatureCollection)
```

## Supported Countries

| Country | Folder | States |
|---------|--------|--------|
| Brunei | `brunei/` | 4 |
| Cambodia | `cambodia/` | 25 |
| China | `china/` | 35 |
| Germany | `germany/` | 11 |
| Greece | `greece/` | 10 |
| Indonesia | `indonesia/` | 34 |
| Japan | `japan/` | 48 |
| Korea | `korea/` | 14 |
| Laos | `laos/` | 18 |
| Malaysia | `malaysia/` | 22 |
| Myanmar | `myanmar/` | 14 |
| Philippines | `philippines/` | 17 |
| Russia | `russia/` | 83 |
| Saudi Arabia | `saudi_arabia/` | 14 |
| Singapore | `singapore/` | 5 |
| Thailand | `thailand/` | 80 |
| Timor-Leste | `timor_leste/` | 13 |
| USA | `usa/` | 51 |
| Vietnam | `vietnam/` | 64 |

### Regional Coverage

**Southeastern Asia (10 countries):**
- Brunei, Cambodia, Indonesia, Laos, Malaysia, Myanmar, Philippines, Singapore, Thailand, Timor-Leste, Vietnam

**East Asia (4 countries):**
- China, Japan, Korea, Taiwan

**Europe (2 countries):**
- Germany, Greece

**Middle East (1 country):**
- Saudi Arabia

**Americas (1 country):**
- USA

**Eurasia (1 country):**
- Russia

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
const countries = require('./countries.json');

// Load continent mappings
const continents = require('./continents.json');

// Get continent info for a country
const info = continents.countryMap['Indonesia'];
// { continent: 'Asia', subcontinent: 'South-Eastern Asia' }

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
