# MapData Prompt Guidelines

## Effective Prompts for This Repository

### Data Query Prompts

**Good:**
- "Show me all districts in California"
- "What states are available in Japan?"
- "Find the boundary coordinates for Texas"

**Avoid:**
- "Show me places" (too vague)
- "Get map data" (unspecific about level)

### Data Manipulation Prompts

**Good:**
- "Add a new district to New York with these boundaries: ..."
- "Update the manifest.json for China to include a new state"
- "Validate all GeoJSON files in the usa folder"

**Avoid:**
- "Fix the data" (no specific issue)
- "Update everything" (no scope)

### Analysis Prompts

**Good:**
- "Which country has the most states?"
- "Calculate the bounding box for all districts in Florida"
- "Find states with 'Unknown' in their name"

## Prompt Patterns by Task

### 1. Exploration
```
"List all [countries|states|districts] in [location]"
"What is the structure of [filename]?"
"How many [features] are in [file]?"
```

### 2. Validation
```
"Validate the GeoJSON in [path]"
"Check if all states in manifest.json have corresponding folders"
"Verify coordinate format in [file]"
```

### 3. Modification
```
"Add [feature] to [file] with properties [props]"
"Rename [old_name] to [new_name] in [context]"
"Merge [file1] and [file2] into [output]"
```

### 4. Conversion
```
"Convert [file] from GeoJSON to [format]"
"Extract coordinates from [feature]"
"Generate a summary of [data]"
```

## Context Requirements

When working with this repository, always specify:

1. **Level**: Country, state, or district
2. **Location**: Which country/state you're referring to
3. **Action**: What you want to do (read, modify, validate)

## Error Prevention

### Before Modifying
- Always read the existing file first
- Check the manifest for correct folder names
- Verify the parent-child relationships

### Common Pitfalls
- Using spaces instead of underscores in folder names
- Forgetting to update manifest.json when adding states
- Mixing up latitude/longitude order in coordinates
