# Zero2Hero C Programming Database Viewer

A command-line employee database management system written in C. This project demonstrates file I/O, binary data serialization, and dynamic memory management.

## Features

- **Create Database Files** - Initialize new employee databases with proper headers
- **Add Employees** - Dynamically add employee records with name, address, and hours
- **List Employees** - View all employees stored in the database
- **Data Validation** - Verify database integrity with magic numbers and version checking
- **Network Byte Order** - Proper big-endian storage for cross-platform compatibility

## Usage

```bash
./bin/dbview -f <database_file> [OPTIONS]
```

### Options

| Flag | Description |
|------|-------------|
| `-f <path>` | Path to database file **(required)** |
| `-n` | Create a new database file |
| `-a "Name,Address,Hours"` | Add an employee to the database |
| `-l` | List all employees in the database |

### Examples

```bash
# Create a new database
./bin/dbview -n -f mydb.db

# Add an employee
./bin/dbview -f mydb.db -a "John Doe,123 Main St,40"

# List all employees
./bin/dbview -f mydb.db -l

# Add multiple employees
./bin/dbview -f mydb.db -a "Jane Smith,456 Oak Ave,35"
./bin/dbview -f mydb.db -l
```

## Building

```bash
make           # Build the project
```
## Database Format

The database uses a binary format with the following structure:

### Header (16 bytes)
- **Magic**: 0x4C4C4144 (validates file type)
- **Version**: 1 (current format version)
- **Count**: Number of employees
- **FileSize**: Total file size in bytes

### Employee Records
Each employee record contains:
- **Name**: 256-byte string
- **Address**: 256-byte string
- **Hours**: 4-byte unsigned integer (network byte order)