# LOPOS-UWB database management

This script provides three R functions to simplify the task of adding tags, devices, and plans into their respective SQL tables. Each function generates SQL `INSERT` statements for the given data.

## Functions Overview

### 1. `add_tags()`

**Purpose**: Generate SQL code to insert given tag IDs into the `tag` table.

**Parameters**:
- `tag_ids`: Vector of tag IDs.
- `group_values` (optional, default is `1` for all): Vector of group values for each tag ID.

```R
tags <- c(75, 79, 84)
add_tags(tags)
```

### 2. add_device()
**Purpose**: Generate SQL code to insert tag details into the device table.

**Parameters**:
- `tag_ids`: Vector of tag IDs.

```R
tags <- c(75, 79, 84)
add_device(tags)
```


### 3. add_plan()
**Purpose**: Generate SQL code to insert tag scenarios into the plan table.

**Parameters**:
- `tag_ids`: Vector of tag IDs.
- `interval_8`: (optional, default is 30): Interval for scenario 8.

```R
tags <- c(75, 79, 84)
add_plan(tags)
```

