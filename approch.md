#### `JavaScript` implementation structure

```bash
@stdlib/blas/base/chemv
├── benchmark/                # Performance benchmarking suite
│   ├── benchmark.js            # Benchmark for standard JS interface
│   └── benchmark.ndarray.js    # Benchmark for ndarray interface
│
├── docs/               # Documentation and type definitions
│   ├── types/
│   │   ├── index.d.ts    # TypeScript type definitions
│   │   └── test.ts       # TypeScript type tests
│   └── repl.txt          # REPL usage examples
│
├── examples/     # Example usage
│   └── index.js    # Demonstrates how to use the routine
│
├── lib/              # JavaScript implementation layer
│   ├── base.js         # Pure JavaScript base implementation
│   ├── {routine}.js    # Main JavaScript wrapper (standard interface)
│   ├── index.js        # API entry point
│   ├── main.js         # Export logic
│   └── ndarray.js      # ndarray-based JavaScript implementation
│
├── test/                   # Test suite
│   ├── fixtures/            # Test data
│   ├── test.js              # General tests
│   ├── test.{routine}.js    # Tests for standard interface
│   └── test.ndarray.js      # Tests for ndarray interface
│
├── README.md       # Documentation and usage guide
└── package.json    # Package configuration
```

#### `C` implementation structure

```bash
@stdlib/blas/base/{routine}
├── benchmark/                  # Performance benchmarking suite
│   └── c/
│       ├── Makefile              # Build configuration for benchmarks
│       ├── benchmark.length.c    # Benchmarks for low-level strided ndarray
│       └── benchmark.c           # Core benchmark implementation
│
├── examples/
│   └── c/
│       ├── Makefile     # Build configuration for example
│       └── example.c    # Demonstrates how to call the routine in C
│
├── include/
│   └── stdlib/
│       └── blas/
│           └── base/
│               ├── {routine}.h          # C header for core and ndarray routine
│               └── {routine}_cblas.h    # Declares the CBLAS interface
│
├── lib/                     # JavaScript bindings (Node.js interface layer)
│   ├── {routine}.native.js    # JavaScript wrapper for native (C) implementation
│   ├── native.js              # Entry point for native bindings
│   └── ndarray.native.js      # ndarray-based JavaScript wrapper
│
├── src/                     # Core native (C) implementation
│   ├── Makefile               # Build commands for native code
│   ├── addon.c                # Node.js addon bridge (C and JavaScript binding)
│   ├── {routine}.c            # C wrapper for native (C) implementation
│   ├── {routine}_cblas.c      # CBLAS-compatible wrapper
│   └── {routine}_ndarray.c    # ndarray-based implementation
│
├── test/                         # Test suite
│   ├── fixtures/                   # Test data
│   ├── test.ndarray.native.js      # Tests for ndarray interface
│   └── test.{routine}.native.js    # Tests for core routine functionality
│
├── README.md        # Usage, API documentation, and examples
├── binding.gyp      # Node-gyp configuration for building native addon
├── include.gypi     # Shared build configuration (compiler flags, paths)
└── manifest.json    # Package metadata for stdlib tooling
```

#### Validating Results Against Reference Implementations

This example demonstrates validation of the `sgemv` implementation by comparing results against the reference implementation provided by `SciPy`.

**`stdlib` implementation**
```js
const sgemv = require('@stdlib/blas/base/sgemv');

var Float32Array = require( '@stdlib/array/float32' );

var A = new Float32Array( [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ] );
var x = new Float32Array( [ 1, 2, 3 ] );
var y = new Float32Array( [ 3, 2, 1 ] );

sgemv( 'row-major', 'no-transpose', 3, 3, 0.5 , A, 3, x, 1, -0.5, y, 1 );
console.log( y );
```

**Output**
```js
Float32Array(3) [ 5.5, 15, 24.5 ]
```

**`SciPy` implementation**
```py
import numpy as np
from scipy.linalg.blas import sgemv

A = np.array( [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ], dtype = np.float32 ).reshape( ( 3, 3 ), order='C' )

x = np.array( [ 1, 2, 3 ], dtype = np.float32 )
y = np.array( [ 3, 2, 1 ], dtype = np.float32 )

result = sgemv( 0.5, A, x, beta = -0.5, y = y )
print( result )
```

**Output**
```py
[ 5.5 15.  24.5]
```

#### **Level 2**

**Input Validation**

This table defines all parameter validation rules for Level 2 enforced before computation. These checks ensure correctness, prevent undefined memory access.

| Parameter          | Condition                                                  | Error Type   | Description                            |
|--------------------|------------------------------------------------------------|--------------|----------------------------------------|
| order              | valid layout (`row-major`/`column-major`)                  | TypeError    | Ensures correct memory interpretation  |
| uplo               | `upper` or `lower`                                         | TypeError    | Ensures correct triangular access      |
| trans              | valid (`no-transpose`, `transpose`, `conjugate-transpose`) | TypeError    | Ensures valid transpose operation      |
| M, N               | ≥ 0                                                        | RangeError   | Matrix dimensions must be non-negative |
| LDA                | ≥ max(1, M) or max(1, N) depending on layout               | RangeError   | Valid leading dimension                |
| strideA1, strideA2 | ≠ 0                                                        | RangeError   | Valid matrix traversal                 |
| strideX,strideY    | ≠ 0                                                        | RangeError   | Valid vector traversal                 |
| offsetA            | ≥ 0                                                        | RangeError   | Valid starting index for matrix        |
| offsetX            | ≥ 0                                                        | RangeError   | Valid starting index for vector `x`    |
| offsetY            | ≥ 0                                                        | RangeError   | Valid starting index for vector `y`    |

