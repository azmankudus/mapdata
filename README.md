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

**94 countries** with hierarchical geographic data (country → state → district).

### Asia (48 countries)

| Country | Folder | States |
|---------|--------|--------|
| Afghanistan | `afghanistan/` | 34 |
| Armenia | `armenia/` | 11 |
| Azerbaijan | `azerbaijan/` | 2 |
| Bahrain | `bahrain/` | 4 |
| Bangladesh | `bangladesh/` | 8 |
| Bhutan | `bhutan/` | 20 |
| Brunei | `brunei/` | 4 |
| Cambodia | `cambodia/` | 25 |
| China | `china/` | 34 |
| Cyprus | `cyprus/` | 6 |
| Georgia | `georgia/` | 12 |
| India | `india/` | 36 |
| Indonesia | `indonesia/` | 34 |
| Iraq | `iraq/` | 18 |
| Israel | `israel/` | 6 |
| Japan | `japan/` | 48 |
| Jordan | `jordan/` | 12 |
| Kazakhstan | `kazakhstan/` | 16 |
| Korea (South) | `korea/` | 14 |
| Kuwait | `kuwait/` | 6 |
| Kyrgyzstan | `kyrgyzstan/` | 7 |
| Laos | `laos/` | 18 |
| Lebanon | `lebanon/` | 9 |
| Malaysia | `malaysia/` | 21 |
| Maldives | `maldives/` | 21 |
| Mongolia | `mongolia/` | 22 |
| Myanmar | `myanmar/` | 14 |
| Nepal | `nepal/` | 7 |
| North Korea | `north_korea/` | 11 |
| Oman | `oman/` | 7 |
| Pakistan | `pakistan/` | 7 |
| Palestine | `palestine/` | 2 |
| Philippines | `philippines/` | 17 |
| Qatar | `qatar/` | 8 |
| Saudi Arabia | `saudi_arabia/` | 14 |
| Singapore | `singapore/` | 5 |
| Sri Lanka | `sri_lanka/` | 9 |
| Syria | `syria/` | 14 |
| Taiwan | `taiwan/` | 22 |
| Tajikistan | `tajikistan/` | 5 |
| Thailand | `thailand/` | 78 |
| Timor-Leste | `timor_leste/` | 13 |
| Turkey | `turkey/` | 81 |
| Turkmenistan | `turkmenistan/` | 5 |
| United Arab Emirates | `united_arab_emirates/` | 7 |
| Uzbekistan | `uzbekistan/` | 14 |
| Vietnam | `vietnam/` | 64 |
| Yemen | `yemen/` | 22 |

### Europe (44 countries)

| Country | Folder | States |
|---------|--------|--------|
| Albania | `albania/` | 12 |
| Andorra | `andorra/` | 7 |
| Austria | `austria/` | 9 |
| Belarus | `belarus/` | 7 |
| Belgium | `belgium/` | 3 |
| Bosnia and Herzegovina | `bosnia_and_herzegovina/` | 3 |
| Bulgaria | `bulgaria/` | 28 |
| Croatia | `croatia/` | 21 |
| Czechia | `czechia/` | 14 |
| Denmark | `denmark/` | 5 |
| Estonia | `estonia/` | 15 |
| Finland | `finland/` | 19 |
| France | `france/` | 13 |
| Germany | `germany/` | 11 |
| Greece | `greece/` | 8 |
| Hungary | `hungary/` | 19 |
| Iceland | `iceland/` | 8 |
| Ireland | `ireland/` | 4 |
| Italy | `italy/` | 5 |
| Kosovo | `kosovo/` | 7 |
| Latvia | `latvia/` | 43 |
| Liechtenstein | `liechtenstein/` | 11 |
| Lithuania | `lithuania/` | 10 |
| Luxembourg | `luxembourg/` | 12 |
| Malta | `malta/` | 68 |
| Moldova | `moldova/` | 37 |
| Monaco | `monaco/` | 1 |
| Montenegro | `montenegro/` | 23 |
| Netherlands | `netherlands/` | 12 |
| North Macedonia | `north_macedonia/` | 8 |
| Norway | `norway/` | 11 |
| Poland | `poland/` | 16 |
| Portugal | `portugal/` | 20 |
| Romania | `romania/` | 42 |
| San Marino | `san_marino/` | 9 |
| Serbia | `serbia/` | 25 |
| Slovakia | `slovakia/` | 8 |
| Slovenia | `slovenia/` | 2 |
| Spain | `spain/` | 19 |
| Sweden | `sweden/` | 21 |
| Switzerland | `switzerland/` | 26 |
| Ukraine | `ukraine/` | 27 |
| United Kingdom | `united_kingdom/` | 4 |

### Americas (1 country)

| Country | Folder | States |
|---------|--------|--------|
| USA | `usa/` | 79 |

### Eurasia (1 country)

| Country | Folder | States |
|---------|--------|--------|
| Russia | `russia/` | 83 |

### Regional Summary

| Region | Countries |
|--------|-----------|
| South-Eastern Asia | 11 |
| Western Asia | 18 |
| Southern Asia | 8 |
| Eastern Asia | 5 |
| Central Asia | 5 |
| Western Europe | 10 |
| Northern Europe | 10 |
| Southern Europe | 16 |
| Eastern Europe | 8 |
| Americas | 1 |
| Eurasia | 1 |

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
