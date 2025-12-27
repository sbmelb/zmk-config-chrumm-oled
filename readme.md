nice!view wiring (uses default/hardware SPI):
CS  = D1 / P0.06
MOSI = D3 / P0.17
SCK  = D2 / P0.20
*note - D2 and D3 are reversed (from the default pin allocations)
* the &pinctrl code is located in chrummv2.keymap



spi pins - for 74HC595 shift registers (software spi in local repository):
  SERIAL OUTPUT (MISO) → D0 / P0.08
  SRCLK→ D5 / P0.24
  RCLK (Latch) → D6 / P1.00
  MISO (unused, but required) → D4 / P0.22
  * the code is located in nice_nano.overlay



