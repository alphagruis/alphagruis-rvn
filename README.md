<p align="center">
  <img width="128" height="128" src="https://github.com/alphagruis/alphagruis-rvn/blob/main/alphagruis-rvn.svg">
  <img width="128" height="128" src="https://github.com/alphagruis/alphagruis-rvn/blob/main/alphagruis-rvn-logo.svg">
</p>

# :small_orange_diamond: alphagruis's Miner for Ravencoin

**alphagruis**'s Miner for **Ravencoin**, is a high performance and rock solid miner. This miner was designed and implemented in C++, OpenCL and CUDA **from scratch** by the **alphagruis** team, a small group of skilled developers, for a huge cryptocurrency mining farm. Now, **alphagruis** can finally publish its wonderful miner. Official binaries are currently only available for the **Windows** platform.

Try it, we are sure you will never want to go back.

## Table of Contents

* [Mining Backends](#mining-backends)
* [Mining Fee](#mining-fee)
* [Mining Transparency](#mining-transparency)
* [Install](#install)
* [Configuration](#configuration)
  * [`"fStratumAddressArray"`](#configuration-fstratumaddressarray)
  * [`"fMinerSettingsArray"`](#configuration-fminersettingsarray)
  * [`"fDevicePCIeTopology"`](#configuration-fdevicepcietopology)
  * [`"fDeviceOverclockSettings"`](#configuration-fdeviceoverclocksettings)
  * [`"fKernelSettings"`](#configuration-fkernelsettings)
* [Usage](#usage)
  * [System Requirements](#system-requirements)
  * [Virtual Memory Size](#virtual-memory-size)
* [License](#license)

## Mining Backends

- **OpenCL** for AMD GPUs.
- **CUDA** for NVIDIA GPUs.

*The miner is able to run on hardware with AMD GPUs and NVIDIA GPUs at the same time.*

## Mining Fee

**alphagruis**'s Miner for **Ravencoin**, is not free. The mining fee time is 36 seconds every 60 minutes minus 36 seconds. In other words, the fee amounts to 1%. The miner unambiguously, display on the console when the mining fee is active.

## Mining Transparency

**alphagruis**'s Miner for **Ravencoin** is completely transparent (the binary (executable machine code) is not packed). The hashrate reported by the miner is not inflated and will match, on average, to the effective hashrate calculated by the pool. Without any tricks. Everything the miner does is displayed on the console and written to the log file. Nothing is left out.

**alphagruis** encourages everyone to scan all files contained in this repository with their favorite antivirus.

## Install

Standalone executable for Windows is provided in the [Releases] section. Download the archive and unpack the content to a place accessible from command line.

## Configuration

To configure the miner, you can easily edit the default **alphagruis-rvn.json** file in JSON format or, if you prefer, you can edit your own configuration file and specify its file path, as additional parameter, via the command line to run the executable. The choice to use a configuration file is essentially due to the number of customizable parameters, which are difficult to specify via the command line, without errors and without exceeding the same limits.

*All JSON field values can be filled with environment variables.*

ex. alphagruis.json file in JSON format to mine with the *ethermine* pool:

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [optional]
    "fLogFile": 1,

    // [optional]
    "fColors": 1,

    // [required]
    "fWorker": "alphagruis",

    // [required]
    "fStratumAddressArray":
    [
        //
        // [RVN] ethermine, nonSSL: 3333, SSL strict: 3443
        //

        {
            // [required]
            "fStratumMode": 1,

            // [required]
            "fWallet": "0000000000000000000000000000000000",

            // [optional]
            "fPassword": "",

            // [required]
            "fSocketAddressName": "stratum-ravencoin.flypool.org",

            // [required]
            "fServerPort": 3443,

            // [optional]
            "fSSL": 2
        }
    ],

    // [required]
    "fMinerSettingsArray":
    [
        //
        // AMD
        //

        {
            // [required] OpenCL: 1
            "fPlatformType": 1,

            // [required] AMD: 1
            "fDeviceType": 1,

        /*
            // [optional]
            "fDevicePCIeTopology":
            {
                // [optional]
                "fDomain": 0,

                // [required]
                "fBus": 0,

                // [required]
                "fDevice": 0,

                // [required]
                "fFunction": 0
            },
        */

            // [optional]
            "fDeviceOverclockSettings":
            {
                // [optional] unit: percentage, expressed in RELATIVE value.
                "fPowerLimit": 0,

                // [optional] unit: celsius, expressed in ABSOLUTE value.
                "fTemperatureLimit": 70,

                // [optional] unit: [MHz, mV] or MHz, expressed in ABSOLUTE value.
                "fClockGraphics": [1150, 850],

                // [optional] unit: [MHz, mV] or MHz, expressed in ABSOLUTE value.
                "fClockMemory": [2050, 850],

                // [optional] unit: natural, AMD only.
                "fMemoryTimingLevel": 2,

                // [optional] unit: percentage, expressed in ABSOLUTE value.
                "fFanSpeed": 100
            },

            // [optional]
            "fKernelSettings":
            {
                // [optional] default: 2
                "fComputeDatasetChannels": 2,

                // [optional] default: 128
                "fComputeDatasetKernelLocalWorkSize": 128,

                // [optional] default: 262144
                "fComputeDatasetKernelGlobalWorkStep": 262144,

                // [optional] default: 2
                "fSearchChannels": 2,

                // [optional] default: 128, 256
                "fProgPowSearchKernelLocalWorkSize": 256,

                // [optional] default: 262144
                "fProgPowSearchKernelGlobalWorkSize": 262144
            }
        },

        //
        // NVIDIA
        //

        {
            // [required] CUDA: 32
            "fPlatformType": 32,

            // [required] NVIDIA: 4
            "fDeviceType": 4,

        /*
            // [optional]
            "fDevicePCIeTopology":
            {
                // [optional]
                "fDomain": 0,

                // [required]
                "fBus": 0,

                // [required]
                "fDevice": 0,

                // [required]
                "fFunction": 0
            },
        */

            // [optional]
            "fDeviceOverclockSettings":
            {
                // [optional] unit: percentage, expressed in ABSOLUTE value.
                "fPowerLimit": 70,

                // [optional] unit: celsius, expressed in ABSOLUTE value.
                "fTemperatureLimit": 70,

                // [optional] unit: MHz, expressed in RELATIVE value.
                "fClockGraphics": 150,

                // [optional] unit: MHz, expressed in RELATIVE value.
                "fClockMemory": 500,

                // [optional] unit: percentage, expressed in ABSOLUTE value.
                "fFanSpeed": 100
            },

            // [optional]
            "fKernelSettings":
            {
                // [optional] default: 2
                "fComputeDatasetChannels": 2,

                // [optional] default: 128
                "fComputeDatasetKernelLocalWorkSize": 128,

                // [optional] default: 0, CUDA only.
                "fComputeDatasetKernelMinBlocksPerMultiprocessor": 0,

                // [optional] default: 262144
                "fComputeDatasetKernelGlobalWorkStep": 262144,

                // [optional] default: 2
                "fSearchChannels": 2,

                // [optional] default: 128, 256
                "fProgPowSearchKernelLocalWorkSize": 128,

                // [optional] default: 0, CUDA only.
                "fProgPowSearchKernelMinBlocksPerMultiprocessor": 0,

                // [optional] default: 262144
                "fProgPowSearchKernelGlobalWorkSize": 262144,

                // [optional] default: 0, CUDA only.
                "fMaximumAmountOfRegisters": 0
            }
        }
    ]
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fLogFile"`|Number|0 to disable logging to file.<br/>1 to enable logging to file.|1|
|`"fColors"`|Number|0 to disable color output on console.<br/>1 to enable color output on console.|1|
|`"fWorker"`|String|The name of your rig. It may only contain letters and numbers. Some pools also only allow up to a maximum of 8 characters.|"alphagruis"|
|`"fStratumAddressArray"`|Array|The array can contain one or more objects with the parameters necessary to connect to the pool. Objects should be specified in order of preemption, from highest to lowest. If connection to the pool is not possible, the miner tries to use the next object to connect to the pool. After 10 minutes, the miner attempts to reestablish the connection using the primary object. And so on.|See Configuration: [`"fStratumAddressArray"`](#configuration-fstratumaddressarray).|
|`"fMinerSettingsArray"`|Array|The array can contain one or more objects to select and configure an entire family of GPUs or a single GPU.|See Configuration: [`"fMinerSettingsArray"`](#configuration-fminersettingsarray).|

#### Configuration: "fStratumAddressArray"

`"fStratumAddressArray"` array, can contain one or more JSON objects as below:

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [required]
    "fStratumMode": 1,

    // [required]
    "fWallet": "0000000000000000000000000000000000",

    // [optional]
    "fPassword": "",

    // [required]
    "fSocketAddressName": "stratum-ravencoin.flypool.org",

    // [required]
    "fServerPort": 3443,

    // [optional]
    "fSSL": 2
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fStratumMode"`|Number|The stratum mode supported by pool.<br/>0 to use the mining proxy protocol (the most widely supported by Ethereum and Ethereum Classic mining pools).<br/>1 to use the plain stratum protocol (the most widely supported by Ravencoin mining pools).<br/>2 to use the ethereum stratum protocol (NiceHash).|1|
|`"fWallet"`|String|The address of the wallet associated with the connection.|"0000000000000000000000000000000000"|
|`"fPassword"`|String|The password, only if required, to connect to the pool. Otherwise, leave it empty.|""|
|`"fSocketAddressName"`|String|The mining server address of the pool.|"stratum-ravencoin.flypool.org"|
|`"fServerPort"`|Number|The mining server port of the pool.|3443|
|`"fSSL"`|Number|0 if `"fServerPort"` refers to an insecure connection (not recommended).<br/>1 if `"fServerPort"` refers to a secure connection (without Certificate Validation, to connect to the server which is using a self-signed certificate).<br/>2 if `"fServerPort"` refers to a secure connection (with Certificate Validation, to connect to the server which is using a CA-signed certificate).|2|

If possible, connect to your favorite mining pool using a secure connection (when available).

#### Configuration: "fMinerSettingsArray"

`"fMinerSettingsArray"` array, can contain one or more JSON objects as below:

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [required] OpenCL: 1
    "fPlatformType": 1,

    // [required] AMD: 1
    "fDeviceType": 1,

/*
    // [optional]
    "fDevicePCIeTopology":
    {
        // [optional]
        "fDomain": 0,

        // [required]
        "fBus": 0,

        // [required]
        "fDevice": 0,

        // [required]
        "fFunction": 0
    },
*/

    // [optional]
    "fDeviceOverclockSettings":
    {
        // [optional] unit: percentage, expressed in RELATIVE value.
        "fPowerLimit": 0,

        // [optional] unit: celsius, expressed in ABSOLUTE value.
        "fTemperatureLimit": 70,

        // [optional] unit: [MHz, mV] or MHz, expressed in ABSOLUTE value.
        "fClockGraphics": [1150, 850],

        // [optional] unit: [MHz, mV] or MHz, expressed in ABSOLUTE value.
        "fClockMemory": [2050, 850],

        // [optional] unit: natural, AMD only.
        "fMemoryTimingLevel": 2,

        // [optional] unit: percentage, expressed in ABSOLUTE value.
        "fFanSpeed": 100
    },

    // [optional]
    "fKernelSettings":
    {
        // [optional] default: 2
        "fComputeDatasetChannels": 2,

        // [optional] default: 128
        "fComputeDatasetKernelLocalWorkSize": 128,

        // [optional] default: 262144
        "fComputeDatasetKernelGlobalWorkStep": 262144,

        // [optional] default: 2
        "fSearchChannels": 2,

        // [optional] default: 128, 256
        "fProgPowSearchKernelLocalWorkSize": 256,

        // [optional] default: 262144
        "fProgPowSearchKernelGlobalWorkSize": 262144
    }
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fPlatformType"`|Number|0 to disable this item.<br/>1 to enable and configure the OpenCL backend (likely when `"fDeviceType"` is equal to 1, namely AMD).<br/>32 to enable and configure the CUDA backend (likely when `"fDeviceType"` is equal to 4, namely NVIDIA).|1|
|`"fDeviceType"`|Number|1 to enable the platform `"fPlatformType"` to use AMD GPUs.<br/>4 to enable the platform `"fPlatformType"` to use NVIDIA GPUs.|1|
|`"fDevicePCIeTopology"`|Object|This object is optional and is used to configure one and only one GPU. This option is useful if your hardware is made up of different GPUs, each requiring an ad hoc customization.|See Configuration: [`"fDevicePCIeTopology"`](#configuration-fdevicepcietopology).|
|`"fDeviceOverclockSettings"`|Object|Overclock settings, to be applied to all GPUs identified with the combination `"fPlatformType"`, `"fDeviceType"` and optionally also with `"fDevicePCIeTopology"`.|See Configuration: [`"fDeviceOverclockSettings"`](#configuration-fdeviceoverclocksettings).|
|`"fKernelSettings"`|Object|Kernel settings, to be applied to all GPUs identified with the combination `"fPlatformType"`, `"fDeviceType"` and optionally also with `"fDevicePCIeTopology"`.|See Configuration: [`"fKernelSettings"`](#configuration-fkernelsettings).|

Simplifying:
- To use AMD GPUs, the `"fMinerSettingsArray"` array must contain an object with `"fPlatformType"` equal to 1 and `"fDeviceType"` equal to 1.
- To use NVIDIA GPUs, the `"fMinerSettingsArray"` array must contain an object with `"fPlatformType"` equal to 32 and `"fDeviceType"` equal to 4.
- To use AMD and NVIDIA together, the `"fMinerSettingsArray"` array must contain two objects, one for AMD and one for NVIDIA. 
- To configure *n* GPUs individually, add *n* objects to `"fMinerSettingsArray"` array, declaring the `"fDevicePCIeTopology"` object to uniquely specify a single GPU.

> If your hardware (single motherboard), for example, consists of 5 AMD Radeon RX 580, 1 AMD Radeon RX 6900 XT, 5 NVIDIA GTX 1070 and 1 NVIDIA RTX 3070, to configure the 4 types of GPU it will be necessary to add to `"fMinerSettingsArray"` array, 4 objects: 
>
> 1. an object to configure 5 AMD Radeon RX 580 (without `"fDevicePCIeTopology"` object).
> 2. an object to work with 1 AMD Radeon RX 6900 XT (with `"fDevicePCIeTopology"` object).
> 3. an object to configure 5 NVIDIA GTX 1070 (without `"fDevicePCIeTopology"` object).
> 4. an object to work with 1 NVIDIA RTX 3070 (with `"fDevicePCIeTopology"` object).

Easier done than said.

#### Configuration: "fDevicePCIeTopology"

This object can optionally be declared in the object added to `"fMinerSettingsArray"`, to uniquely specify a single GPU.

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [optional]
    "fDomain": 0,

    // [required]
    "fBus": 0,

    // [required]
    "fDevice": 0,

    // [required]
    "fFunction": 0
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fDomain"`|Number|PCI domain (always 0 on Windows).|0|
|`"fBus"`|Number|PCI bus number.|0|
|`"fDevice"`|Number|PCI device number.|0|
|`"fFunction"`|Number|PCI function number.|0|

*PCI Addressing.*

*Each PCI peripheral is identified by a **bus** number, a **device** number, and a **function** number. The PCI specification permits a single system to host up to 256 buses, but because 256 buses are not sufficient for many large systems, Linux now supports PCI domains. Each PCI **domain** can host up to 256 buses. Each bus hosts up to 32 devices, and each device can be a multifunction board (such as an audio device with an accompanying CD-ROM drive) with a maximum of eight functions.*

*On the Windows platform using the Task Manager application, you can easily see each GPU's PCIe values.*

#### Configuration: "fDeviceOverclockSettings"

This object can optionally be declared in the object added to `"fMinerSettingsArray"`, to handle overclocking.

![alt text](https://img.shields.io/badge/AMD_GPU_Overclock_Settings-red?color=ed1c24)

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [optional] unit: percentage, expressed in RELATIVE value.
    "fPowerLimit": 0,
    
    // [optional] unit: celsius, expressed in ABSOLUTE value.
    "fTemperatureLimit": 70,
    
    // [optional] unit: [MHz, mV] or MHz, expressed in ABSOLUTE value.
    "fClockGraphics": [1150, 850],
    
    // [optional] unit: [MHz, mV] or MHz, expressed in ABSOLUTE value.
    "fClockMemory": [2050, 850],
    
    // [optional] unit: natural, AMD only.
    "fMemoryTimingLevel": 2,
    
    // [optional] unit: percentage, expressed in ABSOLUTE value.
    "fFanSpeed": 100
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fPowerLimit"`|Number|unit: percentage, expressed in **RELATIVE** value.|0|
|`"fTemperatureLimit"`|Number|unit: celsius, expressed in **ABSOLUTE** value (this parameter is obsolete and recent AMD drivers, no longer seem to contemplate it).|70|
|`"fClockGraphics"`|Array or Number|unit: [MHz, mV] or MHz, expressed in **ABSOLUTE** value.|[1150, 850] or 1150|
|`"fClockMemory"`|Array or Number|unit: [MHz, mV] or MHz, expressed in **ABSOLUTE** value (latest AMD GPUs, do not include voltage control for the memory).|[2050, 850] or 2050|
|`"fMemoryTimingLevel"`|Number|unit: natural, AMD only.|2|
|`"fFanSpeed"`|Number|unit: percentage, expressed in **ABSOLUTE** value.|100|

**The miner overclock the AMD GPUs via AMD Display Library (ADL) SDK using AMD OverdriveN API (version 7) and AMD Overdrive 8 API (version 8). Overdrive versions earlier than version 7 are not supported.**

for more information:<br/>
https://gpuopen.com/adl/

*If you don't know the overclocking values, before launching the miner, temporarily comment out the whole object (multi-line comments start with `/*` and ends with `*/`). Launch the miner. While mining, use of AMD's Radeon WattMan utility to tune your GPU. Once you have determined a stable configuration, uncomment the the whole object and fill in the overclocking values with your optimal overclocking values. Restart the miner for the settings to take effect.*

*Overclocking is automatically applied to all GPUs by the miner, always and only at startup. Since WattMan tends to reset the values when switching to manual tuning mode, remember to switch to manual mode on the GPU you want to control, before starting the miner. If you don't want the miner to handle overclocking, just comment out the whole object.*

![alt text](https://img.shields.io/badge/NVIDIA_GPU_Overclock_Settings-green?color=76b900)

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [optional] unit: percentage, expressed in ABSOLUTE value.
    "fPowerLimit": 70,
    
    // [optional] unit: celsius, expressed in ABSOLUTE value.
    "fTemperatureLimit": 70,
    
    // [optional] unit: MHz, expressed in RELATIVE value.
    "fClockGraphics": 150,
    
    // [optional] unit: MHz, expressed in RELATIVE value.
    "fClockMemory": 450,
    
    // [optional] unit: percentage, expressed in ABSOLUTE value.
    "fFanSpeed": 100
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fPowerLimit"`|Number|unit: percentage, expressed in **ABSOLUTE** value.|70|
|`"fTemperatureLimit"`|Number|unit: celsius, expressed in **ABSOLUTE** value.|70|
|`"fClockGraphics"`|Number|unit: MHz, expressed in **RELATIVE** value.|150|
|`"fClockMemory"`|Number|unit: MHz, expressed in **RELATIVE** value.|450|
|`"fFanSpeed"`|Number|unit: percentage, expressed in **ABSOLUTE** value.|100|

**The miner overclok the NVIDIA GPUs via NVIDIA NVAPI and NVIDIA NVML API.**

for more information:<br/>
https://developer.nvidia.com/nvapi<br/>
https://docs.nvidia.com/deploy/nvml-api/index.html

*If you don't know the overclocking values, before starting the miner, play with the overclocking values of this object, incrementing them carefully and in small steps, starting from 0. Restart the miner for the settings to take effect.*

*Overclocking is automatically applied to all GPUs by the miner, always and only at startup. If you don't want the miner to handle overclocking, just comment out the whole object.*

#### Configuration: "fKernelSettings"

This object is optionally declared in the object added to `"fMinerSettingsArray"`, to set the optimal values to use for mining engines (kernels). The miner invokes two kernels: `ComputeDatasetKernel` kernel to compute the current epoch dataset (DAG), `ProgPowSearchKernel` kernel to compute the hashes. To improve the hashrate, focus on tweaking the parameters of this kernel.

<details>
<summary>JSON Object</summary>
<p>

```json5
{
    // [optional] default: 2
    "fComputeDatasetChannels": 2,

    // [optional] default: 128
    "fComputeDatasetKernelLocalWorkSize": 128,

    // [optional] default: 0, CUDA only.
    "fComputeDatasetKernelMinBlocksPerMultiprocessor": 0,
  
    // [optional] default: 262144
    "fComputeDatasetKernelGlobalWorkStep": 262144,

    // [optional] default: 2
    "fSearchChannels": 2,

    // [optional] default: 128, 256
    "fProgPowSearchKernelLocalWorkSize": 128,

    // [optional] default: 0, CUDA only.
    "fProgPowSearchKernelMinBlocksPerMultiprocessor": 0,

    // [optional] default: 262144
    "fProgPowSearchKernelGlobalWorkSize": 262144,

    // [optional] default: 0, CUDA only.
    "fMaximumAmountOfRegisters": 0
}
```

</p>
</details>

|JSON Field|Data Type|Description|Sample|
|----------|:-------:|-----------|------|
|`"fComputeDatasetChannels"`|Number|Number of channels (command queues in OpenCL, streams in CUDA) to be used to compute the dataset (commonly also known as DAG, acronym for Directed Acyclic Graph).<br/><br/>Integer value, multiple of 1, between 1 and 8.|2|
|`"fComputeDatasetKernelLocalWorkSize"`|Number|The size of the work-group (OpenCL), the size of thread block (CUDA).<br/><br/>Integer value, multiple of 32, between 32 and 4096.|128|
|`"fComputeDatasetKernelMinBlocksPerMultiprocessor"`|Number|This value is optionally used as a parameter by the `__launch_bounds__()` qualifier in the definition of a `__global__` function, CUDA only.|0|
|`"fComputeDatasetKernelGlobalWorkStep"`|Number|Number of dataset items to compute with a kernel execution command, queued on a channel.<br/><br/>Integer value, multiple of 1024, between 1024 and (1024 * 1024).|262144|
|`"fSearchChannels"`|Number|Number of channels (command queues in OpenCL, streams in CUDA) to be used to compute hashes.<br/><br/>Integer value, multiple of 1, between 1 and 8.|2|
|`"fProgPowSearchKernelLocalWorkSize"`|Number|The size of the work-group (OpenCL), the size of thread block (CUDA).<br/><br/>Integer value, multiple of 32, between 32 and 4096.<br/><br/>**:small_red_triangle: This parameter directly affects the hashrate. When setting up your GPU, always look for the best value between 128, 256.**|128|
|`"fProgPowSearchKernelMinBlocksPerMultiprocessor"`|Number|This value is optionally used as a parameter by the `__launch_bounds__()` qualifier in the definition of a `__global__` function, CUDA only.|0|
|`"fProgPowSearchKernelGlobalWorkSize"`|Number|Number of hashes to compute with a kernel execution command, queued on a channel.<br/><br/>Integer value, multiple of 1024, between 1024 and (1024 * 1024 * 1024).|262144|
|`"fMaximumAmountOfRegisters"`|Number|Maximum number of registers that a thread may use, CUDA only.|0|

*Adjust the **global work size** parameters with caution, based on the capabilities of your GPU:*

- *the number of **work-groups** used to launch the kernel is equal to global work size divided by local work size. In other words, the kernel execution is invoked with `number of work-groups` * `work-items per work-group` **work-items** (OpenCL).*

- *the number of **thread blocks** used to launch the kernel is equal to global work size divided by local work size. In other words, the kernel execution is invoked with `number of thread blocks` * `threads per thread block` **threads** (CUDA).*

All kernel settings are automatically adjusted and validated by the miner if needed.

**OpenCL, attribute of the kernels**

The `ComputeDatasetKernel` kernel is compiled at runtime with the OpenCL backend of the driver, using the following attribute:

```OpenCL
#ifndef _M_ComputeDatasetKernelLocalWorkSizeAttribute
#define _M_ComputeDatasetKernelLocalWorkSizeAttribute __attribute__ ((reqd_work_group_size (kComputeDatasetKernelLocalWorkSize, 1, 1)))
#endif
```

The `ProgPowSearchKernel` kernel is compiled at runtime with the OpenCL backend of the driver, using the following attribute:

```OpenCL
#ifndef _M_ProgPowSearchKernelLocalWorkSizeAttribute
#define _M_ProgPowSearchKernelLocalWorkSizeAttribute __attribute__ ((reqd_work_group_size (kProgPowSearchKernelLocalWorkSize, 1, 1)))
#endif
```

> Basically, to maximize device utilization, you can choose to indirectly set the maximum number of registers per-kernel (using `"fProgPowSearchKernelLocalWorkSize"`) adjusting kernel launch configuration.

for more information:<br/>
https://www.khronos.org/registry/OpenCL/sdk/2.2/docs/man/html/optionalAttributeQualifiers.html<br/>
https://www.khronos.org/registry/OpenCL/sdk/2.2/docs/man/html/clEnqueueNDRangeKernel.html

**CUDA, attribute of the kernels**

The `ComputeDatasetKernel` kernel is compiled at runtime with the CUDA backend of the driver, via NVIDIA NVRTC using the following attribute:

```CUDA
#if (qMaximumAmountOfRegisters > 0)
    #ifndef _M_ComputeDatasetKernelLocalWorkSizeAttribute
    #define _M_ComputeDatasetKernelLocalWorkSizeAttribute
    #endif
#elif (kComputeDatasetKernelMinBlocksPerMultiprocessor > 0)
    #ifndef _M_ComputeDatasetKernelLocalWorkSizeAttribute
    #define _M_ComputeDatasetKernelLocalWorkSizeAttribute __launch_bounds__ (kComputeDatasetKernelLocalWorkSize, kComputeDatasetKernelMinBlocksPerMultiprocessor)
    #endif
#else
    #ifndef _M_ComputeDatasetKernelLocalWorkSizeAttribute
    #define _M_ComputeDatasetKernelLocalWorkSizeAttribute __launch_bounds__ (kComputeDatasetKernelLocalWorkSize)
    #endif
#endif
```

The `ProgPowSearchKernel` kernel is compiled at runtime with the CUDA backend of the driver, via NVIDIA NVRTC using the following attribute:

```CUDA
#if (qMaximumAmountOfRegisters > 0)
    #ifndef _M_ProgPowSearchKernelLocalWorkSizeAttribute
    #define _M_ProgPowSearchKernelLocalWorkSizeAttribute
    #endif
#elif (kProgPowSearchKernelMinBlocksPerMultiprocessor > 0)
    #ifndef _M_ProgPowSearchKernelLocalWorkSizeAttribute
    #define _M_ProgPowSearchKernelLocalWorkSizeAttribute __launch_bounds__ (kProgPowSearchKernelLocalWorkSize, kProgPowSearchKernelMinBlocksPerMultiprocessor)
    #endif
#else
    #ifndef _M_ProgPowSearchKernelLocalWorkSizeAttribute
    #define _M_ProgPowSearchKernelLocalWorkSizeAttribute __launch_bounds__ (kProgPowSearchKernelLocalWorkSize)
    #endif
#endif
```

> Basically, to maximize device utilization, you can choose to set the maximum number of registers per-thread (using `"fMaximumAmountOfRegisters"`) or per-kernel (using `"fProgPowSearchKernelLocalWorkSize"` and optionally `"fProgPowSearchKernelMinBlocksPerMultiprocessor"`) adjusting kernel launch configuration.

for more information:<br/>
https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html#execution-configuration-optimizations<br/>
https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html#register-pressure

## Usage
  
The **alphagruis**'s Miner for **Ravencoin** is a command line program. This means you launch it either from a Windows Command Prompt, or create shortcuts to predefined command lines using a Windows batch/cmd file. After setting up the configuration file, **alphagruis**'s Miner for **Ravencoin** is ready to go. 

to launch the miner using the default **alphagruis-rvn.json** file, type:

```batch
alphagruis-rvn.exe
```

to launch the miner using your custom **alphagruis-rvn-custom.json** file (can have any name you like), type:

```batch
alphagruis-rvn.exe alphagruis-rvn-custom.json
```

To ensure that the miner restarts automatically (in the unfortunate event of a crash), **alphagruis** recommends launch it via Windows batch/cmd file (see alphagruis-rvn.cmd and variants, to connect to your favorite mining pool).

```batch
alphagruis-rvn.cmd
```

:small_red_triangle: Press **ctrl+c** to exit gracefully.

*Note:*
- *To overclock AMD GPUs, AMD drivers do not require the executable to run as Administrator.*
- *To overclock NVIDIA GPUs, NVIDIA drivers **require** the executable to run as Administrator.*

#### System Requirements

|Components|Minimum Requirements|
|:--------:|--------------------|
|CPU|Multicore Intel processor (with 64-bit support) or AMD Athlon 64 processor.|
|OS|Windows 10 (64-bit).|
|RAM|8 GiB.|
|GPU|One or more discrete GPUs (AMD or NVIDIA) with **more** than 4 GiB of VRAM (must be above the DAG size). For development, we use hardware up to 12 GPUs each, however, for easy maintenance, we recommend not to exceed 8 GPUs per rig.|
|Storage|256 GiB SSD.|

#### Virtual Memory Size

The virtual memory size must be adjusted upwards according to the current DAG size and the number of discrete GPUs that are installed on your hardware. There is only one imperative rule to respect. The virtual memory size must be equal to or greater than `number of discrete GPUs` * `DAG size` + `size for OS`. For example, if the current DAG size is 4 GiB (4 * 1024 * 1024 * 1024 byte) and you have 7 GPUs, for each GPU you must allocate **at least** 4 GiB of virtual memory plus **at least** 8 GiB for OS: 7 * 4 GiB + 8 GIB = 36 GiB.

**alphagruis** recommends keeping the operating system and the GPU drivers updated to the latest version.

## License

**alphagruis**'s Miner for **Ravencoin** is licensed under the terms of the [BSD 3-Clause License](https://github.com/alphagruis/alphagruis-rvn/blob/main/LICENSE.txt). *alphagruis*, the *alphagruis logo* and the *alphagruis avatar picture* are trademarks of **alphagruis**. All other product names, trademarks or company names, not attributable to **alphagruis**, are used solely for identification and belong to their respective owners.

[Releases]: https://github.com/alphagruis/alphagruis-rvn/releases

<details>
<summary>Sample log file (colorless, *.md file format does not support color).</summary>
<p>

```
Welcome to alphagruis's Miner for Ravencoin, v1.0.2, build: 2021.07.29 20:03:31.000.

PCIe: 00000000:03:00.0, GPU.01: AMD Accelerated Parallel Processing, OpenCL 2.0 (3276.6), AMD Radeon RX 6900 XT, 15.98 GiB, 40 compute units
PCIe: 00000000:07:00.0, GPU.02: NVIDIA CUDA 11.4, NVIDIA GeForce RTX 3070, 8.00 GiB, 46 compute units

--- thread ID: 0x84c, 2021.08.01 14:34:20.326, PCIe: 00000000:03:00.0, GPU.01 fDeviceOverclockSettings:
fPowerLimit: min = -10%, max = +15%, default = +0%, set = +0%
fTemperatureLimit: n/a
fClockGraphics: min = [500 MHz, 825 mV], max = [3000 MHz, 1175 mV], default = [2504 MHz, 1175 mV], set = [1600 MHz, 925 mV]
fClockMemory: min = 2000 MHz, max = 2150 MHz, default = 2000 MHz, set = 2150 MHz
fMemoryTimingLevel: min = 0, max = 1, default = 0, set = 1
fFanSpeed: min = 33%, max = 100%, default = 33%, set = 75%

--- thread ID: 0x84c, 2021.08.01 14:34:20.489, PCIe: 00000000:07:00.0, GPU.02 fDeviceOverclockSettings:
fPowerLimit: min = 41%, max = 110%, default = 100%, set = 75%
fTemperatureLimit: min = 65°C, max = 90°C, default = 83°C, set = 75°C
fClockGraphics: min = -1000 MHz, max = +1000 MHz, default = +0 MHz, set = +200 MHz
fClockMemory: min = -1000 MHz, max = +3000 MHz, default = +0 MHz, set = +500 MHz
fFanSpeed: min = 30%, max = 100%, default = 0%, set = 75%

--- thread ID: 0x84c, 2021.08.01 14:34:20.495
connecting to stratum-ravencoin.flypool.org:3443

--- thread ID: 0x84c, 2021.08.01 14:34:20.594
connected to stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:00:00.103)

<<< thread ID: 0x1ca4, 2021.08.01 14:34:20.594, 0 ms
{"jsonrpc":"2.0","id":1,"method":"mining.subscribe","params":["alphagruis-rvn/1.0.2"]}

>>> thread ID: 0x2424, 2021.08.01 14:34:20.615, 20 ms (20 ms)
{"id":1,"result":[null,"0b8e5b"],"error":null}

<<< thread ID: 0x990, 2021.08.01 14:34:20.615, 0 ms
{"jsonrpc":"2.0","id":10,"method":"mining.extranonce.subscribe","params":[]}

<<< thread ID: 0x760, 2021.08.01 14:34:20.615, 0 ms
{"jsonrpc":"2.0","id":12,"method":"mining.authorize","params":["....alphagruis"]}

--- thread ID: 0x14b0, 2021.08.01 14:34:20.615, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:00:00.123)
PCIe: 00000000:03:00.0, GPU.01: [A = 0, S = 0, R = 0, I = 0], [00:00:00.298, 0 ms], [fan = 75%, 2953 rpm, 41°C], 0.000000 MH/s (27.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 0, S = 0, R = 0, I = 0], [00:00:00.298, 0 ms], [fan = 75%, 1859 rpm, 33°C], 0.000000 MH/s (26.73 W) = 0.000000 MH/s (53.73 W)

>>> thread ID: 0x5d8, 2021.08.01 14:34:20.635, 20 ms (20 ms)
{"id":10,"result":true,"error":null}

>>> thread ID: 0x6d0, 2021.08.01 14:34:20.655, 19 ms (40 ms)
{"id":12,"result":true,"error":null}

>>> thread ID: 0x714, 2021.08.01 14:34:20.655, 0 ms
{"id":null,"method":"mining.set_target","params":["00000009f6000000000000000000000000000000000000000000000000000000"]}

--- thread ID: 0x714, 2021.08.01 14:34:20.655
share difficulty = 0.43118103 GH.

↓↓↓ thread ID: 0x1120, 2021.08.01 14:34:20.897
PCIe: 00000000:03:00.0, GPU.01: mining is suspended, waiting for work.

↓↓↓ thread ID: 0x7f4, 2021.08.01 14:34:20.897
PCIe: 00000000:07:00.0, GPU.02: mining is suspended, waiting for work.

>>> thread ID: 0x710, 2021.08.01 14:34:21.657, 1001 ms
{"id":null,"method":"mining.notify","params":["61da602b93926af1c7c2","c4a9530940f57011507fe048ed12495e267391ac3c66303de2ca004722e1bba1","c61dd6e690b0e87b596a70c4a7451cb67103f3cb830b1c691e5466cec15df702","00000009f6000000000000000000000000000000000000000000000000000000",true,1866617,"1b0135ad"]}

--- thread ID: 0x710, 2021.08.01 14:34:21.659
epoch = 248 (next epoch in 883 blocks), seed = 622205 (next seed in 1 block), share difficulty = 0.43118103 GH.

--- thread ID: 0x710, 2021.08.01 14:34:21.689
epoch = 248, cache size = 49283008 (47.00 MiB), dataset size = 3154109312 (2.94 GiB), compute cache...

--- thread ID: 0x710, 2021.08.01 14:34:22.943, 1254 ms
epoch = 248, cache size = 49283008 (47.00 MiB), dataset size = 3154109312 (2.94 GiB), compute cache: done.

↑↑↑ thread ID: 0x7f4, 2021.08.01 14:34:22.943
PCIe: 00000000:07:00.0, GPU.02: mining is resumed.

↑↑↑ thread ID: 0x1120, 2021.08.01 14:34:22.943
PCIe: 00000000:03:00.0, GPU.01: mining is resumed.

--- thread ID: 0x7f4, 2021.08.01 14:34:22.944
seed = 622205, build PCIe: 00000000:07:00.0, GPU.02 program...

--- thread ID: 0x1120, 2021.08.01 14:34:22.944
seed = 622205, build PCIe: 00000000:03:00.0, GPU.01 program...

--- thread ID: 0x7f4, 2021.08.01 14:34:23.319, 375 ms
seed = 622205, build PCIe: 00000000:07:00.0, GPU.02 program: done.

--- thread ID: 0x99c, 2021.08.01 14:34:23.319
seed = 622206, build PCIe: 00000000:07:00.0, GPU.02 program...

--- thread ID: 0x1120, 2021.08.01 14:34:23.389, 445 ms
seed = 622205, build PCIe: 00000000:03:00.0, GPU.01 program: done.

--- thread ID: 0xd30, 2021.08.01 14:34:23.390
seed = 622206, build PCIe: 00000000:03:00.0, GPU.01 program...

--- thread ID: 0x1120, 2021.08.01 14:34:23.785
epoch = 248, cache size = 49283008 (47.00 MiB), dataset size = 3154109312 (2.94 GiB), compute PCIe: 00000000:03:00.0, GPU.01 dataset...

--- thread ID: 0xd30, 2021.08.01 14:34:24.230, 840 ms
seed = 622206, build PCIe: 00000000:03:00.0, GPU.01 program: done.

--- thread ID: 0x99c, 2021.08.01 14:34:24.320, 1001 ms
seed = 622206, build PCIe: 00000000:07:00.0, GPU.02 program: done.

--- thread ID: 0x7f4, 2021.08.01 14:34:24.325
epoch = 248, cache size = 49283008 (47.00 MiB), dataset size = 3154109312 (2.94 GiB), compute PCIe: 00000000:07:00.0, GPU.02 dataset...

--- thread ID: 0x1120, 2021.08.01 14:34:29.264, 5479 ms
epoch = 248, cache size = 49283008 (47.00 MiB), dataset size = 3154109312 (2.94 GiB), compute PCIe: 00000000:03:00.0, GPU.01 dataset: done.

--- thread ID: 0x7f4, 2021.08.01 14:34:31.597, 7271 ms
epoch = 248, cache size = 49283008 (47.00 MiB), dataset size = 3154109312 (2.94 GiB), compute PCIe: 00000000:07:00.0, GPU.02 dataset: done.

--- thread ID: 0x1120, 2021.08.01 14:34:34.952, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b00102f3e65
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000008eeae0b860f87488d9203b6700d4a7c5aca0cf527340dc7f2c4edf176
   mix: 0x8837b463a0f9819e1735e1f993ee78a82ca92bacd7e35781c5bda3bed93d249a

<<< thread ID: 0x15b8, 2021.08.01 14:34:34.952, 0 ms
{"jsonrpc":"2.0","id":1001,"method":"mining.submit","params":["....alphagruis","61da602b93926af1c7c2","0x0b8e5b00102f3e65","0xc4a9530940f57011507fe048ed12495e267391ac3c66303de2ca004722e1bba1","0x8837b463a0f9819e1735e1f993ee78a82ca92bacd7e35781c5bda3bed93d249a"],"worker":"alphagruis"}

--- thread ID: 0x384, 2021.08.01 14:34:34.976, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x384, 2021.08.01 14:34:34.976, 13318 ms (23 ms)
{"id":1001,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:34:35.101, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b0010b440a9
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000084d24f88800e7953e656d4675df586d2b6fd2f3737c982323fed228cc
   mix: 0x2147c1d0626f471f9e94c121966dcd088e4ce659de9a112e66526191c061929c

<<< thread ID: 0x2424, 2021.08.01 14:34:35.101, 0 ms
{"jsonrpc":"2.0","id":1002,"method":"mining.submit","params":["....alphagruis","61da602b93926af1c7c2","0x0b8e5b0010b440a9","0xc4a9530940f57011507fe048ed12495e267391ac3c66303de2ca004722e1bba1","0x2147c1d0626f471f9e94c121966dcd088e4ce659de9a112e66526191c061929c"],"worker":"alphagruis"}

--- thread ID: 0x990, 2021.08.01 14:34:35.123, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x990, 2021.08.01 14:34:35.123, 147 ms (22 ms)
{"id":1002,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:34:35.637, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:00:15.145)
PCIe: 00000000:03:00.0, GPU.01: [A = 2, S = 0, R = 0, I = 0], [00:00:00.535,  1 ms], [fan = 75%, 2921 rpm, 52°C], 32.070409 MH/s (191.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 0, S = 0, R = 0, I = 0], [00:00:15.320, 12 ms], [fan = 75%, 1858 rpm, 46°C], 26.517798 MH/s (179.53 W) = 58.588207 MH/s (370.53 W)

--- thread ID: 0x7f4, 2021.08.01 14:34:37.671, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 1).
 nonce: 0x0b8e5b0019b6f201
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000033118442d8c29f25152ff7d1dd29a99d22d811edb28a05ee3ec58ea23
   mix: 0xdae9572f278abd563c906dcd9458bcfb0cfc9c40b62c467511d730b992c0d633

<<< thread ID: 0x760, 2021.08.01 14:34:37.672, 0 ms
{"jsonrpc":"2.0","id":1003,"method":"mining.submit","params":["....alphagruis","61da602b93926af1c7c2","0x0b8e5b0019b6f201","0xc4a9530940f57011507fe048ed12495e267391ac3c66303de2ca004722e1bba1","0xdae9572f278abd563c906dcd9458bcfb0cfc9c40b62c467511d730b992c0d633"],"worker":"alphagruis"}

--- thread ID: 0x5d8, 2021.08.01 14:34:37.695, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x5d8, 2021.08.01 14:34:37.695, 2571 ms (23 ms)
{"id":1003,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:34:46.125, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b003760019c
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000008ebd6456a137540bcd2fed7f0d1cb5e1c1ecb5f980ddf3f11ed3fb121
   mix: 0x2a0d5764b8e829417e70a8b1cf5dd644fcb7ebfbaf2e10472fe42c30bb892908

<<< thread ID: 0x6d0, 2021.08.01 14:34:46.125, 0 ms
{"jsonrpc":"2.0","id":1004,"method":"mining.submit","params":["....alphagruis","61da602b93926af1c7c2","0x0b8e5b003760019c","0xc4a9530940f57011507fe048ed12495e267391ac3c66303de2ca004722e1bba1","0x2a0d5764b8e829417e70a8b1cf5dd644fcb7ebfbaf2e10472fe42c30bb892908"],"worker":"alphagruis"}

--- thread ID: 0x714, 2021.08.01 14:34:46.149, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x714, 2021.08.01 14:34:46.149, 8453 ms (24 ms)
{"id":1004,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:34:50.651, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:00:30.159)
PCIe: 00000000:03:00.0, GPU.01: [A = 3, S = 0, R = 0, I = 0], [00:00:04.526, 1 ms], [fan = 75%, 2921 rpm, 55°C], 32.252936 MH/s (192.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 1, S = 0, R = 0, I = 0], [00:00:12.979, 0 ms], [fan = 75%, 1859 rpm, 48°C], 26.669509 MH/s (179.45 W) = 58.922445 MH/s (371.45 W)

--- thread ID: 0x7f4, 2021.08.01 14:34:53.172, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 0).
 nonce: 0x0b8e5b0050118ec4
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000000d52c693866196cb4e3f1acc140ff4173a5b5f5baa76a87628dbb07c1
   mix: 0x6720501b5d1da89b8b51498100eb4294065cdfaa310aa26e5b6c6fa530b329af

<<< thread ID: 0x710, 2021.08.01 14:34:53.172, 0 ms
{"jsonrpc":"2.0","id":1005,"method":"mining.submit","params":["....alphagruis","61da602b93926af1c7c2","0x0b8e5b0050118ec4","0xc4a9530940f57011507fe048ed12495e267391ac3c66303de2ca004722e1bba1","0x6720501b5d1da89b8b51498100eb4294065cdfaa310aa26e5b6c6fa530b329af"],"worker":"alphagruis"}

--- thread ID: 0x15b8, 2021.08.01 14:34:53.194, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x15b8, 2021.08.01 14:34:53.194, 7045 ms (22 ms)
{"id":1005,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:34:58.055, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b006133b936
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000003dfeda5df8519fb8cc695f2deca351cdd07645a861fe77e9723aa13e3
   mix: 0xe20409706130fbecbbd1526ac4f55b0a88a0875534d385f1f06da218562cfdff

<<< thread ID: 0x384, 2021.08.01 14:34:58.055, 0 ms
{"jsonrpc":"2.0","id":1006,"method":"mining.submit","params":["....alphagruis","61da602b93926af1c7c2","0x0b8e5b006133b936","0xc4a9530940f57011507fe048ed12495e267391ac3c66303de2ca004722e1bba1","0xe20409706130fbecbbd1526ac4f55b0a88a0875534d385f1f06da218562cfdff"],"worker":"alphagruis"}

--- thread ID: 0x2424, 2021.08.01 14:34:58.078, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x2424, 2021.08.01 14:34:58.078, 4883 ms (22 ms)
{"id":1006,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:35:05.653, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:00:45.162)
PCIe: 00000000:03:00.0, GPU.01: [A = 4, S = 0, R = 0, I = 0], [00:00:07.598,  4 ms], [fan = 75%, 2921 rpm, 57°C], 32.287399 MH/s (194.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:00:12.481, 14 ms], [fan = 75%, 1865 rpm, 50°C], 26.756957 MH/s (179.46 W) = 59.044356 MH/s (373.46 W)

>>> thread ID: 0x990, 2021.08.01 14:35:05.953, 7875 ms
{"id":null,"method":"mining.notify","params":["b185cfd0a9149e570835","6bf9cf649ec6a4ff8f01958e63391add7c2b023561de377aa8b5b111be051c49","c61dd6e690b0e87b596a70c4a7451cb67103f3cb830b1c691e5466cec15df702","00000009f6000000000000000000000000000000000000000000000000000000",false,1866617,"1b0135ad"]}

--- thread ID: 0x990, 2021.08.01 14:35:05.953
epoch = 248 (next epoch in 883 blocks), seed = 622205 (next seed in 1 block), share difficulty = 0.43118103 GH.

--- thread ID: 0x14b0, 2021.08.01 14:35:20.668, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:01:00.176)
PCIe: 00000000:03:00.0, GPU.01: [A = 4, S = 0, R = 0, I = 0], [00:00:22.612, 10 ms], [fan = 75%, 2921 rpm, 58°C], 32.296031 MH/s (194.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 2, S = 0, R = 0, I = 0], [00:00:27.495, 13 ms], [fan = 75%, 1859 rpm, 52°C], 26.709731 MH/s (179.34 W) = 59.005762 MH/s (373.34 W)

--- thread ID: 0x7f4, 2021.08.01 14:35:26.799, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 0).
 nonce: 0x0b8e5b004946c30f
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000001da6b788a248ba0d92d0ab4f7a91b4b2c24915086537f080416a60120
   mix: 0x647b593e74ce3dd5781610ab444bfbb01bcb34cd274eb012385142abe15b2dd4

<<< thread ID: 0x760, 2021.08.01 14:35:26.799, 0 ms
{"jsonrpc":"2.0","id":1007,"method":"mining.submit","params":["....alphagruis","b185cfd0a9149e570835","0x0b8e5b004946c30f","0x6bf9cf649ec6a4ff8f01958e63391add7c2b023561de377aa8b5b111be051c49","0x647b593e74ce3dd5781610ab444bfbb01bcb34cd274eb012385142abe15b2dd4"],"worker":"alphagruis"}

--- thread ID: 0x5d8, 2021.08.01 14:35:26.822, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x5d8, 2021.08.01 14:35:26.822, 20868 ms (22 ms)
{"id":1007,"result":true,"error":null}

--- thread ID: 0x7f4, 2021.08.01 14:35:29.315, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 1).
 nonce: 0x0b8e5b005220f835
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x0000000357add7e25a8a06183930cdccf39774e02de015f0f6d5b586f2afc29c
   mix: 0xde3708dbf5ac66fb7939df683d0b7399110be4d3c0199d1614f0e8131ae59265

<<< thread ID: 0x6d0, 2021.08.01 14:35:29.315, 0 ms
{"jsonrpc":"2.0","id":1008,"method":"mining.submit","params":["....alphagruis","b185cfd0a9149e570835","0x0b8e5b005220f835","0x6bf9cf649ec6a4ff8f01958e63391add7c2b023561de377aa8b5b111be051c49","0xde3708dbf5ac66fb7939df683d0b7399110be4d3c0199d1614f0e8131ae59265"],"worker":"alphagruis"}

--- thread ID: 0x714, 2021.08.01 14:35:29.337, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x714, 2021.08.01 14:35:29.337, 2515 ms (22 ms)
{"id":1008,"result":true,"error":null}

>>> thread ID: 0x710, 2021.08.01 14:35:31.905, 2567 ms
{"id":null,"method":"mining.notify","params":["55dc20762c5b319a7f07","05b5d0690c0e296b902515f8f66f7af74943ae142a9f9a0cfb7f589fa43971af","c61dd6e690b0e87b596a70c4a7451cb67103f3cb830b1c691e5466cec15df702","00000009f6000000000000000000000000000000000000000000000000000000",true,1866618,"1b0135ae"]}

--- thread ID: 0x710, 2021.08.01 14:35:31.905
epoch = 248 (next epoch in 882 blocks), seed = 622206 (next seed in 3 blocks), share difficulty = 0.43118103 GH.

--- thread ID: 0x1068, 2021.08.01 14:35:31.909
seed = 622207, build PCIe: 00000000:03:00.0, GPU.01 program...

--- thread ID: 0xd28, 2021.08.01 14:35:31.923
seed = 622207, build PCIe: 00000000:07:00.0, GPU.02 program...

--- thread ID: 0xd28, 2021.08.01 14:35:32.291, 367 ms
seed = 622207, build PCIe: 00000000:07:00.0, GPU.02 program: done.

--- thread ID: 0x1068, 2021.08.01 14:35:32.342, 433 ms
seed = 622207, build PCIe: 00000000:03:00.0, GPU.01 program: done.

--- thread ID: 0x14b0, 2021.08.01 14:35:35.682, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:01:15.190)
PCIe: 00000000:03:00.0, GPU.01: [A = 4, S = 0, R = 0, I = 0], [00:00:37.627,  0 ms], [fan = 75%, 2921 rpm, 59°C], 31.314330 MH/s (188.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 4, S = 0, R = 0, I = 0], [00:00:06.367, 16 ms], [fan = 75%, 1865 rpm, 53°C], 26.710547 MH/s (179.65 W) = 58.024877 MH/s (367.65 W)

--- thread ID: 0x7f4, 2021.08.01 14:35:36.740, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 0).
 nonce: 0x0b8e5b00104ad01c
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000000bc4f63c3db2ff691ed53d9dbabcb8677bd1a0b37179074cb88a93280
   mix: 0xd4e2d8d90e320112761ac0134173f73283258ffe084dd311ceace065e2bfc636

<<< thread ID: 0x15b8, 2021.08.01 14:35:36.740, 0 ms
{"jsonrpc":"2.0","id":1009,"method":"mining.submit","params":["....alphagruis","55dc20762c5b319a7f07","0x0b8e5b00104ad01c","0x05b5d0690c0e296b902515f8f66f7af74943ae142a9f9a0cfb7f589fa43971af","0xd4e2d8d90e320112761ac0134173f73283258ffe084dd311ceace065e2bfc636"],"worker":"alphagruis"}

--- thread ID: 0x384, 2021.08.01 14:35:36.763, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x384, 2021.08.01 14:35:36.763, 4857 ms (22 ms)
{"id":1009,"result":true,"error":null}

--- thread ID: 0x7f4, 2021.08.01 14:35:42.945, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 0).
 nonce: 0x0b8e5b0025555d51
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000038ed5d26fa2f7d12169e1580ed8f6616c95259871a5c7833c25d52902
   mix: 0x0f6bd912538cd18110033c6bba60687079517f53b58c8443a33259ab1495c7c7

<<< thread ID: 0x2424, 2021.08.01 14:35:42.945, 0 ms
{"jsonrpc":"2.0","id":1010,"method":"mining.submit","params":["....alphagruis","55dc20762c5b319a7f07","0x0b8e5b0025555d51","0x05b5d0690c0e296b902515f8f66f7af74943ae142a9f9a0cfb7f589fa43971af","0x0f6bd912538cd18110033c6bba60687079517f53b58c8443a33259ab1495c7c7"],"worker":"alphagruis"}

--- thread ID: 0x990, 2021.08.01 14:35:42.967, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x990, 2021.08.01 14:35:42.967, 6204 ms (21 ms)
{"id":1010,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:35:43.780, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b00282a3b8c
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x0000000306fb56b666f44d92ab8abad4cb6e790884b1fcc3dbda7ec7874e97f8
   mix: 0x8e8eb09fe98c128b576d641fcf153c69cee9db7f2aa09bf35194b312f8847c5f

<<< thread ID: 0x760, 2021.08.01 14:35:43.780, 0 ms
{"jsonrpc":"2.0","id":1011,"method":"mining.submit","params":["....alphagruis","55dc20762c5b319a7f07","0x0b8e5b00282a3b8c","0x05b5d0690c0e296b902515f8f66f7af74943ae142a9f9a0cfb7f589fa43971af","0x8e8eb09fe98c128b576d641fcf153c69cee9db7f2aa09bf35194b312f8847c5f"],"worker":"alphagruis"}

--- thread ID: 0x5d8, 2021.08.01 14:35:43.803, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x5d8, 2021.08.01 14:35:43.803, 835 ms (22 ms)
{"id":1011,"result":true,"error":null}

--- thread ID: 0x7f4, 2021.08.01 14:35:44.476, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 0).
 nonce: 0x0b8e5b002a822311
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000007e94042f61dc43d143183caa8b3b05dbcf03279c1438271c86ad81aee
   mix: 0x475a4820cdeb8714a6d991260537a8be7a4c4515856ee513e51f034ca8509b27

<<< thread ID: 0x6d0, 2021.08.01 14:35:44.476, 0 ms
{"jsonrpc":"2.0","id":1012,"method":"mining.submit","params":["....alphagruis","55dc20762c5b319a7f07","0x0b8e5b002a822311","0x05b5d0690c0e296b902515f8f66f7af74943ae142a9f9a0cfb7f589fa43971af","0x475a4820cdeb8714a6d991260537a8be7a4c4515856ee513e51f034ca8509b27"],"worker":"alphagruis"}

--- thread ID: 0x714, 2021.08.01 14:35:44.499, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x714, 2021.08.01 14:35:44.499, 696 ms (22 ms)
{"id":1012,"result":true,"error":null}

>>> thread ID: 0x710, 2021.08.01 14:35:48.764, 4265 ms
{"id":null,"method":"mining.notify","params":["48dc0950fcbf5097119e","4edc3a71a81d8f64a4d8414cd7227fe76ed6f2967b61013d19559b0c2a1f17ad","c61dd6e690b0e87b596a70c4a7451cb67103f3cb830b1c691e5466cec15df702","00000009f6000000000000000000000000000000000000000000000000000000",true,1866619,"1b013484"]}

--- thread ID: 0x710, 2021.08.01 14:35:48.765
epoch = 248 (next epoch in 881 blocks), seed = 622206 (next seed in 2 blocks), share difficulty = 0.43118103 GH.

--- thread ID: 0x14b0, 2021.08.01 14:35:50.696, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:01:30.205)
PCIe: 00000000:03:00.0, GPU.01: [A = 5, S = 0, R = 0, I = 0], [00:00:06.916, 9 ms], [fan = 75%, 2913 rpm, 59°C], 30.226146 MH/s (188.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 7, S = 0, R = 0, I = 0], [00:00:06.220, 9 ms], [fan = 75%, 1865 rpm, 54°C], 26.663051 MH/s (179.00 W) = 56.889197 MH/s (367.00 W)

--- thread ID: 0x1120, 2021.08.01 14:35:53.857, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b00112f002c
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000014a497d3f02e411e220b356fe0c9b3f0b06227ed36129abd0bc16b486
   mix: 0x9a6ca41e93f91a4cf0eca0b90a5b4de54c665865c2a60eb932d2d19b0aa160ff

<<< thread ID: 0x15b8, 2021.08.01 14:35:53.857, 0 ms
{"jsonrpc":"2.0","id":1013,"method":"mining.submit","params":["....alphagruis","48dc0950fcbf5097119e","0x0b8e5b00112f002c","0x4edc3a71a81d8f64a4d8414cd7227fe76ed6f2967b61013d19559b0c2a1f17ad","0x9a6ca41e93f91a4cf0eca0b90a5b4de54c665865c2a60eb932d2d19b0aa160ff"],"worker":"alphagruis"}

--- thread ID: 0x384, 2021.08.01 14:35:53.879, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x384, 2021.08.01 14:35:53.879, 5114 ms (22 ms)
{"id":1013,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:35:53.996, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 1).
 nonce: 0x0b8e5b0011a648c3
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x0000000446f518bfcf8b78a94a71b6167c8ab2b0722a328a2cad8ecb612b7ee0
   mix: 0x8f2227f978ce0d49a6d0df642b35c697a2bb75bc15771e61e43c746f95d50d45

<<< thread ID: 0x2424, 2021.08.01 14:35:53.996, 0 ms
{"jsonrpc":"2.0","id":1014,"method":"mining.submit","params":["....alphagruis","48dc0950fcbf5097119e","0x0b8e5b0011a648c3","0x4edc3a71a81d8f64a4d8414cd7227fe76ed6f2967b61013d19559b0c2a1f17ad","0x8f2227f978ce0d49a6d0df642b35c697a2bb75bc15771e61e43c746f95d50d45"],"worker":"alphagruis"}

--- thread ID: 0x990, 2021.08.01 14:35:54.020, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x990, 2021.08.01 14:35:54.020, 140 ms (23 ms)
{"id":1014,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:36:05.710, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:01:45.219)
PCIe: 00000000:03:00.0, GPU.01: [A = 7, S = 0, R = 0, I = 0], [00:00:11.714,  4 ms], [fan = 75%, 2913 rpm, 60°C], 30.252980 MH/s (188.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 7, S = 0, R = 0, I = 0], [00:00:21.234, 13 ms], [fan = 75%, 1856 rpm, 54°C], 26.657952 MH/s (179.49 W) = 56.910932 MH/s (367.49 W)

>>> thread ID: 0x760, 2021.08.01 14:36:06.285, 12265 ms
{"id":null,"method":"mining.notify","params":["deeb1758d165ee7b0fe0","38a46d077d6b231465b6bf684c5f209065d0a7b2810a7eeab307f6aca6799401","c61dd6e690b0e87b596a70c4a7451cb67103f3cb830b1c691e5466cec15df702","00000009f6000000000000000000000000000000000000000000000000000000",true,1866620,"1b013508"]}

--- thread ID: 0x760, 2021.08.01 14:36:06.285
epoch = 248 (next epoch in 880 blocks), seed = 622206 (next seed in 1 block), share difficulty = 0.43118103 GH.

--- thread ID: 0x1120, 2021.08.01 14:36:14.873, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b001d119f34
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000023ebb918c9d4a04e188f92f46c2b007181bd20fbfd31d11642c4684fe
   mix: 0x143cccb46b49a1c9497743d4def7b01932d2295e0da728e3591fafff31ae30e2

<<< thread ID: 0x5d8, 2021.08.01 14:36:14.873, 0 ms
{"jsonrpc":"2.0","id":1015,"method":"mining.submit","params":["....alphagruis","deeb1758d165ee7b0fe0","0x0b8e5b001d119f34","0x38a46d077d6b231465b6bf684c5f209065d0a7b2810a7eeab307f6aca6799401","0x143cccb46b49a1c9497743d4def7b01932d2295e0da728e3591fafff31ae30e2"],"worker":"alphagruis"}

--- thread ID: 0x6d0, 2021.08.01 14:36:14.895, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x6d0, 2021.08.01 14:36:14.895, 8609 ms (21 ms)
{"id":1015,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:36:15.401, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b001ed65771
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000002b45d66e646f649d6669a3a39c039e0089ffaae57f8d81cda20b7a35c
   mix: 0x7f215d28bb1f0c60b3c20e833f76376b43992f4a77f89965a8e76744b6daf512

<<< thread ID: 0x714, 2021.08.01 14:36:15.401, 0 ms
{"jsonrpc":"2.0","id":1016,"method":"mining.submit","params":["....alphagruis","deeb1758d165ee7b0fe0","0x0b8e5b001ed65771","0x38a46d077d6b231465b6bf684c5f209065d0a7b2810a7eeab307f6aca6799401","0x7f215d28bb1f0c60b3c20e833f76376b43992f4a77f89965a8e76744b6daf512"],"worker":"alphagruis"}

--- thread ID: 0x710, 2021.08.01 14:36:15.427, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x710, 2021.08.01 14:36:15.427, 531 ms (25 ms)
{"id":1016,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:36:20.738, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:02:00.246)
PCIe: 00000000:03:00.0, GPU.01: [A = 9, S = 0, R = 0, I = 0], [00:00:05.337,  0 ms], [fan = 75%, 2921 rpm, 61°C], 30.233367 MH/s (189.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 7, S = 0, R = 0, I = 0], [00:00:36.262, 14 ms], [fan = 75%, 1862 rpm, 54°C], 26.547102 MH/s (179.36 W) = 56.780469 MH/s (368.36 W)

--- thread ID: 0x1120, 2021.08.01 14:36:26.165, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 1).
 nonce: 0x0b8e5b00435c6c21
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000073d8e5ccc88b6f5b4772debee3d887993a183ffdbf218f919db60cb34
   mix: 0x166337f11fe2f8712264eaf301b77f6178e65e0df88e8a91127f7548ca502728

<<< thread ID: 0x15b8, 2021.08.01 14:36:26.165, 0 ms
{"jsonrpc":"2.0","id":1017,"method":"mining.submit","params":["....alphagruis","deeb1758d165ee7b0fe0","0x0b8e5b00435c6c21","0x38a46d077d6b231465b6bf684c5f209065d0a7b2810a7eeab307f6aca6799401","0x166337f11fe2f8712264eaf301b77f6178e65e0df88e8a91127f7548ca502728"],"worker":"alphagruis"}

--- thread ID: 0x384, 2021.08.01 14:36:26.187, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x384, 2021.08.01 14:36:26.187, 10759 ms (21 ms)
{"id":1017,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:36:28.980, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b004ce03c71
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000004c5fc389a4dc04f556f98eb0c070fa09051facd0699e699d19da84417
   mix: 0x699687748266d4f972fffbf832ae417a64daad9fb08553abb4304f5620a11ebe

<<< thread ID: 0x2424, 2021.08.01 14:36:28.980, 0 ms
{"jsonrpc":"2.0","id":1018,"method":"mining.submit","params":["....alphagruis","deeb1758d165ee7b0fe0","0x0b8e5b004ce03c71","0x38a46d077d6b231465b6bf684c5f209065d0a7b2810a7eeab307f6aca6799401","0x699687748266d4f972fffbf832ae417a64daad9fb08553abb4304f5620a11ebe"],"worker":"alphagruis"}

--- thread ID: 0x990, 2021.08.01 14:36:29.003, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x990, 2021.08.01 14:36:29.003, 2816 ms (22 ms)
{"id":1018,"result":true,"error":null}

--- thread ID: 0x7f4, 2021.08.01 14:36:34.223, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 1).
 nonce: 0x0b8e5b005ea4b27a
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000046c77e8e2d26933adb4724e7fac8a0f61f4080aadba6d24280f07a876
   mix: 0x744339a17254d5f2c2e8c2bdab906d3a0e1748ad4dd67987728f511ab8c580a4

<<< thread ID: 0x760, 2021.08.01 14:36:34.223, 0 ms
{"jsonrpc":"2.0","id":1019,"method":"mining.submit","params":["....alphagruis","deeb1758d165ee7b0fe0","0x0b8e5b005ea4b27a","0x38a46d077d6b231465b6bf684c5f209065d0a7b2810a7eeab307f6aca6799401","0x744339a17254d5f2c2e8c2bdab906d3a0e1748ad4dd67987728f511ab8c580a4"],"worker":"alphagruis"}

--- thread ID: 0x5d8, 2021.08.01 14:36:34.245, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x5d8, 2021.08.01 14:36:34.245, 5241 ms (22 ms)
{"id":1019,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:36:35.766, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:02:15.274)
PCIe: 00000000:03:00.0, GPU.01: [A = 11, S = 0, R = 0, I = 0], [00:00:06.785,  2 ms], [fan = 75%, 2921 rpm, 61°C], 30.240513 MH/s (189.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A =  8, S = 0, R = 0, I = 0], [00:00:01.543, 17 ms], [fan = 75%, 1859 rpm, 55°C], 26.615227 MH/s (179.74 W) = 56.855740 MH/s (368.74 W)

--- thread ID: 0x1120, 2021.08.01 14:36:37.367, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 1).
 nonce: 0x0b8e5b00694a5d35
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x0000000054d8d8c60da5239a5edf14693b4db49eb71bf03e365ec6ca8e9fd766
   mix: 0xbb50e053d5a170274cc516a57e50284c96cea6810ae5a22f5ffd830bf02709ff

<<< thread ID: 0x6d0, 2021.08.01 14:36:37.367, 0 ms
{"jsonrpc":"2.0","id":1020,"method":"mining.submit","params":["....alphagruis","deeb1758d165ee7b0fe0","0x0b8e5b00694a5d35","0x38a46d077d6b231465b6bf684c5f209065d0a7b2810a7eeab307f6aca6799401","0xbb50e053d5a170274cc516a57e50284c96cea6810ae5a22f5ffd830bf02709ff"],"worker":"alphagruis"}

--- thread ID: 0x714, 2021.08.01 14:36:37.389, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x714, 2021.08.01 14:36:37.389, 3144 ms (22 ms)
{"id":1020,"result":true,"error":null}

>>> thread ID: 0x710, 2021.08.01 14:36:42.493, 5103 ms
{"id":null,"method":"mining.notify","params":["15991ac6b82af276b426","b77a3fe87f8dbf98bc51c290ccb0c5eaaab204890ce40b3f2f73de3948978190","c61dd6e690b0e87b596a70c4a7451cb67103f3cb830b1c691e5466cec15df702","00000009f6000000000000000000000000000000000000000000000000000000",true,1866621,"1b013490"]}

--- thread ID: 0x710, 2021.08.01 14:36:42.493
epoch = 248 (next epoch in 879 blocks), seed = 622207 (next seed in 3 blocks), share difficulty = 0.43118103 GH.

--- thread ID: 0x10dc, 2021.08.01 14:36:42.500
seed = 622208, build PCIe: 00000000:03:00.0, GPU.01 program...

--- thread ID: 0xc48, 2021.08.01 14:36:42.501
seed = 622208, build PCIe: 00000000:07:00.0, GPU.02 program...

--- thread ID: 0xc48, 2021.08.01 14:36:42.883, 381 ms
seed = 622208, build PCIe: 00000000:07:00.0, GPU.02 program: done.

--- thread ID: 0x10dc, 2021.08.01 14:36:42.937, 436 ms
seed = 622208, build PCIe: 00000000:03:00.0, GPU.01 program: done.

--- thread ID: 0x7f4, 2021.08.01 14:36:49.375, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 1).
 nonce: 0x0b8e5b0017f9ac8d
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x0000000543468a40f5a73200689d97621afcfe8822615c1787c6c01ce74c422b
   mix: 0xb2b15dd319aba27c491ee5a4d36d19ce5adf775cfed81c5b0560bac4d3aeacc6

<<< thread ID: 0x15b8, 2021.08.01 14:36:49.375, 0 ms
{"jsonrpc":"2.0","id":1021,"method":"mining.submit","params":["....alphagruis","15991ac6b82af276b426","0x0b8e5b0017f9ac8d","0xb77a3fe87f8dbf98bc51c290ccb0c5eaaab204890ce40b3f2f73de3948978190","0xb2b15dd319aba27c491ee5a4d36d19ce5adf775cfed81c5b0560bac4d3aeacc6"],"worker":"alphagruis"}

--- thread ID: 0x384, 2021.08.01 14:36:49.397, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x384, 2021.08.01 14:36:49.397, 6903 ms (22 ms)
{"id":1021,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:36:50.782, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:02:30.290)
PCIe: 00000000:03:00.0, GPU.01: [A = 12, S = 0, R = 0, I = 0], [00:00:13.415, 4 ms], [fan = 75%, 2921 rpm, 63°C], 32.694042 MH/s (196.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A =  9, S = 0, R = 0, I = 0], [00:00:01.407, 5 ms], [fan = 75%, 1860 rpm, 55°C], 25.691191 MH/s (179.76 W) = 58.385233 MH/s (375.76 W)

--- thread ID: 0x7f4, 2021.08.01 14:36:54.134, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 1).
 nonce: 0x0b8e5b00289152cb
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000009a1cb718854406af966f8d3fa1f729d9f0a6798ab2848f2ce2e8f1886
   mix: 0x2fb8f2ccd52489e3f5197faa4f2e714724d652900228b99c81a0d8e8c26cf337

<<< thread ID: 0x2424, 2021.08.01 14:36:54.134, 0 ms
{"jsonrpc":"2.0","id":1022,"method":"mining.submit","params":["....alphagruis","15991ac6b82af276b426","0x0b8e5b00289152cb","0xb77a3fe87f8dbf98bc51c290ccb0c5eaaab204890ce40b3f2f73de3948978190","0x2fb8f2ccd52489e3f5197faa4f2e714724d652900228b99c81a0d8e8c26cf337"],"worker":"alphagruis"}

--- thread ID: 0x990, 2021.08.01 14:36:54.157, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x990, 2021.08.01 14:36:54.157, 4759 ms (22 ms)
{"id":1022,"result":true,"error":null}

--- thread ID: 0x7f4, 2021.08.01 14:36:56.286, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 1).
 nonce: 0x0b8e5b003017a0a2
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000003ca89ef5226e24fd0f0f9a46281d9656977c12bec634d72503bbf882
   mix: 0xd21f5315f50e8a6f83f7d9f1f0a09347a843f416c019dda7f03121fbc4abac25

<<< thread ID: 0x760, 2021.08.01 14:36:56.286, 0 ms
{"jsonrpc":"2.0","id":1023,"method":"mining.submit","params":["....alphagruis","15991ac6b82af276b426","0x0b8e5b003017a0a2","0xb77a3fe87f8dbf98bc51c290ccb0c5eaaab204890ce40b3f2f73de3948978190","0xd21f5315f50e8a6f83f7d9f1f0a09347a843f416c019dda7f03121fbc4abac25"],"worker":"alphagruis"}

--- thread ID: 0x5d8, 2021.08.01 14:36:56.308, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x5d8, 2021.08.01 14:36:56.308, 2151 ms (21 ms)
{"id":1023,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:37:05.783, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:02:45.291)
PCIe: 00000000:03:00.0, GPU.01: [A = 12, S = 0, R = 0, I = 0], [00:00:28.416, 1 ms], [fan = 75%, 2913 rpm, 63°C], 32.909581 MH/s (197.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 11, S = 0, R = 0, I = 0], [00:00:09.496, 3 ms], [fan = 75%, 1863 rpm, 55°C], 25.533866 MH/s (179.86 W) = 58.443447 MH/s (376.86 W)

--- thread ID: 0x7f4, 2021.08.01 14:37:20.376, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 0).
 nonce: 0x0b8e5b00842b936b
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000054cb94f92e89a5049c9ec2085b5cb22fbf8ab03e271ae75b3c14759f1
   mix: 0x937c485ee2da0ce1222caa93768b047e728991b2fb87b8a1aef8d83f8378a763

<<< thread ID: 0x6d0, 2021.08.01 14:37:20.376, 0 ms
{"jsonrpc":"2.0","id":1024,"method":"mining.submit","params":["....alphagruis","15991ac6b82af276b426","0x0b8e5b00842b936b","0xb77a3fe87f8dbf98bc51c290ccb0c5eaaab204890ce40b3f2f73de3948978190","0x937c485ee2da0ce1222caa93768b047e728991b2fb87b8a1aef8d83f8378a763"],"worker":"alphagruis"}

--- thread ID: 0x714, 2021.08.01 14:37:20.399, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x714, 2021.08.01 14:37:20.399, 24091 ms (23 ms)
{"id":1024,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:37:20.783, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:03:00.292)
PCIe: 00000000:03:00.0, GPU.01: [A = 12, S = 0, R = 0, I = 0], [00:00:43.417, 2 ms], [fan = 75%, 2913 rpm, 64°C], 32.888561 MH/s (197.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 12, S = 0, R = 0, I = 0], [00:00:00.408, 2 ms], [fan = 75%, 1862 rpm, 55°C], 25.723188 MH/s (179.29 W) = 58.611749 MH/s (376.29 W)

--- thread ID: 0x1120, 2021.08.01 14:37:21.329, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b008785bf9b
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x0000000338762e47f954f3afdcba68029001c2c92e0bd123b2054f09c8476b17
   mix: 0x4b40b349df983ea31fe58fbf7db7155e2e9429550989c3f4ff7c8d84ad481df8

<<< thread ID: 0x710, 2021.08.01 14:37:21.329, 0 ms
{"jsonrpc":"2.0","id":1025,"method":"mining.submit","params":["....alphagruis","15991ac6b82af276b426","0x0b8e5b008785bf9b","0xb77a3fe87f8dbf98bc51c290ccb0c5eaaab204890ce40b3f2f73de3948978190","0x4b40b349df983ea31fe58fbf7db7155e2e9429550989c3f4ff7c8d84ad481df8"],"worker":"alphagruis"}

--- thread ID: 0x15b8, 2021.08.01 14:37:21.352, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x15b8, 2021.08.01 14:37:21.352, 952 ms (22 ms)
{"id":1025,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:37:35.798, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:03:15.306)
PCIe: 00000000:03:00.0, GPU.01: [A = 13, S = 0, R = 0, I = 0], [00:00:14.468, 1 ms], [fan = 75%, 2913 rpm, 64°C], 32.905724 MH/s (197.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 12, S = 0, R = 0, I = 0], [00:00:15.422, 9 ms], [fan = 75%, 1863 rpm, 55°C], 25.661495 MH/s (179.27 W) = 58.567219 MH/s (376.27 W)

--- thread ID: 0x1120, 2021.08.01 14:37:40.387, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b00ca1225d1
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000000b2992f4faee185e988bb55f70570949103d1ab0a43d2ba451f8dcc9b
   mix: 0x2d92bf5f83ff28bf8999bc61ae24e84adffc00e7b024be18323a0f203bf3ce79

<<< thread ID: 0x384, 2021.08.01 14:37:40.387, 0 ms
{"jsonrpc":"2.0","id":1026,"method":"mining.submit","params":["....alphagruis","15991ac6b82af276b426","0x0b8e5b00ca1225d1","0xb77a3fe87f8dbf98bc51c290ccb0c5eaaab204890ce40b3f2f73de3948978190","0x2d92bf5f83ff28bf8999bc61ae24e84adffc00e7b024be18323a0f203bf3ce79"],"worker":"alphagruis"}

--- thread ID: 0x2424, 2021.08.01 14:37:40.409, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x2424, 2021.08.01 14:37:40.409, 19057 ms (22 ms)
{"id":1026,"result":true,"error":null}

>>> thread ID: 0x990, 2021.08.01 14:37:42.943, 2533 ms
{"id":null,"method":"mining.notify","params":["f53bca83ae0254a60981","bfdf5d510049a8574337ac4985a5f9cfbd03944804c0c9ac400744b4af77a218","c61dd6e690b0e87b596a70c4a7451cb67103f3cb830b1c691e5466cec15df702","00000009f6000000000000000000000000000000000000000000000000000000",false,1866621,"1b013490"]}

--- thread ID: 0x990, 2021.08.01 14:37:42.943
epoch = 248 (next epoch in 879 blocks), seed = 622207 (next seed in 3 blocks), share difficulty = 0.43118103 GH.

--- thread ID: 0x14b0, 2021.08.01 14:37:50.825, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:03:30.334)
PCIe: 00000000:03:00.0, GPU.01: [A = 14, S = 0, R = 0, I = 0], [00:00:10.438, 13 ms], [fan = 75%, 2913 rpm, 64°C], 32.782613 MH/s (196.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 12, S = 0, R = 0, I = 0], [00:00:30.450,  7 ms], [fan = 75%, 1863 rpm, 55°C], 25.673030 MH/s (179.41 W) = 58.455643 MH/s (375.41 W)

--- thread ID: 0x1120, 2021.08.01 14:37:56.332, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 1).
 nonce: 0x0b8e5b002ea466f3
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000003c7d2dbf33593e4287487968597e6beeff334c2321a3da732b4239f74
   mix: 0xf1b5e9be5796f27b2907a1ad5da732fefa4fe3c9facf3da205d1fc17f71f62bd

<<< thread ID: 0x760, 2021.08.01 14:37:56.332, 0 ms
{"jsonrpc":"2.0","id":1027,"method":"mining.submit","params":["....alphagruis","f53bca83ae0254a60981","0x0b8e5b002ea466f3","0xbfdf5d510049a8574337ac4985a5f9cfbd03944804c0c9ac400744b4af77a218","0xf1b5e9be5796f27b2907a1ad5da732fefa4fe3c9facf3da205d1fc17f71f62bd"],"worker":"alphagruis"}

--- thread ID: 0x5d8, 2021.08.01 14:37:56.355, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x5d8, 2021.08.01 14:37:56.355, 13411 ms (22 ms)
{"id":1027,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:38:03.656, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b00482d39fc
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x0000000494962d843c3aa2d21c20d7be85001e860d2ebc17ae891aee0343409d
   mix: 0x56df131ede620156187ff24f36633e0df52c4974d83ce4eb465ecec643326d4d

<<< thread ID: 0x6d0, 2021.08.01 14:38:03.656, 0 ms
{"jsonrpc":"2.0","id":1028,"method":"mining.submit","params":["....alphagruis","f53bca83ae0254a60981","0x0b8e5b00482d39fc","0xbfdf5d510049a8574337ac4985a5f9cfbd03944804c0c9ac400744b4af77a218","0x56df131ede620156187ff24f36633e0df52c4974d83ce4eb465ecec643326d4d"],"worker":"alphagruis"}

--- thread ID: 0x714, 2021.08.01 14:38:03.679, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x714, 2021.08.01 14:38:03.679, 7324 ms (22 ms)
{"id":1028,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:38:05.839, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:03:45.348)
PCIe: 00000000:03:00.0, GPU.01: [A = 16, S = 0, R = 0, I = 0], [00:00:02.183, 6 ms], [fan = 75%, 2913 rpm, 64°C], 32.917772 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 12, S = 0, R = 0, I = 0], [00:00:45.464, 0 ms], [fan = 75%, 1862 rpm, 56°C], 25.679866 MH/s (179.46 W) = 58.597638 MH/s (377.46 W)

--- thread ID: 0x1120, 2021.08.01 14:38:06.950, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 1).
 nonce: 0x0b8e5b0053aecbb0
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000082047f6e79251e5ddb843d69f1071ef1f0e5c0aa0fe61cea713f5fab7
   mix: 0xbebf77d51477add832e9aeba019967902818bb9938d75f5c7f198386a0d708d2

<<< thread ID: 0x710, 2021.08.01 14:38:06.950, 0 ms
{"jsonrpc":"2.0","id":1029,"method":"mining.submit","params":["....alphagruis","f53bca83ae0254a60981","0x0b8e5b0053aecbb0","0xbfdf5d510049a8574337ac4985a5f9cfbd03944804c0c9ac400744b4af77a218","0xbebf77d51477add832e9aeba019967902818bb9938d75f5c7f198386a0d708d2"],"worker":"alphagruis"}

--- thread ID: 0x15b8, 2021.08.01 14:38:06.972, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x15b8, 2021.08.01 14:38:06.972, 3293 ms (22 ms)
{"id":1029,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:38:20.854, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:04:00.362)
PCIe: 00000000:03:00.0, GPU.01: [A = 17, S = 0, R = 0, I = 0], [00:00:13.903, 2 ms], [fan = 75%, 2921 rpm, 65°C], 32.904669 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 12, S = 0, R = 0, I = 0], [00:01:00.478, 2 ms], [fan = 75%, 1863 rpm, 56°C], 25.711233 MH/s (179.74 W) = 58.615902 MH/s (377.74 W)

--- thread ID: 0x7f4, 2021.08.01 14:38:32.975, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 0).
 nonce: 0x0b8e5b00b406e678
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000086bce7baa6e8c8a600097097aa912620cecd9a90926fc8139c60a7b3d
   mix: 0x1896101a03721acbfcca1ef16b72b1be8ce7d0319786f08cb88acc33914ee153

<<< thread ID: 0x384, 2021.08.01 14:38:32.975, 0 ms
{"jsonrpc":"2.0","id":1030,"method":"mining.submit","params":["....alphagruis","f53bca83ae0254a60981","0x0b8e5b00b406e678","0xbfdf5d510049a8574337ac4985a5f9cfbd03944804c0c9ac400744b4af77a218","0x1896101a03721acbfcca1ef16b72b1be8ce7d0319786f08cb88acc33914ee153"],"worker":"alphagruis"}

--- thread ID: 0x2424, 2021.08.01 14:38:32.997, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x2424, 2021.08.01 14:38:32.997, 26024 ms (21 ms)
{"id":1030,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:38:34.311, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:04:13.819)
PCIe: 00000000:03:00.0, GPU.01: [A = 17, S = 0, R = 0, I = 0], [00:00:28.931, 11 ms], [fan = 75%, 2913 rpm, 65°C], 32.901248 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 13, S = 0, R = 0, I = 0], [00:00:01.336, 14 ms], [fan = 75%, 1859 rpm, 56°C], 25.709347 MH/s (179.52 W) = 58.610595 MH/s (377.52 W)

--- thread ID: 0x7f4, 2021.08.01 14:38:34.755, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 0).
 nonce: 0x0b8e5b00ba424cda
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000094637976b9a2d7ab36b71968322418f80593779caeb46b91838770a35
   mix: 0xabf42d94730f32983158609fd36bd27621f9d97dd497070d3c3a9d4d5ecdedef

<<< thread ID: 0x990, 2021.08.01 14:38:34.755, 0 ms
{"jsonrpc":"2.0","id":1031,"method":"mining.submit","params":["....alphagruis","f53bca83ae0254a60981","0x0b8e5b00ba424cda","0xbfdf5d510049a8574337ac4985a5f9cfbd03944804c0c9ac400744b4af77a218","0xabf42d94730f32983158609fd36bd27621f9d97dd497070d3c3a9d4d5ecdedef"],"worker":"alphagruis"}

--- thread ID: 0x760, 2021.08.01 14:38:34.777, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x760, 2021.08.01 14:38:34.777, 1780 ms (21 ms)
{"id":1031,"result":true,"error":null}

>>> thread ID: 0x5d8, 2021.08.01 14:38:41.899, 7121 ms
{"id":null,"method":"mining.notify","params":["f97b0108acb5e2a2c596","986571f6aeef8110034c8a9b6869c3d00f34b58bbf604a4a171f246ed6ae224e","c61dd6e690b0e87b596a70c4a7451cb67103f3cb830b1c691e5466cec15df702","00000009f6000000000000000000000000000000000000000000000000000000",false,1866621,"1b013490"]}

--- thread ID: 0x5d8, 2021.08.01 14:38:41.899
epoch = 248 (next epoch in 879 blocks), seed = 622207 (next seed in 3 blocks), share difficulty = 0.43118103 GH.

--- thread ID: 0x14b0, 2021.08.01 14:38:49.312, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:04:28.820)
PCIe: 00000000:03:00.0, GPU.01: [A = 17, S = 0, R = 0, I = 0], [00:00:43.932, 4 ms], [fan = 75%, 2921 rpm, 65°C], 32.926071 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 14, S = 0, R = 0, I = 0], [00:00:14.556, 9 ms], [fan = 75%, 1865 rpm, 56°C], 25.713997 MH/s (179.76 W) = 58.640068 MH/s (377.76 W)

--- thread ID: 0x7f4, 2021.08.01 14:38:51.369, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 1).
 nonce: 0x0b8e5b00210352da
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000074c1a9cee49d2be1e8e48d69b5ed3f0b6b65690598af8fe5e69bf3bed
   mix: 0x938b0aa679afe56477da1b6926f1c778f97841566ad0c91c63f38a71bd8862a7

<<< thread ID: 0x6d0, 2021.08.01 14:38:51.369, 0 ms
{"jsonrpc":"2.0","id":1032,"method":"mining.submit","params":["....alphagruis","f97b0108acb5e2a2c596","0x0b8e5b00210352da","0x986571f6aeef8110034c8a9b6869c3d00f34b58bbf604a4a171f246ed6ae224e","0x938b0aa679afe56477da1b6926f1c778f97841566ad0c91c63f38a71bd8862a7"],"worker":"alphagruis"}

--- thread ID: 0x714, 2021.08.01 14:38:51.392, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x714, 2021.08.01 14:38:51.392, 9493 ms (23 ms)
{"id":1032,"result":true,"error":null}

--- thread ID: 0x7f4, 2021.08.01 14:39:00.455, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 0).
 nonce: 0x0b8e5b0040a65787
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000025d7636eef710611d6ef87189165963da5662d882256189ed6e9457dc
   mix: 0x384b433ec8c4ef5d2fdc88cf44073be277779defc8e1def53a3233c91202b259

<<< thread ID: 0x710, 2021.08.01 14:39:00.456, 0 ms
{"jsonrpc":"2.0","id":1033,"method":"mining.submit","params":["....alphagruis","f97b0108acb5e2a2c596","0x0b8e5b0040a65787","0x986571f6aeef8110034c8a9b6869c3d00f34b58bbf604a4a171f246ed6ae224e","0x384b433ec8c4ef5d2fdc88cf44073be277779defc8e1def53a3233c91202b259"],"worker":"alphagruis"}

--- thread ID: 0x15b8, 2021.08.01 14:39:00.480, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x15b8, 2021.08.01 14:39:00.480, 9087 ms (24 ms)
{"id":1033,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:39:04.326, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:04:43.834)
PCIe: 00000000:03:00.0, GPU.01: [A = 17, S = 0, R = 0, I = 0], [00:00:58.946, 2 ms], [fan = 75%, 2921 rpm, 65°C], 32.904487 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 16, S = 0, R = 0, I = 0], [00:00:03.870, 0 ms], [fan = 75%, 1860 rpm, 56°C], 25.611784 MH/s (179.54 W) = 58.516271 MH/s (377.54 W)

--- thread ID: 0x1120, 2021.08.01 14:39:04.970, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 1).
 nonce: 0x0b8e5b00506e455d
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000008f4400cb29e2efe458bf7a5c054c75467172e75dad06d6e2d715ab057
   mix: 0xe851adf453505e34d8dad500ee5d45d332bdcd15a83033fc99dcc49785b6adb7

<<< thread ID: 0x384, 2021.08.01 14:39:04.970, 0 ms
{"jsonrpc":"2.0","id":1034,"method":"mining.submit","params":["....alphagruis","f97b0108acb5e2a2c596","0x0b8e5b00506e455d","0x986571f6aeef8110034c8a9b6869c3d00f34b58bbf604a4a171f246ed6ae224e","0xe851adf453505e34d8dad500ee5d45d332bdcd15a83033fc99dcc49785b6adb7"],"worker":"alphagruis"}

--- thread ID: 0x2424, 2021.08.01 14:39:04.992, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x2424, 2021.08.01 14:39:04.992, 4512 ms (22 ms)
{"id":1034,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:39:10.728, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 1).
 nonce: 0x0b8e5b00648374de
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000004f467fa0a51389d2a335b61cd0c6fce767dbc0ca200fe69c12b2fb9e5
   mix: 0x046630de4a8f19b24cdf61db2a56213a4bc8dbf647f1606bfcd96d5d7a880642

<<< thread ID: 0x990, 2021.08.01 14:39:10.728, 0 ms
{"jsonrpc":"2.0","id":1035,"method":"mining.submit","params":["....alphagruis","f97b0108acb5e2a2c596","0x0b8e5b00648374de","0x986571f6aeef8110034c8a9b6869c3d00f34b58bbf604a4a171f246ed6ae224e","0x046630de4a8f19b24cdf61db2a56213a4bc8dbf647f1606bfcd96d5d7a880642"],"worker":"alphagruis"}

--- thread ID: 0x760, 2021.08.01 14:39:10.749, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x760, 2021.08.01 14:39:10.749, 5756 ms (21 ms)
{"id":1035,"result":true,"error":null}

>>> thread ID: 0x5d8, 2021.08.01 14:39:14.599, 3849 ms
{"id":null,"method":"mining.notify","params":["c6cf908dfb20110c8d8b","f096943e0ee8b3ff25f1803f21d98e3d2a404b2721458d3a6d759ad636cc75a9","c61dd6e690b0e87b596a70c4a7451cb67103f3cb830b1c691e5466cec15df702","00000009f6000000000000000000000000000000000000000000000000000000",true,1866622,"1b0138ed"]}

--- thread ID: 0x5d8, 2021.08.01 14:39:14.599
epoch = 248 (next epoch in 878 blocks), seed = 622207 (next seed in 2 blocks), share difficulty = 0.43118103 GH.

--- thread ID: 0x14b0, 2021.08.01 14:39:19.353, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:04:58.862)
PCIe: 00000000:03:00.0, GPU.01: [A = 19, S = 0, R = 0, I = 0], [00:00:08.626,  8 ms], [fan = 75%, 2913 rpm, 66°C], 32.902834 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 16, S = 0, R = 0, I = 0], [00:00:18.898, 15 ms], [fan = 75%, 1860 rpm, 56°C], 25.600175 MH/s (179.76 W) = 58.503009 MH/s (377.76 W)

>>> thread ID: 0x6d0, 2021.08.01 14:39:27.196, 12596 ms
{"id":null,"method":"mining.notify","params":["4ea1ec273edcce621e7b","df81c109fb5516608d728f2a742ad3b0bbb0586a54137ebceb2b798fb0d89eb3","c61dd6e690b0e87b596a70c4a7451cb67103f3cb830b1c691e5466cec15df702","00000009f6000000000000000000000000000000000000000000000000000000",true,1866623,"1b012e3d"]}

--- thread ID: 0x6d0, 2021.08.01 14:39:27.196
epoch = 248 (next epoch in 877 blocks), seed = 622207 (next seed in 1 block), share difficulty = 0.43118103 GH.

--- thread ID: 0x14b0, 2021.08.01 14:39:34.356, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:05:13.865)
PCIe: 00000000:03:00.0, GPU.01: [A = 19, S = 0, R = 0, I = 0], [00:00:23.629, 8 ms], [fan = 75%, 2905 rpm, 66°C], 32.916013 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 16, S = 0, R = 0, I = 0], [00:00:33.901, 9 ms], [fan = 75%, 1867 rpm, 56°C], 25.544433 MH/s (179.68 W) = 58.460446 MH/s (377.68 W)

--- thread ID: 0x7f4, 2021.08.01 14:39:42.037, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 0).
 nonce: 0x0b8e5b0033b1be54
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000007794a7edeb8d1db6e0cc208ab845a1ff316fc3d61201b950253b0bea1
   mix: 0xb61a53e7b70c9a485509ca170b19da4e3911dfda3e5e5059dbf876dc7a986a5c

<<< thread ID: 0x714, 2021.08.01 14:39:42.037, 0 ms
{"jsonrpc":"2.0","id":1036,"method":"mining.submit","params":["....alphagruis","4ea1ec273edcce621e7b","0x0b8e5b0033b1be54","0xdf81c109fb5516608d728f2a742ad3b0bbb0586a54137ebceb2b798fb0d89eb3","0xb61a53e7b70c9a485509ca170b19da4e3911dfda3e5e5059dbf876dc7a986a5c"],"worker":"alphagruis"}

--- thread ID: 0x710, 2021.08.01 14:39:42.059, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x710, 2021.08.01 14:39:42.059, 14863 ms (22 ms)
{"id":1036,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:39:42.507, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b00356198b2
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000002b33881e0202156382f5050db0091cef73fa639d1508884bf3001e9fe
   mix: 0xede36d8e557f4bdc1c3ebc0ed23b5579d3fca0636f2b334097a5368644ccfece

<<< thread ID: 0x15b8, 2021.08.01 14:39:42.507, 0 ms
{"jsonrpc":"2.0","id":1037,"method":"mining.submit","params":["....alphagruis","4ea1ec273edcce621e7b","0x0b8e5b00356198b2","0xdf81c109fb5516608d728f2a742ad3b0bbb0586a54137ebceb2b798fb0d89eb3","0xede36d8e557f4bdc1c3ebc0ed23b5579d3fca0636f2b334097a5368644ccfece"],"worker":"alphagruis"}

--- thread ID: 0x384, 2021.08.01 14:39:42.529, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x384, 2021.08.01 14:39:42.529, 469 ms (21 ms)
{"id":1037,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:39:49.357, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:05:28.865)
PCIe: 00000000:03:00.0, GPU.01: [A = 20, S = 0, R = 0, I = 0], [00:00:06.850,  6 ms], [fan = 75%, 2921 rpm, 66°C], 32.910253 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 17, S = 0, R = 0, I = 0], [00:00:07.320, 17 ms], [fan = 75%, 1865 rpm, 56°C], 25.737337 MH/s (179.69 W) = 58.647590 MH/s (377.69 W)

--- thread ID: 0x1120, 2021.08.01 14:40:01.899, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 1).
 nonce: 0x0b8e5b007938ce0e
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000003880fbdfb166b052d61a37b619b95eee6468a925fbcf8d6e88f854a72
   mix: 0x17c0022ced2c55747208913a94ae47a8c8cf1b5cfc3686dd6579d7f08d26b65a

<<< thread ID: 0x2424, 2021.08.01 14:40:01.899, 0 ms
{"jsonrpc":"2.0","id":1038,"method":"mining.submit","params":["....alphagruis","4ea1ec273edcce621e7b","0x0b8e5b007938ce0e","0xdf81c109fb5516608d728f2a742ad3b0bbb0586a54137ebceb2b798fb0d89eb3","0x17c0022ced2c55747208913a94ae47a8c8cf1b5cfc3686dd6579d7f08d26b65a"],"worker":"alphagruis"}

--- thread ID: 0x990, 2021.08.01 14:40:01.923, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x990, 2021.08.01 14:40:01.923, 19394 ms (23 ms)
{"id":1038,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:40:04.385, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:05:43.893)
PCIe: 00000000:03:00.0, GPU.01: [A = 21, S = 0, R = 0, I = 0], [00:00:02.485, 11 ms], [fan = 75%, 2913 rpm, 66°C], 32.906227 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 17, S = 0, R = 0, I = 0], [00:00:22.348, 15 ms], [fan = 75%, 1861 rpm, 56°C], 25.822748 MH/s (179.51 W) = 58.728975 MH/s (377.51 W)

--- thread ID: 0x1120, 2021.08.01 14:40:09.956, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 1).
 nonce: 0x0b8e5b00956bf07f
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000009e0456e8f0e8af40532592538a4d1a0a8288731fa2d48707e09c803e7
   mix: 0x6789c4ccfbdebab1b5e73be1cbb3ea4d5929c12686e4e7b0e95ba58c2b82d4e8

<<< thread ID: 0x760, 2021.08.01 14:40:09.956, 0 ms
{"jsonrpc":"2.0","id":1039,"method":"mining.submit","params":["....alphagruis","4ea1ec273edcce621e7b","0x0b8e5b00956bf07f","0xdf81c109fb5516608d728f2a742ad3b0bbb0586a54137ebceb2b798fb0d89eb3","0x6789c4ccfbdebab1b5e73be1cbb3ea4d5929c12686e4e7b0e95ba58c2b82d4e8"],"worker":"alphagruis"}

--- thread ID: 0x5d8, 2021.08.01 14:40:09.978, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x5d8, 2021.08.01 14:40:09.978, 8054 ms (22 ms)
{"id":1039,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:40:19.385, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:05:58.894)
PCIe: 00000000:03:00.0, GPU.01: [A = 22, S = 0, R = 0, I = 0], [00:00:09.430, 2 ms], [fan = 75%, 2905 rpm, 66°C], 32.908783 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 17, S = 0, R = 0, I = 0], [00:00:37.349, 4 ms], [fan = 75%, 1857 rpm, 56°C], 25.747710 MH/s (179.46 W) = 58.656493 MH/s (377.46 W)

--- thread ID: 0x1120, 2021.08.01 14:40:27.148, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 1).
 nonce: 0x0b8e5b00d198ef39
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000049224ee706c30e201638fb2ed96cc9c8e8583b2b428da2f954b481215
   mix: 0xdd4fe750d5574ab89306a9fb0ed4f41c491a8241a5ea0ccb846eccd3378ea1f4

<<< thread ID: 0x6d0, 2021.08.01 14:40:27.148, 0 ms
{"jsonrpc":"2.0","id":1040,"method":"mining.submit","params":["....alphagruis","4ea1ec273edcce621e7b","0x0b8e5b00d198ef39","0xdf81c109fb5516608d728f2a742ad3b0bbb0586a54137ebceb2b798fb0d89eb3","0xdd4fe750d5574ab89306a9fb0ed4f41c491a8241a5ea0ccb846eccd3378ea1f4"],"worker":"alphagruis"}

--- thread ID: 0x714, 2021.08.01 14:40:27.171, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x714, 2021.08.01 14:40:27.171, 17192 ms (22 ms)
{"id":1040,"result":true,"error":null}

>>> thread ID: 0x710, 2021.08.01 14:40:27.500, 329 ms
{"id":null,"method":"mining.notify","params":["2bd159f66cccab91c852","45b87ad7349f62be4628b11ad3d6f937cbc0d22f5f8b712d96f26a5b32af811c","c61dd6e690b0e87b596a70c4a7451cb67103f3cb830b1c691e5466cec15df702","00000009f6000000000000000000000000000000000000000000000000000000",false,1866623,"1b012e3d"]}

--- thread ID: 0x710, 2021.08.01 14:40:27.500
epoch = 248 (next epoch in 877 blocks), seed = 622207 (next seed in 1 block), share difficulty = 0.43118103 GH.

--- thread ID: 0x1120, 2021.08.01 14:40:27.808, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b0001078cdb
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000005f99eaf22cdce8cffa368266b7f8d9fd8fbddd343a5abe9bef634f35b
   mix: 0x0ce83a6c21d58dccf0e775dd0f55c0fc6755c49d8ae443abede9d3b29fb666a3

<<< thread ID: 0x15b8, 2021.08.01 14:40:27.809, 0 ms
{"jsonrpc":"2.0","id":1041,"method":"mining.submit","params":["....alphagruis","2bd159f66cccab91c852","0x0b8e5b0001078cdb","0x45b87ad7349f62be4628b11ad3d6f937cbc0d22f5f8b712d96f26a5b32af811c","0x0ce83a6c21d58dccf0e775dd0f55c0fc6755c49d8ae443abede9d3b29fb666a3"],"worker":"alphagruis"}

--- thread ID: 0x384, 2021.08.01 14:40:27.831, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x384, 2021.08.01 14:40:27.831, 330 ms (22 ms)
{"id":1041,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:40:28.650, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b0003f85d0d
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000016c8a21b4a6a704956945acaeed0e0c8275d59c59cf7d671577dc2ca0
   mix: 0x16d8ab22d7077c1db72dde054b8af9a2ec9d59607fb5f6e6336d37ba62e0ae09

<<< thread ID: 0x2424, 2021.08.01 14:40:28.650, 0 ms
{"jsonrpc":"2.0","id":1042,"method":"mining.submit","params":["....alphagruis","2bd159f66cccab91c852","0x0b8e5b0003f85d0d","0x45b87ad7349f62be4628b11ad3d6f937cbc0d22f5f8b712d96f26a5b32af811c","0x16d8ab22d7077c1db72dde054b8af9a2ec9d59607fb5f6e6336d37ba62e0ae09"],"worker":"alphagruis"}

--- thread ID: 0x990, 2021.08.01 14:40:28.674, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x990, 2021.08.01 14:40:28.674, 842 ms (23 ms)
{"id":1042,"result":true,"error":null}

--- thread ID: 0x7f4, 2021.08.01 14:40:32.507, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 0).
 nonce: 0x0b8e5b001170ad06
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x0000000274c99ba820f6ef0d1752f9e9e1ee4597390f3d0196d365091e6fc787
   mix: 0x3b777bc3ec970bc96ea295e0b804bad8fcc89138181c484324811312d19bee07

<<< thread ID: 0x760, 2021.08.01 14:40:32.507, 0 ms
{"jsonrpc":"2.0","id":1043,"method":"mining.submit","params":["....alphagruis","2bd159f66cccab91c852","0x0b8e5b001170ad06","0x45b87ad7349f62be4628b11ad3d6f937cbc0d22f5f8b712d96f26a5b32af811c","0x3b777bc3ec970bc96ea295e0b804bad8fcc89138181c484324811312d19bee07"],"worker":"alphagruis"}

--- thread ID: 0x5d8, 2021.08.01 14:40:32.530, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x5d8, 2021.08.01 14:40:32.530, 3856 ms (22 ms)
{"id":1043,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:40:34.386, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:06:13.894)
PCIe: 00000000:03:00.0, GPU.01: [A = 25, S = 0, R = 0, I = 0], [00:00:05.736,  3 ms], [fan = 75%, 2913 rpm, 66°C], 32.891539 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 18, S = 0, R = 0, I = 0], [00:00:01.879, 12 ms], [fan = 75%, 1859 rpm, 56°C], 25.820279 MH/s (179.69 W) = 58.711818 MH/s (377.69 W)

--- thread ID: 0x7f4, 2021.08.01 14:40:40.119, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 1).
 nonce: 0x0b8e5b002c168c22
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000010e68f6081914bfaf977a8755c30e819bbe4f11433a9e8314942e41cc
   mix: 0xc2c881729dac8fbe2b6dc7415ed15b9d7cfba1cdb2b12826beb43cdf85a04da0

<<< thread ID: 0x6d0, 2021.08.01 14:40:40.119, 0 ms
{"jsonrpc":"2.0","id":1044,"method":"mining.submit","params":["....alphagruis","2bd159f66cccab91c852","0x0b8e5b002c168c22","0x45b87ad7349f62be4628b11ad3d6f937cbc0d22f5f8b712d96f26a5b32af811c","0xc2c881729dac8fbe2b6dc7415ed15b9d7cfba1cdb2b12826beb43cdf85a04da0"],"worker":"alphagruis"}

--- thread ID: 0x714, 2021.08.01 14:40:40.141, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x714, 2021.08.01 14:40:40.141, 7611 ms (22 ms)
{"id":1044,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:40:40.400, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b002d122b47
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000000757c8cb1e9ad14f6fc07a002d0428139f1c168b3cd084f5699008a86
   mix: 0x7e1aa2b530dc1d18ebc7e0934d081173d625baf6a4d93979e6eb2a5bd7c4850c

<<< thread ID: 0x710, 2021.08.01 14:40:40.400, 0 ms
{"jsonrpc":"2.0","id":1045,"method":"mining.submit","params":["....alphagruis","2bd159f66cccab91c852","0x0b8e5b002d122b47","0x45b87ad7349f62be4628b11ad3d6f937cbc0d22f5f8b712d96f26a5b32af811c","0x7e1aa2b530dc1d18ebc7e0934d081173d625baf6a4d93979e6eb2a5bd7c4850c"],"worker":"alphagruis"}

--- thread ID: 0x15b8, 2021.08.01 14:40:40.422, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x15b8, 2021.08.01 14:40:40.422, 280 ms (22 ms)
{"id":1045,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:40:45.177, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 1).
 nonce: 0x0b8e5b003dceb381
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000008cc0f375c4077d41cb159b62ac6d07126dd815997e62de47009e9e4f
   mix: 0xcd25c420276e33ad295367250ada160a5126010eae52d5225c4216fe88d18f53

<<< thread ID: 0x384, 2021.08.01 14:40:45.177, 0 ms
{"jsonrpc":"2.0","id":1046,"method":"mining.submit","params":["....alphagruis","2bd159f66cccab91c852","0x0b8e5b003dceb381","0x45b87ad7349f62be4628b11ad3d6f937cbc0d22f5f8b712d96f26a5b32af811c","0xcd25c420276e33ad295367250ada160a5126010eae52d5225c4216fe88d18f53"],"worker":"alphagruis"}

--- thread ID: 0x2424, 2021.08.01 14:40:45.199, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x2424, 2021.08.01 14:40:45.199, 4776 ms (22 ms)
{"id":1046,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:40:49.415, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:06:28.924)
PCIe: 00000000:03:00.0, GPU.01: [A = 27, S = 0, R = 0, I = 0], [00:00:04.238,  5 ms], [fan = 75%, 2913 rpm, 66°C], 32.921263 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 19, S = 0, R = 0, I = 0], [00:00:09.296, 11 ms], [fan = 75%, 1862 rpm, 56°C], 25.839599 MH/s (179.59 W) = 58.760862 MH/s (377.59 W)

--- thread ID: 0x7f4, 2021.08.01 14:40:57.394, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 1).
 nonce: 0x0b8e5b0068912880
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000003c1f654dba3547f46a9e24f37dacb8f83a6a16ebbae95d07bc7e089cd
   mix: 0x950b4d0ad880955310ea99a2799e397a35af84d6f4c77f924279a4ce327666d2

<<< thread ID: 0x990, 2021.08.01 14:40:57.394, 0 ms
{"jsonrpc":"2.0","id":1047,"method":"mining.submit","params":["....alphagruis","2bd159f66cccab91c852","0x0b8e5b0068912880","0x45b87ad7349f62be4628b11ad3d6f937cbc0d22f5f8b712d96f26a5b32af811c","0x950b4d0ad880955310ea99a2799e397a35af84d6f4c77f924279a4ce327666d2"],"worker":"alphagruis"}

--- thread ID: 0x760, 2021.08.01 14:40:57.416, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x760, 2021.08.01 14:40:57.416, 12217 ms (22 ms)
{"id":1047,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:40:57.890, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b006a4bca9e
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000006231fa534f29a044b160be59d1ae5630fb3a54ce9e0d51b2b61d865c0
   mix: 0x9df7662032a7a6575801e08533bf3123b2689974e2297fa26e9f022d899cd0aa

<<< thread ID: 0x5d8, 2021.08.01 14:40:57.890, 0 ms
{"jsonrpc":"2.0","id":1048,"method":"mining.submit","params":["....alphagruis","2bd159f66cccab91c852","0x0b8e5b006a4bca9e","0x45b87ad7349f62be4628b11ad3d6f937cbc0d22f5f8b712d96f26a5b32af811c","0x9df7662032a7a6575801e08533bf3123b2689974e2297fa26e9f022d899cd0aa"],"worker":"alphagruis"}

--- thread ID: 0x6d0, 2021.08.01 14:40:57.912, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x6d0, 2021.08.01 14:40:57.912, 495 ms (21 ms)
{"id":1048,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:40:59.510, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 1).
 nonce: 0x0b8e5b006ff810b1
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000091791cf4087eb32fd3ac404540c5db4418b98b26b1992efda8c165524
   mix: 0x8b9157c8af51b01d1ee756b7dbb43a383c2ea9a278978a9dce4eac5a09acbad6

<<< thread ID: 0x714, 2021.08.01 14:40:59.510, 0 ms
{"jsonrpc":"2.0","id":1049,"method":"mining.submit","params":["....alphagruis","2bd159f66cccab91c852","0x0b8e5b006ff810b1","0x45b87ad7349f62be4628b11ad3d6f937cbc0d22f5f8b712d96f26a5b32af811c","0x8b9157c8af51b01d1ee756b7dbb43a383c2ea9a278978a9dce4eac5a09acbad6"],"worker":"alphagruis"}

--- thread ID: 0x710, 2021.08.01 14:40:59.533, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x710, 2021.08.01 14:40:59.533, 1620 ms (22 ms)
{"id":1049,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:41:04.416, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:06:43.924)
PCIe: 00000000:03:00.0, GPU.01: [A = 29, S = 0, R = 0, I = 0], [00:00:04.905,  3 ms], [fan = 75%, 2913 rpm, 66°C], 32.910608 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 20, S = 0, R = 0, I = 0], [00:00:07.022, 16 ms], [fan = 75%, 1861 rpm, 56°C], 25.785052 MH/s (179.63 W) = 58.695660 MH/s (377.63 W)

--- thread ID: 0x14b0, 2021.08.01 14:41:19.430, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:06:58.938)
PCIe: 00000000:03:00.0, GPU.01: [A = 29, S = 0, R = 0, I = 0], [00:00:19.920,  3 ms], [fan = 75%, 2913 rpm, 66°C], 32.919349 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 20, S = 0, R = 0, I = 0], [00:00:22.036, 10 ms], [fan = 75%, 1861 rpm, 56°C], 25.809496 MH/s (179.57 W) = 58.728845 MH/s (377.57 W)

--- thread ID: 0x7f4, 2021.08.01 14:41:19.461, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 0).
 nonce: 0x0b8e5b00b5bf7459
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x0000000555549040e08854afaa4e20ccd9f8d230ff990ff60e11bceae8c9cafa
   mix: 0x187e0b885d8ca6dd293892c824bbb9487b37a5b0d40c7b1fa0e96d9019695aeb

<<< thread ID: 0x15b8, 2021.08.01 14:41:19.461, 0 ms
{"jsonrpc":"2.0","id":1050,"method":"mining.submit","params":["....alphagruis","2bd159f66cccab91c852","0x0b8e5b00b5bf7459","0x45b87ad7349f62be4628b11ad3d6f937cbc0d22f5f8b712d96f26a5b32af811c","0x187e0b885d8ca6dd293892c824bbb9487b37a5b0d40c7b1fa0e96d9019695aeb"],"worker":"alphagruis"}

--- thread ID: 0x384, 2021.08.01 14:41:19.483, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x384, 2021.08.01 14:41:19.483, 19950 ms (21 ms)
{"id":1050,"result":true,"error":null}

--- thread ID: 0x7f4, 2021.08.01 14:41:24.585, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 1).
 nonce: 0x0b8e5b00c7af527d
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000001ad4772fbbe6ccc3639a1e14601ace12b53ae6ccfc27fc18e97144fa7
   mix: 0x04f985a13b2aef6860f265b8229d816a9f2247137ee79ecffc58503929be97c0

<<< thread ID: 0x2424, 2021.08.01 14:41:24.585, 0 ms
{"jsonrpc":"2.0","id":1051,"method":"mining.submit","params":["....alphagruis","2bd159f66cccab91c852","0x0b8e5b00c7af527d","0x45b87ad7349f62be4628b11ad3d6f937cbc0d22f5f8b712d96f26a5b32af811c","0x04f985a13b2aef6860f265b8229d816a9f2247137ee79ecffc58503929be97c0"],"worker":"alphagruis"}

--- thread ID: 0x990, 2021.08.01 14:41:24.607, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x990, 2021.08.01 14:41:24.607, 5123 ms (22 ms)
{"id":1051,"result":true,"error":null}

--- thread ID: 0x1120, 2021.08.01 14:41:25.217, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b00c9e82320
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000009d6d1c9b87303d547fe257d900bce6ae7813a0131641a851b590059f7
   mix: 0x98042d9c8d6919f3bd9f732af525337ab56d5b2edd1af7f5dcac603f1c77f863

<<< thread ID: 0x760, 2021.08.01 14:41:25.217, 0 ms
{"jsonrpc":"2.0","id":1052,"method":"mining.submit","params":["....alphagruis","2bd159f66cccab91c852","0x0b8e5b00c9e82320","0x45b87ad7349f62be4628b11ad3d6f937cbc0d22f5f8b712d96f26a5b32af811c","0x98042d9c8d6919f3bd9f732af525337ab56d5b2edd1af7f5dcac603f1c77f863"],"worker":"alphagruis"}

--- thread ID: 0x5d8, 2021.08.01 14:41:25.239, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x5d8, 2021.08.01 14:41:25.239, 632 ms (22 ms)
{"id":1052,"result":true,"error":null}

>>> thread ID: 0x6d0, 2021.08.01 14:41:27.832, 2593 ms
{"id":null,"method":"mining.notify","params":["9638258012e09b0b86bd","bc7e0e2131c1aed97ddf6443e17e48c6b4f8f6b700a8cad53a8f75d856322e7e","c61dd6e690b0e87b596a70c4a7451cb67103f3cb830b1c691e5466cec15df702","00000009f6000000000000000000000000000000000000000000000000000000",false,1866623,"1b012e3d"]}

--- thread ID: 0x6d0, 2021.08.01 14:41:27.832
epoch = 248 (next epoch in 877 blocks), seed = 622207 (next seed in 1 block), share difficulty = 0.43118103 GH.

--- thread ID: 0x14b0, 2021.08.01 14:41:34.459, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:07:13.967)
PCIe: 00000000:03:00.0, GPU.01: [A = 30, S = 0, R = 0, I = 0], [00:00:09.242, 11 ms], [fan = 75%, 2913 rpm, 66°C], 32.911513 MH/s (198.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 22, S = 0, R = 0, I = 0], [00:00:09.874, 15 ms], [fan = 75%, 1861 rpm, 56°C], 25.736391 MH/s (179.57 W) = 58.647904 MH/s (377.57 W)

>>> thread ID: 0x714, 2021.08.01 14:41:41.730, 13897 ms
{"id":null,"method":"mining.notify","params":["ce6c56ff7d6a9a8c50cb","131c5a21770c0a8cebc1225b9448752f90075b8dea3717e8406d0a4f44611641","c61dd6e690b0e87b596a70c4a7451cb67103f3cb830b1c691e5466cec15df702","00000009f6000000000000000000000000000000000000000000000000000000",true,1866624,"1b013198"]}

--- thread ID: 0x714, 2021.08.01 14:41:41.730
epoch = 248 (next epoch in 876 blocks), seed = 622208 (next seed in 3 blocks), share difficulty = 0.43118103 GH.

--- thread ID: 0x4bc, 2021.08.01 14:41:41.732
seed = 622209, build PCIe: 00000000:03:00.0, GPU.01 program...

--- thread ID: 0x1704, 2021.08.01 14:41:41.749
seed = 622209, build PCIe: 00000000:07:00.0, GPU.02 program...

--- thread ID: 0x1704, 2021.08.01 14:41:42.129, 380 ms
seed = 622209, build PCIe: 00000000:07:00.0, GPU.02 program: done.

--- thread ID: 0x4bc, 2021.08.01 14:41:42.179, 446 ms
seed = 622209, build PCIe: 00000000:03:00.0, GPU.01 program: done.

--- thread ID: 0x1120, 2021.08.01 14:41:48.583, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b0017ecf35b
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x000000089d9a9e15b9320315ab5d04c6e121f9981cee1aa63d9cfd188de07c44
   mix: 0xb90fdaf559589472ad02c8f510b028c8b20776aeaec9bcf8fa50367256770b2c

<<< thread ID: 0x710, 2021.08.01 14:41:48.583, 0 ms
{"jsonrpc":"2.0","id":1053,"method":"mining.submit","params":["....alphagruis","ce6c56ff7d6a9a8c50cb","0x0b8e5b0017ecf35b","0x131c5a21770c0a8cebc1225b9448752f90075b8dea3717e8406d0a4f44611641","0xb90fdaf559589472ad02c8f510b028c8b20776aeaec9bcf8fa50367256770b2c"],"worker":"alphagruis"}

--- thread ID: 0x15b8, 2021.08.01 14:41:48.605, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x15b8, 2021.08.01 14:41:48.605, 6875 ms (22 ms)
{"id":1053,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:41:49.473, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:07:28.982)
PCIe: 00000000:03:00.0, GPU.01: [A = 31, S = 0, R = 0, I = 0], [00:00:00.890, 13 ms], [fan = 75%, 2905 rpm, 67°C], 32.778048 MH/s (202.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 22, S = 0, R = 0, I = 0], [00:00:24.888, 12 ms], [fan = 75%, 1858 rpm, 56°C], 25.878814 MH/s (179.70 W) = 58.656862 MH/s (381.70 W)

--- thread ID: 0x14b0, 2021.08.01 14:42:04.487, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:07:43.996)
PCIe: 00000000:03:00.0, GPU.01: [A = 31, S = 0, R = 0, I = 0], [00:00:15.905, 11 ms], [fan = 75%, 2913 rpm, 67°C], 32.801819 MH/s (202.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 22, S = 0, R = 0, I = 0], [00:00:39.902,  0 ms], [fan = 75%, 1862 rpm, 56°C], 25.967802 MH/s (179.51 W) = 58.769621 MH/s (381.51 W)

--- thread ID: 0x1120, 2021.08.01 14:42:15.908, PCIe: 00000000:03:00.0, GPU.01 share found (search channel 0).
 nonce: 0x0b8e5b00777370d7
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000006d4c4a9ea7bb7cb5c38c8ed025cf9dc669f58dceb0389689a37e883f7
   mix: 0x955384c9b72730ea90d01174116e3b2370e50eebfd10f3c2635a6470a50dcbce

<<< thread ID: 0x384, 2021.08.01 14:42:15.908, 0 ms
{"jsonrpc":"2.0","id":1054,"method":"mining.submit","params":["....alphagruis","ce6c56ff7d6a9a8c50cb","0x0b8e5b00777370d7","0x131c5a21770c0a8cebc1225b9448752f90075b8dea3717e8406d0a4f44611641","0x955384c9b72730ea90d01174116e3b2370e50eebfd10f3c2635a6470a50dcbce"],"worker":"alphagruis"}

--- thread ID: 0x2424, 2021.08.01 14:42:15.931, PCIe: 00000000:03:00.0, GPU.01 share accepted.

>>> thread ID: 0x2424, 2021.08.01 14:42:15.931, 27325 ms (22 ms)
{"id":1054,"result":true,"error":null}

--- thread ID: 0x14b0, 2021.08.01 14:42:19.515, stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:07:59.024)
PCIe: 00000000:03:00.0, GPU.01: [A = 32, S = 0, R = 0, I = 0], [00:00:03.607,  2 ms], [fan = 75%, 2913 rpm, 67°C], 32.801084 MH/s (202.00 W) +
PCIe: 00000000:07:00.0, GPU.02: [A = 22, S = 0, R = 0, I = 0], [00:00:54.930, 15 ms], [fan = 75%, 1861 rpm, 56°C], 25.804801 MH/s (179.71 W) = 58.605885 MH/s (381.71 W)

--- thread ID: 0x7f4, 2021.08.01 14:42:19.981, PCIe: 00000000:07:00.0, GPU.02 share found (search channel 0).
 nonce: 0x0b8e5b0085a14c32
target: 0x00000009f6000000000000000000000000000000000000000000000000000000
result: 0x00000005034966c9786e6b37a62cc9add7ef86723f04800237193c25b855100a
   mix: 0xad52579a9f7cbda18e41b5bd384798096b28e67d0d6fcce0bfa7c8f723867a84

<<< thread ID: 0x990, 2021.08.01 14:42:19.981, 0 ms
{"jsonrpc":"2.0","id":1055,"method":"mining.submit","params":["....alphagruis","ce6c56ff7d6a9a8c50cb","0x0b8e5b0085a14c32","0x131c5a21770c0a8cebc1225b9448752f90075b8dea3717e8406d0a4f44611641","0xad52579a9f7cbda18e41b5bd384798096b28e67d0d6fcce0bfa7c8f723867a84"],"worker":"alphagruis"}

--- thread ID: 0x760, 2021.08.01 14:42:20.004, PCIe: 00000000:07:00.0, GPU.02 share accepted.

>>> thread ID: 0x760, 2021.08.01 14:42:20.004, 4073 ms (22 ms)
{"id":1055,"result":true,"error":null}

quitting...

--- thread ID: 0x84c, 2021.08.01 14:42:23.378
disconnected from stratum-ravencoin.flypool.org:3443 (172.65.228.1:3443 TLSv1.2, 00:08:02.887)

--- thread ID: 0x1120, 2021.08.01 14:42:23.422
PCIe: 00000000:03:00.0, GPU.01: exit thread.

--- thread ID: 0x7f4, 2021.08.01 14:42:23.428
PCIe: 00000000:07:00.0, GPU.02: exit thread.
```

</p>
</details>
