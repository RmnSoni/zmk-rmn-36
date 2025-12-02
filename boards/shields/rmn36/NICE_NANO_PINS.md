# nice!nano v2 Pin Reference

## Pin Layout (Pro Micro Compatible)

The nice!nano v2 uses a Pro Micro footprint. Here are the available pins:

```
         nice!nano v2
    ┌─────────────────────┐
    │                     │
D3  │ (1)           (24)  │ RAW
D2  │ (2)           (23)  │ GND
GND │ (3)           (22)  │ RST
GND │ (4)           (21)  │ VCC
D1  │ (5)           (20)  │ F4 / A3
D0  │ (6)           (19)  │ F5 / A2
D4  │ (7)           (18)  │ F6 / A1
C6  │ (8)           (17)  │ F7 / A0
D7  │ (9)           (16)  │ B1
E6  │ (10)          (15)  │ B3
B4  │ (11)          (14)  │ B2
B5  │ (12)          (13)  │ B6
    │                     │
    └─────────────────────┘
```

## Pin Mapping for ZMK

In your `rmn36.overlay` file, use these with the `&pro_micro` reference:

| Pro Micro Label | Pin Number | ZMK Usage Example |
|----------------|------------|-------------------|
| D3             | 1          | `&pro_micro 1 GPIO_ACTIVE_HIGH` |
| D2             | 0          | `&pro_micro 0 GPIO_ACTIVE_HIGH` |
| D1             | 2          | `&pro_micro 2 GPIO_ACTIVE_HIGH` |
| D0             | 3          | `&pro_micro 3 GPIO_ACTIVE_HIGH` |
| D4             | 4          | `&pro_micro 4 GPIO_ACTIVE_HIGH` |
| C6             | 5          | `&pro_micro 5 GPIO_ACTIVE_HIGH` |
| D7             | 6          | `&pro_micro 6 GPIO_ACTIVE_HIGH` |
| E6             | 7          | `&pro_micro 7 GPIO_ACTIVE_HIGH` |
| B4             | 8          | `&pro_micro 8 GPIO_ACTIVE_HIGH` |
| B5             | 9          | `&pro_micro 9 GPIO_ACTIVE_HIGH` |
| F4 / A3        | 20         | `&pro_micro 20 GPIO_ACTIVE_HIGH` |
| F5 / A2        | 18         | `&pro_micro 18 GPIO_ACTIVE_HIGH` |
| F6 / A1        | 19         | `&pro_micro 19 GPIO_ACTIVE_HIGH` |
| F7 / A0        | 21         | `&pro_micro 21 GPIO_ACTIVE_HIGH` |
| B1             | 15         | `&pro_micro 15 GPIO_ACTIVE_HIGH` |
| B3             | 14         | `&pro_micro 14 GPIO_ACTIVE_HIGH` |
| B2             | 16         | `&pro_micro 16 GPIO_ACTIVE_HIGH` |
| B6             | 10         | `&pro_micro 10 GPIO_ACTIVE_HIGH` |

## Example Configuration

For a 10 column x 4 row keyboard, you could use:

### Columns (10 pins needed):
```c
col-gpios
    = <&pro_micro 21 GPIO_ACTIVE_HIGH>  // F7 / A0
    , <&pro_micro 20 GPIO_ACTIVE_HIGH>  // F4 / A3
    , <&pro_micro 19 GPIO_ACTIVE_HIGH>  // F6 / A1
    , <&pro_micro 18 GPIO_ACTIVE_HIGH>  // F5 / A2
    , <&pro_micro 15 GPIO_ACTIVE_HIGH>  // B1
    , <&pro_micro 14 GPIO_ACTIVE_HIGH>  // B3
    , <&pro_micro 16 GPIO_ACTIVE_HIGH>  // B2
    , <&pro_micro 10 GPIO_ACTIVE_HIGH>  // B6
    , <&pro_micro 1 GPIO_ACTIVE_HIGH>   // D3
    , <&pro_micro 0 GPIO_ACTIVE_HIGH>   // D2
    ;
```

### Rows (4 pins needed):
```c
row-gpios
    = <&pro_micro 2 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>  // D1
    , <&pro_micro 3 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>  // D0
    , <&pro_micro 4 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>  // D4
    , <&pro_micro 5 (GPIO_ACTIVE_HIGH | GPIO_PULL_DOWN)>  // C6
    ;
```

## Important Notes

1. **Do not use** pins marked as GND, RAW, RST, or VCC for GPIO
2. The nice!nano v2 has **14 usable digital pins** (enough for your 10 columns + 4 rows)
3. Pin numbers in ZMK correspond to the Pro Micro pinout, not the nRF52840 GPIO numbers
4. For `col2row` diode direction (cathode to columns), columns should be `GPIO_ACTIVE_HIGH`
5. Rows should include `GPIO_PULL_DOWN` flag when using `col2row` configuration

## Testing Your Pin Assignment

Once you assign your pins:
1. Test each key individually to verify correct wiring
2. If a key doesn't work, check the diode orientation
3. Use a multimeter to verify continuity between switches and controller pins
