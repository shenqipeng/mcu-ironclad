# WCH MCU Data Collection Report

**Date:** 2026-04-30  
**Manufacturer:** WCH (沁恒微电子)  
**Website:** https://www.wch.cn  
**Database File:** skills/mcu-selection/references/mcu_database.json

## Completion Summary

| Metric | Value |
|--------|-------|
| Total WCH Models | 80 |
| Series Covered | 19 |
| ADC Resolutions | 10-bit, 12-bit, 14-bit |
| Voltage Ranges | 9 variants (1.2V~12V) |

### Fields Completed

- ✅ **adc_channels**: Complete (10/12/14-bit options per series)
- ✅ **voltage_range**: Complete (per model)
- ✅ **temperature_range**: Standard industrial -40°C~+85°C for most series
- ✅ **peripherals**: Complete (uart, spi, i2c, can, usb, ethernet, wireless, lcd_driver)
- ✅ **pins**: Complete (per model)
- ✅ **package**: Complete (per model)

## Series Field Fixes

### CH32V00x Series (9 models)
- **ADC Resolution:** 10-bit (V003) / 12-bit (V002/V004/V005/V006/V007)
- **Temperature Range:** -40°C~+85°C (industrial grade)
- **Voltage Range:** 2.7V~5.5V (V003), 2.0V~5.5V (V002/V004/V005/V006/V007)
- **Peripherals:** USART, SPI, I2C, ADC, TIM, OPA, DMA, TouchKey (V002+)

### CH32V103 Series (4 models)
- **ADC Resolution:** 12-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 2.7V~5.5V
- **Peripherals:** USART(2-3), SPI(2), I2C(2), USB, ADC, TIM, CAN, TouchKey

### CH32V203 Series (11 models)
- **ADC Resolution:** 12-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 2.5V/3.3V
- **Peripherals:** USART(2-4), SPI, I2C, USB(2), ADC, TIM, OPA(2), CAN, TouchKey

### CH32V208 Series (4 models)
- **ADC Resolution:** 12-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 2.5V/3.3V
- **Peripherals:** USART(4), SPI(2), I2C(2), USB(2), ADC, TIM, OPA, CAN, ETH(10M), BLE 5.3
- **BLE Version:** BLE 5.3

### CH32V303 Series (3 models)
- **ADC Resolution:** 12-bit (dual ADC)
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 2.5V/3.3V
- **Peripherals:** USART(8), SPI(2), I2C(2), USB, ADC(2x12-bit), TIM(10), OPA(4), CAN, DAC(2)

### CH32V305 Series (2 models)
- **ADC Resolution:** 12-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 2.5V/3.3V
- **Peripherals:** USART(8), SPI(2), I2C(2), USB(2), ADC, TIM(10), OPA, CAN(2), SDIO

### CH32V307 Series (2 models)
- **ADC Resolution:** 12-bit (dual ADC)
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 2.5V/3.3V
- **Peripherals:** USART(8), SPI(2), I2C(2), USB(2), ADC(2x12-bit), TIM(10), OPA(4), CAN(2), SDIO, DVP, ETH(1000M MAC+10M PHY)

### CH32V317 Series (2 models)
- **ADC Resolution:** 12-bit (dual ADC)
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 2.5V/3.3V
- **Peripherals:** USART(8), SPI(2), I2C(2), USB(2), ADC(2x12-bit), TIM(10), OPA(4), CAN(2), SDIO, DVP, ETH(1000M MAC+10M PHY)

### CH32X033 Series (1 model)
- **ADC Resolution:** 12-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 2.0V~5.5V
- **Peripherals:** USART(4), SPI, I2C, USB PD, ADC, TIM, OPA, CMP(2), PIOC

### CH32X035 Series (7 models)
- **ADC Resolution:** 12-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 2.0V~5.5V
- **Peripherals:** USART(3-4), SPI, I2C, USB PD, ADC, TIM, OPA(2), CMP(3), PIOC

### CH32L103 Series (6 models)
- **ADC Resolution:** 12-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 1.8V~3.6V
- **Peripherals:** USART(3-4), SPI(2), I2C(2), USB PD, ADC, TIM, OPA, CMP(3), CAN

### CH57x BLE Series (6 models)
- **ADC Resolution:** 12-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 2.3V~3.6V (1.7V~3.6V for CH573X)
- **Peripherals:** UART(2-4), SPI, USB, ADC, TIM, PWM, RTC, BLE 4.2, TouchKey
- **BLE Version:** BLE 4.2

### CH58x BLE Series (4 models)
- **ADC Resolution:** 12-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 2.3V~3.6V (1.7V~3.6V for CH583M)
- **Peripherals:** UART(2-4), SPI(2), USB(2), ADC, TIM, PWM, RTC, BLE 5.3, TouchKey
- **BLE Version:** BLE 5.3

### CH59x BLE Series (6 models)
- **ADC Resolution:** 12-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 1.7V~3.6V (2.3V~3.6V for CH591x)
- **Peripherals:** UART(2-4), SPI, I2C, USB, ADC, TIM, PWM, RTC, BLE 5.4, LCD, TouchKey
- **BLE Version:** BLE 5.4

### CH58x Advanced BLE Series (4 models)
- **ADC Resolution:** 14-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 1.7V~3.6V
- **Peripherals:** UART(4), SPI(2), I2C, USB FS/HS, ADC, TIM, PWM, RTC, BLE 5.4, NFC, LED Matrix, LCD
- **BLE Version:** BLE 5.4

