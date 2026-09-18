# r2r-dac

A 4-bit R-2R ladder DAC built from eight resistors (10k and 20k), driven by 3.3 V logic.

![Schematic](docs/r2r_dac.svg)

## How it works

Each bit drives a 20k leg into the ladder, and the 10k series resistors halve each bit's contribution as it moves toward the LSB end. The output is

    Vout = 3.3 V × code / 16

where `code` is the 4-bit input value, with B3 as the MSB. That gives 0 V at code 0, 1.65 V at code 8, and 3.09 V at code 15. Each step is 0.206 V.

## Files

| File | What it is |
|---|---|
| `r2r_dac.kicad_pro`, `r2r_dac.kicad_sch` | KiCad 10 project and schematic |
| `r2r_dac.cir` | SPICE netlist with a 4-bit counter on the inputs |
| `docs/r2r_dac.svg` | Schematic export |

J1 takes the four bits (pin 1 = B0). J2 carries VOUT (pin 1) and GND (pin 2). The reference designators match the SPICE netlist.

## Simulating

```
ngspice r2r_dac.cir
```

The netlist counts from 0 to 15 over 8 ms and measures the output at code 8 and code 15.
