## 8x4 Register File

This project implements a structural 8×4 register file in VHDL — 8 registers, each 4 bits wide, supporting one write and one read per clock cycle to independently addressed locations.

**Functional units:**
- **3-to-8 Decoder** — takes a 3-bit address plus an enable line and produces a one-hot 8-bit output, activating exactly one line when enabled and none when disabled
- **Register Module** — a single generic-width register with active-low asynchronous reset and a write-enable input; on a rising clock edge with write-enable asserted, it latches the input data
- **8-to-1 Multiplexer** — selects one of eight 4-bit input buses based on a 3-bit select signal

**Top-level Register File:** The decoder converts the write address into a one-hot enable vector, so on a given clock edge only the addressed register captures the incoming data — the other seven hold their state. Eight register instances are generated structurally with a `for...generate` loop rather than instantiated individually. The same address line simultaneously drives the read mux, which continuously outputs the contents of the addressed register.

Because the write address and read address are shared, this design supports one read and one write to the *same* address per cycle — a natural precursor to the register files used in a single-cycle CPU datapath.
