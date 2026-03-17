# KRL Math Library

A comprehensive 3D mathematics and geometry library written in **KUKA KRL** for industrial robot programming. Provides vector algebra, matrix operations, rotations, planes, and pose transformations tailored to KUKA robot controllers.

## Project Structure

```
MATH/
├── UTILS.dat                 # Utils types
├── UTILS.src                 # Robot-specific utilities (HOME projection, frame conversion)
├── ALGEBRA/
│   ├── ALGEBRA.dat           # Algebra types
│   ├── VECTOR3.src           # 3D vector operations
│   └── MATRIX3.src           # 3x3 matrix operations
└── GEOMETRY/
    ├── GEOMETRY.dat          # Geometry types
    ├── ROTATION3D.src        # 3D rotation operations (Euler angles, axis rotations)
    ├── PLANE3D.src           # 3D plane operations
    └── POSE3D.src            # 3D pose transformations
```

## Modules

### Algebra

#### VECTOR3

3D vector mathematics with 24 functions:

- **Constructors** — `CREATE_VECTOR3`, `VECTOR3_ZERO`, `VECTOR3_UNIT_X`, `VECTOR3_UNIT_Y`, `VECTOR3_UNIT_Z`
- **Arithmetic** — `VECTOR3_ADD`, `VECTOR3_SUBTRACT`, `VECTOR3_NEGATE`, `VECTOR3_SCALE`, `VECTOR3_MULT_COMPONENT`
- **Products** — `VECTOR3_DOT`, `VECTOR3_CROSS`, `VECTOR3_OUTER`
- **Analysis** — `VECTOR3_NORM`, `VECTOR3_DISTANCE`, `VECTOR3_ANGLE`
- **Transforms** — `VECTOR3_NORMALIZE`, `VECTOR3_PROJECTION`, `VECTOR3_REJECTION`, `VECTOR3_REFLECT`, `VECTOR3_LERP`
- **Utilities** — `VECTOR3_SKEW`

#### MATRIX3

3x3 matrix operations with 18 functions:

- **Constructors** — `CREATE_MATRIX3`, `MATRIX3_ZERO`, `MATRIX3_IDENTITY`, `MATRIX3_DIAGONAL`
- **Accessors** — `MATRIX3_ROW`, `MATRIX3_COLUMN`
- **Arithmetic** — `MATRIX3_ADD`, `MATRIX3_MULT`, `MATRIX3_SCALE`
- **Properties** — `MATRIX3_TRACE`, `MATRIX3_DETERMINANT`, `MATRIX3_TRANSPOSE`
- **Advanced** — `MATRIX3_INVERSE`, `MATRIX3_COFACTOR`, `MATRIX3_ADJOINT`
- **Utilities** — `MATRIX3_MULT_VECTOR3`, `MATRIX3_IS_APPROX`, `MATRIX3_IS_IDENTITY`

### Geometry

#### ROTATION3D

3D rotations using Euler angles (KUKA ZYX convention: A, B, C) with 13 functions:

- **Conversions** — `EULER_TO_ROTATION3D`, `ROTATION3D_TO_EULER`, `FRAME_TO_ROTATION3D`
- **Axis rotations** — `ROTATION3D_X`, `ROTATION3D_Y`, `ROTATION3D_Z`
- **Composition** — `ROTATION3D_INVERSE`, `ROTATION3D_DIFFERENCE`
- **Analysis** — `ROTATION3D_GET_ANGLE`, `ROTATION3D_GET_X_ANGLE`, `ROTATION3D_GET_Y_ANGLE`, `ROTATION3D_GET_Z_ANGLE`
- **Validation** — `MATRIX3_IS_ROTATION3D`
- **Gimbal lock** handling included

#### PLANE3D

3D plane operations with 10 functions:

- **Constructors** — `CREATE_PLANE3D`, `POINTS_TO_PLANE3D`, `POSE3D_TO_PLANE`
- **Queries** — `PLANE3D_DISTANCE_POINT`, `PLANE3D_PROJECT_POINT`, `PLANE3D_ANGLE`
- **Intersections** — `PLANE3D_INTERSECT_LINE`
- **Transforms** — `PLANE3D_REFLECT_POINT`, `PLANE3D_TRANSFORM`, `PLANE3D_IS_PARALLEL`

#### POSE3D

3D pose (position + orientation) transformations with 13 functions:

- **Constructors** — `POSE3D_IDENTITY`, `CREATE_POSE3D`, `E6POS_TO_POSE3D`, `FRAME_TO_POSE3D`
- **Composition** — `POSE3D_TRANSFORM`, `POSE3D_INVERSE`, `POSE3D_DIFFERENCE`
- **Translations** — `POSE3D_TRANSLATE_LOCAL`, `POSE3D_TRANSLATE_WORLD`
- **Rotations** — `POSE3D_ROTATE`
- **Conversions** — `POSE3D_TO_FRAME`
- **Analysis** — `POSE3D_NORM`

### Utils

Robot-specific utility functions:

- `HOME_AS_POSE3D` — HOME position retrieval as `POSE3D`
- `PROJ_CURR_POSE_ON_HOME` — Current pose projection onto HOME planes
- `PROJECT_POSE_ON_PLANE` — Project 3D pose onto a plane

## Usage

Copy the `MATH/` folder into your KUKA robot controller project. Import the required modules in your KRL programs:

```krl
EXT CREATE_VECTOR3(REAL:IN, REAL:IN, REAL:IN):VECTOR3_T
EXT VECTOR3_ADD(VECTOR3_T:IN, VECTOR3_T:IN):VECTOR3_T
; ... declare the external functions you need
```

## Custom Types

The library defines the following types in `.dat` files:

| Type        | Description                      |
| ----------- | -------------------------------- |
| `VECTOR3_T` | 3D vector (X, Y, Z)              |
| `MATRIX3_T` | 3x3 matrix                       |
| `POSE3D_T`  | 3D pose (position + orientation) |
| `PLANE3D_T` | 3D plane (point + normal)        |

## Requirements

- KUKA KRC controller (KSS 8.x or compatible)
- KRL compiler

## License

[MIT](LICENSE)