### CH595 Series (1 model)
- **ADC Resolution:** 12-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 2.3V~3.6V
- **Peripherals:** UART, SPI, USB, ADC, TIM, BLE 5.x, LCD
- **BLE Version:** BLE 5.x

### CH596 Series (1 model)
- **ADC Resolution:** 12-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 1.2V~1.8V (single battery)
- **Peripherals:** UART, SPI, USB, ADC, TIM, BLE 5.x, LCD
- **BLE Version:** BLE 5.x

### CH56x Series (4 models)
- **ADC Resolution:** 12-bit
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 3.3V
- **Peripherals:** UART(3-8), SPI(1-3), USB 2.0/3.0, ADC, ETH(100M/1000M), SerDes, AES/SM4, CAN, SDIO, DVP

### CH64x Series (3 models)
- **ADC Resolution:** 10-bit (CH641) / 12-bit (CH643/CH645)
- **Temperature Range:** -40°C~+85°C
- **Voltage Range:** 5V~12V (CH641), 3.3V/5V (CH643), 3.3V (CH645)
- **Peripherals:** UART(1-4), SPI, I2C, USB PD/USB 2.0 HS/USB HUB, ADC, ETH(100M), RGB LED Driver (CH643), SerDes (CH645)

## Missing Models Found and Added

The following 46 models were missing from mcu_database.json and have been added:

### CH32V203 Series (4 models)
- CH32V203F8U6 (QFN20)
- CH32V203G6U6 (QFN28)
- CH32V203G8R6 (QSOP28)
- CH32V203C8U6 (QFN48)

### CH32V208 Series (1 model)
- CH32V208GBU6 (QFN28)

### CH32V303 Series (3 models)
- CH32V303CBT6 (LQFP48)
- CH32V303RCT6 (LQFP64)
- CH32V303VCT6 (LQFP100)

### CH32V317 Series (2 models)
- CH32V317WCU6 (QFN68)
- CH32V317VCT6 (LQFP100)

### CH32X033 Series (1 model)
- CH32X033F8P6 (TSSOP20)

### CH32X035 Series (6 models)
- CH32X035F7P6 (TSSOP20)
- CH32X035F8U6 (QFN20)
- CH32X035G8U6 (QFN28)
- CH32X035G8R6 (QSOP28)
- CH32X035C8T6 (LQFP48)
- CH32X035R8T6 (LQFP64)

### CH32L103 Series (5 models)
- CH32L103K8U6 (QFN32)
- CH32L103G8R6 (QSOP28)
- CH32L103F8U6 (QFN20)
- CH32L103F8P6 (TSSOP20)
- CH32L103F7P6 (TSSOP20)

### CH57x Series (4 models)
- CH573Q (LQFP32)
- CH571F (QFN28)
- CH571D (QFN20)
- CH571K (ESSOP10)

### CH58x Series (2 models)
- CH582M (QFN48)
- CH581F (QFN28)

### CH59x Series (5 models)
- CH592F (QFN28)
- CH592D (QFN20)
- CH591F (QFN28)
- CH591D (QFN20)
- CH591R (QSOP24)

### CH58x Advanced Series (4 models)
- CH585M (QFN48)
- CH585F (QFN32)
- CH584M (QFN48)
- CH584F (QFN32)

### CH595/596 Series (2 models)
- CH595 (QFN32)
- CH596 (QFN32)

### CH56x Series (4 models)
- CH569W (QFN68)
- CH565W (QFN68)
- CH565M (QFN40)
- CH564 (LQFP64)

### CH64x Series (3 models)
- CH641 (QFN20)
- CH643 (QFN68)
- CH645 (QFN68)

## Model Pin Count Summary

| Series | Pin Counts Available |
|--------|---------------------|
| CH32V00x | 8, 16, 20 |
| CH32V103 | 48, 64 |
| CH32V203 | 20, 28, 32, 48, 64 |
| CH32V208 | 28, 48, 64, 68 |
| CH32V303 | 48, 64, 100 |
| CH32V305 | 20, 64 |
| CH32V307 | 64, 100 |
| CH32V317 | 68, 100 |
| CH32X033/035 | 20, 28, 48, 64 |
| CH32L103 | 20, 28, 32, 48 |
| CH57x | 10, 20, 28, 32 |
| CH58x | 28, 48 |
| CH59x | 20, 24, 28, 32 |
| CH58x Advanced | 32, 48 |
| CH595/596 | 32 |
| CH56x | 40, 64, 68 |
| CH64x | 20, 68 |

## Data Notes

### ADC Resolution Mapping
- **10-bit:** CH32V003, CH641
- **12-bit:** CH32V002/004/005/006/007, CH32V103, CH32V203, CH32V208, CH32V303/305/307/317, CH32X033/035, CH32L103, CH57x, CH58x, CH59x, CH56x, CH643/645
- **14-bit:** CH584, CH585

### Temperature Range Note
Most WCH MCUs use standard industrial temperature range -40°C~+85°C. Specific grades (automotive, extended) are not documented in standard datasheets.

### High-Performance Excluded
CH32H417 series (400MHz dual-core, 960KB Flash) excluded as high-performance parts outside entry-level/mainstream scope.

## Verification

- ✅ JSON Valid: true
- ✅ Total WCH models in database: 80
- ✅ WCH detailed source models: 115 (including CH32H417 high-performance series)
- ✅ Difference reason: CH32H417 high-performance series (4 models) excluded; minor packaging variants not duplicated
- ✅ Fields verified: part_number, series, core, flash_kb, ram_kb, max_freq_mhz, package, gpio, adc_channels, uart, spi, i2c, can, usb, ethernet, wireless, lcd_driver, voltage_range