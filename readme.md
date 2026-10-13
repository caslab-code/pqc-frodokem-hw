# FrodoKEM RTL Implementation

This directory contains the verilog implementation of the FrodoKEM post-quantum cryptographic algorithm.

## Directory Structure

### `/rtl/aes128`
AES-128 encryption implementation including key expansion, S-box operations, and encryption rounds.

### `/rtl/common`
Shared parameters and utilities used across the design, including system-wide parameter definitions.

### `/rtl/shake256`
SHAKE-256 cryptographic hash function implementation with Keccak round functions and top-level modules.

### `/rtl/tb`
Testbench directory containing verification files and simulation scripts for all modules.

## Core Modules

- `frodo_kem_top.v` - Top-level FrodoKEM module
- `matrix_arithmetic.v` - Matrix operations
- `encode.v` / `decode.v` - encode and decode modules
- `sample.v` - Random sampling operations
- `sram.v` / `sram_dp.v` - Memory modules (single and dual-port)

## Makefile Usage

The main Makefile is located in the `tb/` directory and provides targets for:

- **Individual module testing**: `tb_<module_name>` (e.g., `tb_sram`, `tb_encode`)
- **Full system test**: `tb_frodo_kem_top`
- **Cleanup**: `clean` - removes generated files

### Running Tests
```bash
cd rtl/tb/
make tb_frodo_kem_top    # Run full system testbench
make tb_matrix_arithmetic # Test matrix operations
make clean               # Clean generated files
```

All testbenches use Icarus Verilog for simulation. 

### Reference

Deshpande, S., Longa, P., & Szefer, J. (2026). Accelerating FrodoKEM in Hardware. IACR Transactions on Cryptographic Hardware and Embedded Systems, 2026(3), 881-907. https://doi.org/10.46586/tches.v2026.i3.881-907

Bibtex entry:
```
@article{Deshpande_Longa_Szefer_2026, title={Accelerating FrodoKEM in Hardware}, volume={2026}, url={https://tches.iacr.org/index.php/TCHES/article/view/13129}, DOI={10.46586/tches.v2026.i3.881-907}, abstractNote={
FrodoKEM, a conservative post-quantum key encapsulation mechanism based on the plain Learning with Errors (LWE) problem, has been recommended for use by several government cybersecurity agencies and is currently undergoing standardization by the International Organization for Standardization (ISO). Despite its robust security guarantees, FrodoKEM’s performance remains one of the main challenges to its widespread adoption. This work addresses this concern by presenting a fully standard-compliant, high-performance hardware implementation of FrodoKEM targeting both FPGA and ASIC platforms. The design introduces a scalable parallelization architecture that supports run-time configurability across all twelve parameter sets, covering three security levels (L1, L3, L5), two PRNG variants (SHAKE-based and AES-based), and both standard and ephemeral modes, alongside synthesis-time tunability through a configurable performance parameter to balance throughput and resource utilization. For security level L1 on AMD Artix 7 FPGA, the implementation achieves 2,599, 2,338, and 2,147 operations per second for key generation, encapsulation, and decapsulation, respectively, representing the fastest standard-compliant performance reported to date while consuming only 37.6K LUTs, 64 DSPs, and 10.1K flip-flops. The design achieves a 2.3–159x improvement in the Area–Time Product (ATP) over all prior specification-compliant FPGA implementations. Furthermore, this work presents the first ASIC evaluation of FrodoKEM using the NANGATE45 45 nm technology library, achieving 7,721, 6,946, and 6,378 operations per second for key generation, encapsulation, and decapsulation, respectively, with a logic area of 0.250 mm2. The ASIC implementation exhibits favorable sub-linear area scaling and competitive energy efficiency across different performance parameter configurations, establishing a baseline for future comparative studies. The results validate FrodoKEM’s practical viability for deployment in high-throughput, resource-constrained, and power-sensitive cryptographic applications, demonstrating that conservative post-quantum security can be achieved without compromising performance.
}, number={3}, journal={IACR Transactions on Cryptographic Hardware and Embedded Systems}, author={Deshpande, Sanjay and Longa, Patrick and Szefer, Jakub}, year={2026}, month={Jul.}, pages={881–907}
```

