nice!view wiring (uses default/hardware SPI):
CS  = D1 / P0.06
MOSI = D2 / P0.17
SCK  = D3 / P0.20



spi pins - for 74HC595 shift registers (software spi in local repository):
  SERIAL OUTPUT (MISO) → D0 / P0.08
  SRCLK→ D5 / P0.24
  RCLK (Latch) → D6 / P1.00
  MISO (unused, but required) → D4 / P0.22



##########################################################################################################################

nice!view wiring (uses default/hardware SPI):
CS  = D1 / P0.06
MOSI = D2 / P0.17
SCK  = D3 / P0.20



spi pins - for 74HC595 shift registers (software spi in local repository):
  SERIAL OUTPUT (MISO) → D0 / P0.08
  SRCLK→ D5 / P0.24
  RCLK (Latch) → D6 / P1.00
  Mosi?? (unused, but required) → D4 / P0.22


col-gpios = <&pro_micro 21 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 20 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 19 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 18 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 15 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 14 (GPIO_ACTIVE_HIGH)>, 
                  <&pro_micro 6 (GPIO_ACTIVE_HIGH)>,  ** shift register − RCLK (Latch)
                  <&pro_micro 5 (GPIO_ACTIVE_HIGH)>,  ** shift register - SRCLK
                  <&pro_micro 4 (GPIO_ACTIVE_HIGH)>,   ** must be empty
                  <&pro_micro 3 (GPIO_ACTIVE_HIGH)>,   ** niceview sck
                  <&pro_micro 2 (GPIO_ACTIVE_HIGH)>,  ** niceview mosi
                  <&pro_micro 0 (GPIO_ACTIVE_HIGH)>, ** shift register - serial output (miso)
                  <&pro_micro 1 (GPIO_ACTIVE_HIGH)>;  ** niceview CS
    };


    left_encoder: encoder_left {
        compatible = "alps,ec11";
        a-gpios = <&gpio1 1 (GPIO_ACTIVE_LOW | GPIO_PULL_UP)>;
        b-gpios = <&gpio1 2 (GPIO_ACTIVE_LOW | GPIO_PULL_UP)>;
        steps = <40>;




 / {
    spi_595_bus: spi_595_bus {
        compatible = "zephyr,spi-bitbang";
        status = "okay";

        /* 595 wiring:
         *   SERIAL OUTPUT (MISO) → D0
         *   SRCLK→ D5
         *   RCLK → D6 (latch)
         *   MISO → D4 (unused, but required)
         */
        clk-gpios  = <&pro_micro 5 GPIO_ACTIVE_HIGH>;  /* D5: SHCP (shift clock) */
        mosi-gpios = <&pro_micro 0 GPIO_ACTIVE_HIGH>;  /* D0: SERIAL OUT */
        miso-gpios = <&pro_micro 4 GPIO_ACTIVE_HIGH>;  /* unused, but required */

        cs-gpios   = <&pro_micro 6 GPIO_ACTIVE_LOW>;   /* D6: STCP (latch clock) */

        #address-cells = <1>;
        #size-cells = <0>;

        shifter: gpio_595@0 {
            compatible = "zmk,gpio-595";
            status = "okay";

            reg = <0>;                  /* first entry in cs-gpios */
            spi-max-frequency = <200000>;

            gpio-controller;
            #gpio-cells = <2>;
            ngpios = <16>;              /* 2×74HC595 */
        };
    };
};



        status = "disabled";