### Platform Support

The following table shows ADC module APIs available for each platform.

|  | Linux<br/>(Ubuntu) | Raspbian<br/>(Raspberry Pi) | Nuttx<br/>(STM32F4-Discovery) |
| :---: | :---: | :---: | :---: |
| adc.open | O | O | O |
| adcpin.read | O | O | O |
| adcpin.readSync | O | O | O |
| adcpin.close | O | O | O |
| adcpin.closeSync | O | O | O |


## Class: ADC

This class allows reading analogue data from hardware pins.

The hardware pins can be read from or written to, therefore they are called bidirectional IO pins. This module provides the reading part.

On Nuttx, you have to know the number of pins that is defined on the target board module. For more information, please see the list below.
  * [STM32F4-discovery](../targets/nuttx/stm32f4dis/IoT.js-API-Stm32f4dis.md#adc-pin)


### new ADC()

Returns a new ADC object which can open an ADC pin.


### adc.open(configuration[, callback])
* `configuration` {Object}
  * `device` {string} mandatory configuration on Linux
  * `pin` {int} mandatory configuration on Nuttx
* `callback` {Function}
  * `err`: {Error|null}
* Returns: `AdcPin` {adc.AdcPin}

Opens an ADC pin with the specified configuration.

**Example**
```js
var Adc = require('adc');
var adc = new Adc();
var adc0 = adc.open({
  device: '/sys/devices/12d10000.adc/iio:device0/in_voltage0_raw'
}, function(err) {
  if (err) {
    throw err;
  }
});
```


## Class: ADCPin


### adcpin.read([callback])
* `callback` {Function}
  * `err`: {Error|null}

Reads the analog value from the pin asynchronously.

`callback` will be called having read the analog value.

**Example**
```js
adc0.read(function(err, value) {
  if (err) {
    throw err;
  }
  console.log('value:', value);
});
```


### adcpin.readSync()
* Returns: `{int}` analog value

Reads the analog value from the pin synchronously.

**Example**
```js
var value = adc0.readSync();
console.log('value:', value);
```


### adcpin.close([callback])
* `callback` {Function}
  * `err`: {Error|null}

Closes ADC pin asynchronously. This function must be called after the work of ADC finished.

`callback` will be called after ADC device is released.

**Example**
```js
adc0.close(function(err) {
  if (err) {
    throw err;
  }
});
```


### adcpin.closeSync()

Closes ADC pin synchronously. This function must be called after the work of ADC finished.

**Example**
```js
adc0.closeSync();
console.log('adc pin is closed');
```
