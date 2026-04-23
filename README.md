# GenericGridSystem

A simple generic 2D grid for Unity. Store any type on a grid with world-space conversion, movement helpers, and reverse lookups.

## Installation

Add via Unity Package Manager using the Git URL:
```
https://github.com/MegaMulti/GenericGridSystem.git
```

## Quick Start

```csharp
using MegaMulti.GenericGridSystem;

// Create a 10x10 grid with 1x1 cells
var grid = new GenericGrid<string>(10, 10);

// Or with custom cell size and world offset
var grid = new GenericGrid<string>(10, 10, new Vector2(2f, 2f), new Vector3(5f, 0f, 0f));

// Set, get, remove
grid.Set(0, 0, "Player");
string value = grid.Get(0, 0);
grid.Remove(0, 0);

// Move
grid.MoveRight(0, 0);   // x + 1
grid.MoveLeft(0, 0);    // x - 1
grid.MoveUp(0, 0);      // y + 1
grid.MoveDown(0, 0);    // y - 1

// World ↔ Grid conversion
Vector3 worldPos = grid.CalculateWorldPosition(2, 3);
Vector2Int gridPos = grid.CalculateGridPosition(worldPos);

// Clear everything
grid.Clear();
```

## API Reference

### Constructors
| Constructor | Description |
|---|---|
| `GenericGrid(width, height)` | Creates a grid with 1x1 cells and no offset. |
| `GenericGrid(width, height, cellSize, offset)` | Creates a grid with custom cell size and world offset. |

> Set `width` or `height` to `0` for an unlimited axis.

### Get / Set / Remove
| Method | Description |
|---|---|
| `Set(x, y, value)` | Places a value at the given position. |
| `Get(x, y)` | Returns the value at the position, or `default` if empty. |
| `Remove(x, y)` | Removes the value at the position. |
| `Remove(value)` | Removes a value by reverse lookup. |
| `Contains(x, y)` | Returns `true` if the cell is occupied. |
| `Contains(value)` | Returns `true` if the value exists on the grid. |

> All methods also accept `Vector2Int` or `Vector3` (world position) overloads.
> Each value can only exist at **one position** at a time.

### Movement
| Method | Description |
|---|---|
| `Move(fromX, fromY, toX, toY)` | Moves a value to a new cell. Ignored if destination is occupied. |
| `MoveDirection(x, y, dirX, dirY)` | Moves by a direction offset. |
| `MoveUp/Down/Left/Right(x, y)` | Moves one cell in a cardinal direction. |

### Coordinate Conversion
| Method | Description |
|---|---|
| `CalculateWorldPosition(x, y)` | Converts grid coordinates to world space. |
| `CalculateGridPosition(worldPos)` | Converts a world position to grid coordinates. |
| `GetGridPosition(value)` | Gets the grid position of a value (reverse lookup). |
| `GetWorldPosition(value)` | Gets the world position of a value (reverse lookup). |
| `IsPositionValid(x, y)` | Returns `true` if the position is within bounds. |

### Enumeration
| Method | Description |
|---|---|
| `GetAllCells()` | Returns all stored values. |
| `GetAllPositions()` | Returns all occupied grid positions. |
| `GetAllKeyValuePairs()` | Returns all position-value pairs. |