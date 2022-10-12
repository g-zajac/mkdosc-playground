# Meanwell Power Supplies
In addition to the adjustment via the built-in potentiometer, the output voltage can be trimmed to 40~110% (depending from the PS specification/model, check the table) of the nominal voltage by applying EXTERNAL VOLTAGE.

Adjustment of constant current level is allowable to:

* 40 ~ 110% of rated current for RSP-750
* 20 ~ 100% of rated current for RSP-1600  

<!-- TODO add current range as voltage -->

## [RSP-750-48](https://www.meanwell.com/Upload/PDF/RSP-750/RSP-750-SPEC.PDF)

|  Type       | Output V Range | Nominal Voltage | Min Voltage |  Max Voltage | Current | 
| ----------- | ------------ | --------------- | ----------- | ------------ |-------- |
| RSP-750-5 |  40 - 110%   |        5V         |    2V     |      5.5V     |  100A   |
| RSP-750-12 |  40 - 110%   |       12V       |    4.8V     |      13.2V     |  62.5A   |
| RSP-750-15 |  40 - 110%   |       15V       |    6V     |      16.5V     |  50A   |
| RSP-750-24 |  40 - 110%   |       24V       |    9,6V     |      26.4V     |  31.3A   |
| RSP-750-27 |  40 - 110%   |       27V       |    10.8V     |      29.7V     |  27.8A   |
| **RSP-750-48** | **40 - 110%** | **48V** | **19,2V** | **52.8V** | **15.7A** |

We use RSP-750-48

## [RSP-1600-48](https://www.meanwell.com/Upload/PDF/RSP-1600/RSP-1600-SPEC.PDF)
The Meanwell (RSP-1600-48) 

|  Type       | Output V Range | Nominal Voltage | Min Voltage |  Max Voltage | Current | 
| ----------- | ------------ | --------------- | ----------- | ------------ |-------- |
| RSP-1600-12 |  60 - 125%   |       12V       |    7.2V     |      15V     |  125A   |
| RSP-1600-24 |  40 - 125%   |       24V       |    9,6V     |      30V     |  67A    |
| RSP-1600-27 |  40 - 125%   |       27V       |    10.8V    |    34.75V    |  59A    |
| RSP-1600-36 |  40 - 125%   |       36V       |    14.4V    |      45V     |  44.5A  |
| **RSP-1600-48** | **40 - 125%** | **48V** |  **19,2V**    |    **60V**   |  **33.5A** |

Practicly we should use mainly RSP-1600-48 unless the battery specs need lower voltage then 19.2V as the hardware will not be able to handle more then 30A.



<!-- TODO add current range in similar way as voltage -->