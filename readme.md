nice!view wiring (uses default/hardware SPI):
CS  = D1 / P0.06
MOSI = D2 / P0.17
SCK  = D3 / P0.20



spi pins - for 74HC595 shift registers (software spi in local repository):
  SERIAL OUTPUT (MISO) → D0 / P0.08
  SRCLK→ D5 / P0.24
  RCLK (Latch) → D6 / P1.00
  MISO (unused, but required) → D4 / P0.22


col-gpios = <&pro_micro 21 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 20 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 19 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 18 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 15 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 14 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 6 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 5 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 4 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 3 (GPIO_ACTIVE_HIGH)>,  // * D3
                  <&pro_micro 2 (GPIO_ACTIVE_HIGH)>,  // * D2
                  <&pro_micro 0 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 1 (GPIO_ACTIVE_HIGH)>; // * D1
    };


    left_encoder: encoder_left {
        compatible = "alps,ec11";
        a-gpios = <&gpio1 1 (GPIO_ACTIVE_LOW | GPIO_PULL_UP)>;
        b-gpios = <&gpio1 2 (GPIO_ACTIVE_LOW | GPIO_PULL_UP)>;
        steps = <40>;
        status = "disabled";