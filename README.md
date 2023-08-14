# BIIL_MTB-110_LED_Brightness_using_PWM_via_PDL_Template

This Lab demonstrates the process of controlling an LED brightness using PWM via Peripheral Driver Library (PDL) on a PSoC 6 microcontroller.
## 🔥 Requirements
| Resources                                  | Links                                                                                                  |
|--------------------------------------------|--------------------------------------------------------------------------------------------------------|
| Computer                                   | 💻                                                                                                    |
| ModusToolbox™ software v3.0 or later       | [Link](https://www.infineon.com/modustoolbox)                                                         |
| CY8CKIT-062S2-43012 Infineon Board         | [Link](https://github.com/Advance-Innovation-Centre-AIC/BIIL_MTB-100_Hello_World_and_LED_Blinking_Programming_Template/assets/88732241/0215501d-b774-4045-8e64-ef49e28d8404) |
| Technical Report | [dropbox](https://www.dropbox.com/scl/fi/amaxc94pte0ut2i1r5ewx/Technical-Report-Lab00.paper?rlkey=b3xm3vrerz9xgv1glb30cvy9z&dl=0)

## 🚩 Let start
### Create Application 
![image](https://2700952642-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MClo3nC-1US0rbK8Qau%2Fuploads%2FYkuKYh6aVcdXJtCIfFgA%2Fimage.png?alt=media&token=3762f247-cc7d-439f-b28f-69194e506d11)

### Use Device Configurator and set the UART and ADC pin
![image](https://2700952642-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MClo3nC-1US0rbK8Qau%2Fuploads%2FIQfENrEaCI0aH3np0YjR%2Fimage.png?alt=media&token=7655caf7-ba23-4d7e-9983-95e1c1fdf543)
![image](https://2700952642-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MClo3nC-1US0rbK8Qau%2Fuploads%2FU5JWKtNGGbDmWInNQ64d%2Fimage.png?alt=media&token=1934c438-4220-466f-9a7c-e959ede71a23)
![image](https://2700952642-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MClo3nC-1US0rbK8Qau%2Fuploads%2FKeOJvh47XrYRIMaHgsIU%2Fimage.png?alt=media&token=01d4a4bd-d67a-4976-b71c-1cd99ec7bc34)



### Coding
Coding: Open the main.c file and add the following code to the main(void) function.
```
#include "cy_pdl.h"
#include "cybsp.h"

int main(void)
{
    cy_rslt_t result;

    /* Initialize the device and board peripherals */
    result = cybsp_init() ;
    if (result != CY_RSLT_SUCCESS)
    {
        CY_ASSERT(0);
    }

    /* Enable global interrupts */
    __enable_irq();

    // Initialize the TCPWM block
	Cy_TCPWM_PWM_Init(PWM_HW, PWM_NUM, &PWM_config);
	// Enable the TCPWM block
	Cy_TCPWM_PWM_Enable(PWM_HW, PWM_NUM);
	// Start the PWM
	Cy_TCPWM_TriggerReloadOrIndex(PWM_HW, PWM_MASK);

    for (;;)
    {
    	for(int i = 0; i < 500; i++){
    		Cy_TCPWM_PWM_SetCompare0(PWM_HW, PWM_NUM, i);
    		Cy_SysLib_Delay(10); // Delay 10 ms
    	}
    }
}
```
### Build the Application      
![image](https://2700952642-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MClo3nC-1US0rbK8Qau%2Fuploads%2FURPtO3RG4zSzdFQVBzIy%2Fimage.png?alt=media&token=279fdd2a-ac04-4142-bfed-3fd1aaed10e9)



### Launching the Application      
![image](https://2700952642-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MClo3nC-1US0rbK8Qau%2Fuploads%2FwIbXYtGRNDYaYwBkZGZ9%2Fimage.png?alt=media&token=de722e54-d2c4-46e9-9668-027009f4d653)

  Note: Before launching the program to the board, make sure that you have already connected the board to the computer through a USB cable.    
  ![image](https://github.com/Advance-Innovation-Centre-AIC/BIIL_MTB-107_Read_potentiometer_sensor_value_via_an_ADC_HAL_Template/assets/88732241/c9966b5b-702f-478e-bbe8-ba9e277800d2)


### Result     
  Once the device is set up, run the program. The microcontroller will continuously read the potentiometer's analog value, convert it to a digital signal through the ADC, and then convert that signal to millivolts using the PDL functions.
![image](https://2700952642-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MClo3nC-1US0rbK8Qau%2Fuploads%2FQHQJgbwkwuBXZb9bGWmq%2Fimage.png?alt=media&token=361694aa-12e4-43ef-8001-4982d0e52336)

### 🎉  Congratulations! You can now complete Lab110

## Supported toolchains (make variable 'TOOLCHAIN')

- GNU Arm&reg; embedded compiler v10.3.1 (`GCC_ARM`) - Default value of `TOOLCHAIN`
- Arm&reg; compiler v6.16 (`ARM`)
- IAR C/C++ compiler v9.30.1 (`IAR`)

## Supported kits (make variable 'TARGET')

- [PSoC&trade; 62S2 Wi-Fi Bluetooth&reg; pioneer kit](https://www.infineon.com/CY8CKIT-062S2-43012) (`CY8CKIT-062S2-43012`)
- [PSoC&trade; 62S1 Wi-Fi Bluetooth&reg; pioneer kit](https://www.infineon.com/CYW9P62S1-43438EVB-01) (`CYW9P62S1-43438EVB-01`)
- [PSoC&trade; 62S1 Wi-Fi Bluetooth&reg; pioneer kit](https://www.infineon.com/CYW9P62S1-43012EVB-01) (`CYW9P62S1-43012EVB-01`)
- [PSoC&trade; 62S3 Wi-Fi Bluetooth&reg; prototyping kit](https://www.infineon.com/CY8CPROTO-062S3-4343W) (`CY8CPROTO-062S3-4343W`)


## Related resources
Resources  | Links
-----------|----------------------------------
ModusToolbox™ Software Training | [link](https://www.dropbox.com/sh/waj898o4o8eccx0/AAB3hBBaIQo2OvJ5-fubGJIha/training-modustoolbox-level1-getting-started-master/Manual/Ch2-Tools.pdf?dl=0)

## Other resources

Infineon provides a wealth of data at www.infineon.com to help you select the right device, and quickly and effectively integrate it into your design.


## Document history

Document title: BILL_MTB-110 – Read potentiometer sensor value via an ADC PDL

 Version | Description of change
 ------- | ---------------------
 1.0.0   | Lab 110: Learn basic GPIO of controlling LED brightness using PWM via  Peripheral Driver Library (PDL) on a PSoC 6 microcontroller.

## Authors:
- *Assoc. Prof. Wiroon Sriborrirux*
- *Mr. Sriengchhun Chheang*
- *Mr. Sabol Socare*
<br>

<br>

---------------------------------------------------------

© BDH Corporation, 2022-2023