**Testing**

1. **General Layout Tests**

	Covers all transpose configurations across both memory layouts. 

	> Note: Conjugate transpose is only applicable to compatable complex valued routines.

	| Operation Mode      | Row-major Fixtures   | Column-major Fixtures |
	|---------------------|----------------------|-----------------------|
	| No Transpose        | `row_major_nt`       | `column_major_nt`     |
	| Transpose           | `row_major_t`        | `column_major_t`      |
	| Conjugate Transpose | `row_major_ct`       | `column_major_ct`     |

---

2. **General Layout Tests for triangular matrix**

	Validates correct handling of upper and lower triangular matrix regions.

	| Triangle (uplo) | Row-major Fixtures | Column-major Fixtures |
	|-----------------|--------------------|-----------------------|
	| Upper           | `row_major_u`      | `column_major_u`      |
	| Lower           | `row_major_l`      | `column_major_l`      |

---

3. **Scalar and Vector Edge Cases**

	Tests behavior under  scalar values (`α`, `β`) and vector conditions to ensure correct mathematical handling of degenerate cases.

	| α   | β   | x           | Row-major Fixtures              | Column-major Fixtures              |Result               |
	|-----|-----|-------------|---------------------------------|------------------------------------|---------------------|
	| 0   | any | any vector  | `row_major_alpha_zero`          | `column_major_alpha_zero`          | y scaled to β       |
	| 0   | 1   | any vector  | `row_major_alpha_zero_beta_one` | `column_major_alpha_zero_beta_one` | y remains unchanged |
	| any | any | zero vector | `row_major_x_zeros`             | `column_major_x_zeros`             | y scaled to β       |
	| any | 1   | zero vector | `row_major_x_zeros_beta_one`    | `column_major_x_zeros_beta_one`    | y remains unchanged |

---

4. **Vector Stride Handling Tests**

	Ensures correctness when traversing vectors with different stride directions.

	| strideX  | strideY  | Row-major Fixtures   | Column-major Fixtures |
	|----------|----------|----------------------|-----------------------|
	| positive | positive | `row-major_xpyp`     | `column-major_xpyp`   |
	| negative | positive | `row-major_xnyp`     | `column-major_xnyp`   |
	| positive | negative | `row-major_xpyn`     | `column-major_xpyn`   |
	| negative | negative | `row-major_xnyn`     | `column-major_xnyn`   |

---

5. **Offset Handling Tests**

	Verifies correct behavior when computations begin from non-zero memory offsets.

	| Test Condition | Row-major Fixture | Column-major Fixture |
	|----------------|-------------------|----------------------|
	| offsetA > 0    | `row_major_oa`    | `column_major_oa`    |

---

6. **Matrix Stride Handling Tests**

	Tests traversal of matrices with varying stride configurations.

	| strideA1 | strideA2 | Row-major Fixtures    | Column-major Fixtures    |
	|----------|----------|-----------------------|--------------------------|
	| positive | positive | `row-major_sa1_sa2`   | `column-major_sa1_sa2`   |
	| negative | positive | `row-major_sa1n_sa2`  | `column-major_sa1n_sa2`  |
	| positive | negative | `row-major_sa1_sa2n`  | `column-major_sa1_sa2n`  |
	| negative | negative | `row-major_sa1n_sa2n` | `column-major_sa1n_sa2n` |

---

7. **Complex Access Pattern Tests**

	Combines negative strides and offsets.

	| Layout       | strideX  | strideY  | offsetA | offsetX | offsetY | Fixture Name                          |
	|--------------|----------|----------|---------|---------|---------|---------------------------------------|
	| Row-major    | negative | negative | present | present | present | `row_major_complex_access_pattern`    |
	| Column-major | negative | negative | present | present | present | `column_major_complex_access_pattern` |

---

#### **Level 3**

**Input Validation**

Defines validation rules specific to matrix-matrix operations, ensuring dimensional consistency and safe memory access before computation.

