# NeoPixel driver for Matrix Display

This library provides a driver for various Neo Pixel LED matrix displays. This library should be backwards compatible
with the original neopixel library for micro:bit and can therefore act as a drop in replacement for the original
library.

This version adds support for drawing images on matrix displays.

NeoPixels consist of programmable RGB LEDs (WS2812B), every one of them controlled
separately.  

## ~ hint

See [Microsoft/pxt-ws2812b](https://makecode.microbit.org/pkg/microsoft/pxt-ws2812b) for basic WS2812B led support. 

## ~

## Basic usage

```blocks
// Create a NeoPixel driver - specify the pin, number of LEDs, and the type of 
// the NeoPixel srip, either standard RGB (with GRB or RGB format) or RGB+White.
let strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB);

let image = images.createImage(`
        . . # . .
        . # # # .
        # . # . #
        . . # . .
        . . # . .
        `);
strip.setMatrixMode(true, direction: MatrixDirection.DOWN_TOP);
strip.setMatrixDimensions(5, 5);
strip.showImage(image, NeoPixelColors.Red);

// send the data to the strip
strip.show()
```

Use ``||setBrightness||`` to lower the brightness (it's maxed out by default).

Use ``||shift||`` or ``||rotate||`` to shift the lights around.

Use ``||setPixelWhiteLED||`` to set brightness of the white pixel for RGB+W strips. 

## HSL color format

Use `neopixel.hslToRgb()` to create colors using hue, saturation, and lightness.

## Example: Using accelerometer to control colors

This little program will let the position of the microbit control the color of the first LED.
This first LED will then get shifted further away every 100ms.

```blocks
let strip = neopixel.create(DigitalPin.P0, 24, NeoPixelMode.RGB_RGB)
while (true) {
    let x = input.acceleration(Dimension.X) / 2;
    let y = input.acceleration(Dimension.Y) / 2;
    let z = input.acceleration(Dimension.Z) / 2;
    strip.shift(1);
    strip.setPixelColor(0, neopixel.rgb(x, y, -z));
    strip.show();
    basic.pause(100);
}
```

## Supported targets

* for PXT/microbit
* for PXT/calliope

## License

MIT

## Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
