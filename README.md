# ADC DMA Linear Potentiometer

Basic STM32G0 firmware project for reading a linear potentiometer with `ADC1` and `DMA` on an `STM32G071RB` target.

The project is generated from STM32CubeMX and structured with:

- `hal/` for STM32Cube-generated startup code, HAL drivers, linker scripts, and Makefile
- `app/` for user application code

## Target

- Board: `NUCLEO-G071RB`
- MCU: `STM32G071RBTx`
- Toolchain: `arm-none-eabi-gcc`
- Project type: STM32CubeMX Makefile project

## Current Configuration

The generated firmware currently configures:

- `ADC1` on `PA0` (`ADC1_IN0`)
- `DMA1_Channel1` for ADC transfers
- `USART2` on `PA2` / `PA3` at `115200` baud
- `PA5` as `LED_GREEN`
- System clock from internal `HSI` at `16 MHz`

## Project Status

Hardware initialization is present, but the application logic is still minimal.

- `main.c` initializes GPIO, DMA, UART, and ADC
- `app/app.c` contains an empty `APP_Loop()`
- ADC + DMA are configured in the HAL layer, but application-side sampling / processing is not implemented yet

## Build

From the `hal/` directory:

```sh
make
```

Build artifacts are generated in:

```text
hal/build/
```

Expected outputs include:

- `.elf`
- `.hex`
- `.bin`

## Hardware Notes

For a basic potentiometer test:

- connect one end of the potentiometer to `3.3V`
- connect the other end to `GND`
- connect the wiper to `PA0`

If you want serial output later, use `USART2` through the Nucleo ST-LINK virtual COM port.

## Repository Layout

```text
.
|- app/
|  |- app.c
|  `- app.h
`- hal/
   |- Core/
   |- Drivers/
   |- Makefile
   `- hal-ADC-DMA-Linear-Potentiometer.ioc
```

## Next Steps

Typical follow-up work for this project:

- start ADC conversions with DMA
- store the converted sample in a buffer or variable
- scale the ADC value to a useful range
- transmit readings over UART or use them to control output behavior