| Parameter          |  Condition                                                 | Error Type   | Description                                 |
|--------------------|------------------------------------------------------------|--------------|---------------------------------------------|
| transA             | valid (`no-transpose`, `transpose`, `conjugate-transpose`) | TypeError    | Ensures valid operation for matrix A        |
| transB             | valid (`no-transpose`, `transpose`, `conjugate-transpose`) | TypeError    | Ensures valid operation for matrix B        |
| M                  | ≥ 0                                                        | RangeError   | Rows of op(A) and C must be non-negative    |
| N                  | ≥ 0                                                        | RangeError   | Columns of op(B) and C must be non-negative |
| K                  | ≥ 0                                                        | RangeError   | Shared dimension between A and B            |
| strideA1, strideA2 | (assumed valid)                                            | —            | Define traversal of matrix A                |
| strideB1, strideB2 | (assumed valid)                                            | —            | Define traversal of matrix B                |
| strideC1, strideC2 | ≠ 0                                                        | RangeError   | Prevents invalid traversal of matrix C      |
| offsetA            | ≥ 0 (assumed)                                              | —            | Starting index for matrix A                 |
| offsetB            | ≥ 0 (assumed)                                              | —            | Starting index for matrix B                 |
| offsetC            | ≥ 0 (assumed)                                              | —            | Starting index for matrix C                 |

---

**Testing**

The following tables collectively define a combinatorial testing strategy, where all relevant parameter dimensions (layout, operation type, strides, offsets, and triangular configurations) are systematically combined to generate comprehensive test cases.

1. **Layout Combinations**

	Covers all possible memory layout combinations for matrices `A`, `B`, and `C` to ensure correctness across row-major and column-major storage formats.

	| Layout `A`   | Layout `B`   | Layout `C`   | Fixtures Prefix |
	|--------------|--------------|--------------|-----------------|
	| column-major | column-major | column-major | `ca_cb_cc`      |
	| column-major | column-major | row-major    | `ca_cb_rc`      |
	| column-major | row-major    | column-major | `ca_rb_cc`      |
	| column-major | row-major    | row-major    | `ca_rb_rc`      |
	| row-major    | column-major | column-major | `ra_cb_cc`      |
	| row-major    | column-major | row-major    | `ra_cb_rc`      |
	| row-major    | row-major    | column-major | `ra_rb_cc`      |
	| row-major    | row-major    | row-major    | `ra_rb_rc`      |

---

2. **Operation Combinations**

	Ensures correctness across all combinations of transpose and conjugate-transpose operations applied to matrices `A` and `B`. 
	> Note: Conjugate transpose is only applicable to compatable complex valued routines.

	| Operation A         | Operation B         | Fixtures Suffix |
	|---------------------|---------------------|-----------------|
	| no-transpose        | no-transpose        | `nta_ntb`       |
	| no-transpose        | transpose           | `nta_tb`        |
	| transpose           | no-transpose        | `ta_ntb`        |
	| transpose           | transpose           | `ta_tb`         |
	| conjugate-transpose | no-transpose        | `cta_ntb`       |
	| conjugate-transpose | transpose           | `cta_tb`        |
	| no-transpose        | conjugate-transpose | `nta_ctb`       |
	| transpose           | conjugate-transpose | `ta_ctb`        |
	| conjugate-transpose | conjugate-transpose | `cta_ctb`       |

---

3. **Side and Triangular Variants**

	Validates triangular matrix operations under different configurations, including left/right application and upper/lower storage.

	| Side  | Triangle (uplo) | Fixture Suffix |
	|-------|-----------------|----------------|
	| left  | upper           | `l_u`          |
	| left  | lower           | `l_l`          |
	| right | upper           | `r_u`          |
	| right | lower           | `r_l`          |

---

4. **Offset Handling**

	Ensures correctness when matrices begin at non-zero offsets.

	| Test Condition | Fixture Suffix |   
	|----------------|----------------|
	| offsetA > 0    | `oa`           |
	| offsetB > 0    | `ob`           |
	| offsetC > 0    | `oc`           |

---

5. **Matrix Stride Handling**

	Validates traversal behavior for each matrix independently under varying stride configurations, including reverse and non-contiguous memory layouts.

	**Matrix A**

	| strideA1 | strideA2 | Fixture Suffix |
	|----------|----------|----------------|
	| positive | positive | `sa1_sa2`      |
	| negative | positive | `sa1n_sa2`     |
	| positive | negative | `sa1_sa2n`     |
	| negative | negative | `sa1n_sa2n`    |

	**Matrix B**

	| strideB1 | strideB2 | Fixture Suffix |
	|----------|----------|----------------|
	| positive | positive | `sb1_sb2`      |
	| negative | positive | `sb1n_sb2`     |
	| positive | negative | `sb1_sb2n`     |
	| negative | negative | `sb1n_sb2n`    |

	**Matrix C**

	| strideC1 | strideC2 | Fixture Suffix |
	|----------|----------|----------------|
	| positive | positive | `sc1_sc2`      |
	| negative | positive | `sc1n_sc2`     |
	| positive | negative | `sc1_sc2n`     |
	| negative | negative | `sc1n_sc2n`    |

---

6. **Complex Access Pattern Tests**

Combines strides and offsets across all matrices to simulate realistic, non-contiguous memory access patterns.

| strideA1 | strideA2 | strideB1 | strideB2 | strideC1 | strideC2 | offsetA | offsetB | offsetC | Fixture Suffix           |
|----------|----------|----------|----------|----------|----------|---------|---------|---------|--------------------------|
| positive | positive | positive | positive | positive | positive | present | present | present | `complex_access_pattern` |