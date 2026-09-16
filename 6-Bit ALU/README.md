## 6-bit ALU

6-bit combinational Arithmetic Logic Unit in VHDL, built by composing four independent functional units — logic, arithmetic, multiplication, and shifting — behind a single top-level opcode select.

**Functional units:**
- **Logic Unit** — bitwise NOT, AND, OR, and XOR on two 6-bit operands
- **Adder/Subtractor** — computes both A+B and A−B in parallel using a 7-bit carry/borrow-extended signal, with separate outputs for the 6-bit result and the carry-out/borrow-out bit
- **Multiplier** — multiplies two 6-bit unsigned operands into a 12-bit product, output in two 6-bit halves (low/high) since the result doesn't fit in a single 6-bit bus
- **Shifter** — performs logical left shift, logical right shift, and arithmetic (sign-extending) right shift by a variable amount

**Top-level ALU:** All four units run in parallel off the same A/B inputs. A 4-bit select signal routes the correct result to the output: the top 2 bits choose which unit's result to use (adder, multiplier, logic, or shifter), and the bottom 2 bits are passed through to that unit to select its specific operation (e.g. add vs. subtract, or which half of the product to output).

The design is fully combinational — no clock — so the output resolves in a single pass through the logic for any given input and select combination.
