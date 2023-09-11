# LOPOS-UWB database management

This script provides three R functions to simplify the task of adding tags, devices, and plans into their respective SQL tables. Each function generates SQL `INSERT` statements for the given data.

## Functions Overview

### 1. `add_tags()`

**Purpose**: Generate SQL code to insert given tag IDs into the `tag` table. In case of duplicates, the data will be updated based on the new input.

**Parameters**:
- `tag_ids`: Vector of tag IDs.
- `group_values` (optional, default is `1` for all): Vector of group values for each tag ID.

**Example**:
```R
tags <- c(75, 79, 84)
add_tags(tags)
```

**Output**:
```sql
INSERT INTO tag (id, addr, `group`) VALUES
(75, 4171, 1),
(79, 4175, 1),
(84, 4180, 1)
ON DUPLICATE KEY UPDATE addr=VALUES(addr), `group`=VALUES(`group`);
```

### 2. add_device()
**Purpose**: Generate SQL code to insert tag details into the device table. Duplicate entries will be ignored.

**Parameters**:
- `tag_ids`: Vector of tag IDs.

**Example**:
```R
tags <- c(75, 79, 84)
add_device(tags)
```
**Output**:
```sql
INSERT IGNORE INTO device (addr, mac, vbattATdfu, added, uwbTxPower) VALUES
(4171, 'tag75', 3.000, '2023-09-02 10:15:25', 0),
(4175, 'tag79', 3.000, '2023-09-02 10:15:25', 0),
(4180, 'tag84', 3.000, '2023-09-02 10:15:25', 0);
```


### 3. add_plan()
**Purpose**: Generate SQL code to insert tag scenarios into the plan table. In case of duplicates, the interval for the existing scenario will be updated based on the new input.

**Parameters**:
- `tag_ids`: Vector of tag IDs.
- `interval_8`: (optional, default is 30): Interval for scenario 8.

**Example**:
```R
tags <- c(75, 79, 84)
add_plan(tags)
```
**Output**:
```sql
INSERT INTO plan (addr, scenario, `interval`) VALUES
(4171, 8, 30),
(4171, 12, 60),
(4175, 8, 30),
(4175, 12, 60),
(4180, 8, 30),
(4180, 12, 60)
ON DUPLICATE KEY UPDATE `interval`=VALUES(`interval`) ;
```


