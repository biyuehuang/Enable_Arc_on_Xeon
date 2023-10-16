# Enable_Arc_on_Xeon
enable multi-dGPU on Xeon server such as 2 Arc A770

## Step 1: 安装DGPU驱动，然后执行以下指令
```
:~$ sudo dmesg | grep i915
[    6.313500] i915 0000:45:00.0: enabling device (0140 -> 0142)
[    6.313803] i915 0000:45:00.0: BAR 0: releasing [mem 0xbc000000-0xbcffffff 64bit]
[    6.313807] i915 0000:45:00.0: BAR 2: releasing [mem 0x202fe0000000-0x202fefffffff 64bit pref]
[    6.313841] i915 0000:45:00.0: BAR 2: no space for [mem size 0x400000000 64bit pref]
[    6.313842] i915 0000:45:00.0: BAR 2: failed to assign [mem size 0x400000000 64bit pref]
[    6.313844] i915 0000:45:00.0: BAR 0: assigned [mem 0xbc000000-0xbcffffff 64bit]
[    6.313892] i915 0000:45:00.0: [drm] Failed to resize BAR2 to 16384M (-ENOSPC)
[    6.313895] i915 0000:45:00.0: BAR 2: assigned [mem 0x202fe0000000-0x202fefffffff 64bit pref]
[    6.313934] i915 0000:45:00.0: [drm] GT count: 1, enabled: 1
[    6.314877] i915 0000:45:00.0: [drm] Using Transparent Hugepages
[    6.315159] i915 0000:45:00.0: [drm] Cannot use the full memory 0x00000003fa000000 on the device as LMEM BAR size was found to be smaller
[    6.315161] i915 0000:45:00.0: [drm] Continuing with reduced LMEM size: 0x0000000010000000
[    6.315182] i915 0000:45:00.0: [drm] Local memory IO size: 0x0000000010000000
[    6.315183] i915 0000:45:00.0: [drm] Local memory available: 0x0000000010000000
[    6.368833] i915 0000:45:00.0: vgaarb: changed VGA decodes: olddecodes=io+mem,decodes=none:owns=none
[    6.372584] i915 0000:45:00.0: [drm] Finished loading DMC firmware i915/dg2_dmc_ver2_07.bin (v2.7)
[    6.381197] i915 0000:45:00.0: [drm] GT0: GuC firmware i915/dg2_guc_70.9.1.bin version 70.9.1
[    6.381202] i915 0000:45:00.0: [drm] GT0: HuC firmware i915/dg2_huc_7.10.3_gsc.bin version 7.10.3
[    6.392847] i915 0000:45:00.0: [drm] GT0: GUC: submission enabled
[    6.392851] i915 0000:45:00.0: [drm] GT0: GUC: SLPC enabled
[    6.393192] i915 0000:45:00.0: [drm] GT0: GUC: RC enabled
[    6.414245] i915 0000:45:00.0: GT0: local0 bcs'0.0 clear bandwidth:120015 MB/s
[    6.414891] [drm] Initialized i915 1.6.0 20201103 for 0000:45:00.0 on minor 1
[    6.476978] i915 0000:45:00.0: SPI access overridden by jumper
[    6.480684] mei_gsc i915.mei-gsc.17664: unexpected reset: fw_pm_event = 0x0
[    6.481135] mei_gsc i915.mei-gscfi.17664: unexpected reset: fw_pm_event = 0x0
[    6.483029] Creating 4 MTD partitions on "i915.spi.17664":
[    6.483032] 0x000000000000-0x000000001000 : "i915.spi.17664.DESCRIPTOR"
[    6.485716] 0x000000001000-0x0000005f0000 : "i915.spi.17664.GSC"
[    6.487152] 0x0000005f0000-0x0000007f0000 : "i915.spi.17664.OptionROM"
[    6.488578] 0x0000007f0000-0x000000800000 : "i915.spi.17664.DAM"
[    6.502987] snd_hda_intel 0000:46:00.0: bound 0000:45:00.0 (ops i915_audio_component_bind_ops [i915])
[    6.503629] i915 0000:45:00.0: [drm] Cannot find any crtc or sizes
[    6.503755] i915 0000:71:00.0: enabling device (0140 -> 0142)
[    6.503859] i915 0000:45:00.0: [drm] Cannot find any crtc or sizes
[    6.503865] i915 0000:71:00.0: BAR 0: releasing [mem 0xd1000000-0xd1ffffff 64bit]
[    6.503868] i915 0000:71:00.0: BAR 2: releasing [mem 0x203fe0000000-0x203fefffffff 64bit pref]
[    6.503901] i915 0000:71:00.0: BAR 2: no space for [mem size 0x400000000 64bit pref]
[    6.503902] i915 0000:71:00.0: BAR 2: failed to assign [mem size 0x400000000 64bit pref]
[    6.503904] i915 0000:71:00.0: BAR 0: assigned [mem 0xd1000000-0xd1ffffff 64bit]
[    6.503951] i915 0000:71:00.0: [drm] Failed to resize BAR2 to 16384M (-ENOSPC)
[    6.503954] i915 0000:71:00.0: BAR 2: assigned [mem 0x203fe0000000-0x203fefffffff 64bit pref]
[    6.503998] i915 0000:71:00.0: [drm] GT count: 1, enabled: 1
[    6.504908] i915 0000:71:00.0: [drm] Using Transparent Hugepages
[    6.505110] i915 0000:71:00.0: [drm] Cannot use the full memory 0x00000003fa000000 on the device as LMEM BAR size was found to be smaller
[    6.505112] i915 0000:71:00.0: [drm] Continuing with reduced LMEM size: 0x0000000010000000
[    6.505127] i915 0000:71:00.0: [drm] Local memory IO size: 0x0000000010000000
[    6.505128] i915 0000:71:00.0: [drm] Local memory available: 0x0000000010000000
[    6.561717] i915 0000:71:00.0: [drm] Finished loading DMC firmware i915/dg2_dmc_ver2_07.bin (v2.7)
[    6.569375] i915 0000:71:00.0: [drm] GT0: GuC firmware i915/dg2_guc_70.9.1.bin version 70.9.1
[    6.569379] i915 0000:71:00.0: [drm] GT0: HuC firmware i915/dg2_huc_7.10.3_gsc.bin version 7.10.3
[    6.580167] i915 0000:71:00.0: [drm] GT0: GUC: submission enabled
[    6.580170] i915 0000:71:00.0: [drm] GT0: GUC: SLPC enabled
[    6.580503] i915 0000:71:00.0: [drm] GT0: GUC: RC enabled
[    6.601794] i915 0000:71:00.0: GT0: local0 bcs'0.0 clear bandwidth:127978 MB/s
[    6.602568] [drm] Initialized i915 1.6.0 20201103 for 0000:71:00.0 on minor 2
[    6.602764] i915 0000:71:00.0: SPI access overridden by jumper
[    6.605971] Creating 4 MTD partitions on "i915.spi.28928":
[    6.605973] 0x000000000000-0x000000001000 : "i915.spi.28928.DESCRIPTOR"
[    6.607430] 0x000000001000-0x0000005f0000 : "i915.spi.28928.GSC"
[    6.608582] 0x0000005f0000-0x0000007f0000 : "i915.spi.28928.OptionROM"
[    6.610778] 0x0000007f0000-0x000000800000 : "i915.spi.28928.DAM"
[    6.612708] mei_gsc i915.mei-gsc.28928: unexpected reset: fw_pm_event = 0x0
[    6.613253] mei_gsc i915.mei-gscfi.28928: unexpected reset: fw_pm_event = 0x0
[    6.615236] snd_hda_intel 0000:72:00.0: bound 0000:71:00.0 (ops i915_audio_component_bind_ops [i915])
[    6.615929] i915 0000:71:00.0: [drm] Cannot find any crtc or sizes
[    6.616126] i915 0000:71:00.0: [drm] Cannot find any crtc or sizes
[    6.616204] i915 0000:71:00.0: [drm] Cannot find any crtc or sizes
[    6.995352] i915 0000:45:00.0: [drm] GT0: HuC: authenticated!
[    6.995360] mei_pxp i915.mei-gsc.17664-fbf6fcf1-96cf-4e2e-a6a6-1bab8cbe36b1: bound 0000:45:00.0 (ops i915_pxp_tee_component_ops [i915])
[    7.124477] i915 0000:71:00.0: [drm] GT0: HuC: authenticated!
[    7.124488] mei_pxp i915.mei-gsc.28928-fbf6fcf1-96cf-4e2e-a6a6-1bab8cbe36b1: bound 0000:71:00.0 (ops i915_pxp_tee_component_ops [i915])
```

```
:~$ lspci -v | grep -A8 VGA
02:00.0 VGA compatible controller: ASPEED Technology, Inc. ASPEED Graphics Family (rev 52) (prog-if 00 [VGA controller])
        DeviceName: Onboard VGA
        Subsystem: ASPEED Technology, Inc. ASPEED Graphics Family
        Flags: medium devsel, IRQ 16, NUMA node 0
        Memory at 94000000 (32-bit, non-prefetchable) [size=16M]
        Memory at 95000000 (32-bit, non-prefetchable) [size=256K]
        I/O ports at 2000 [size=128]
        Capabilities: <access denied>
        Kernel driver in use: ast
        Kernel modules: ast
--
45:00.0 VGA compatible controller: Intel Corporation Device 56a0 (rev 08) (prog-if 00 [VGA controller])
        Subsystem: Device 1ef7:1334
        Flags: bus master, fast devsel, latency 0, IRQ 150, NUMA node 0
        Memory at bc000000 (64-bit, non-prefetchable) [size=16M]
        Memory at 202fe0000000 (64-bit, prefetchable) [size=256M]
        Expansion ROM at bd000000 [disabled] [size=2M]
        Capabilities: <access denied>
        Kernel driver in use: i915
        Kernel modules: i915
--
71:00.0 VGA compatible controller: Intel Corporation Device 56a0 (rev 08) (prog-if 00 [VGA controller])
        Subsystem: Device 1ef7:1334
        Flags: bus master, fast devsel, latency 0, IRQ 153, NUMA node 0
        Memory at d1000000 (64-bit, non-prefetchable) [size=16M]
        Memory at 203fe0000000 (64-bit, prefetchable) [size=256M]
        Expansion ROM at d2000000 [disabled] [size=2M]
        Capabilities: <access denied>
        Kernel driver in use: i915
        Kernel modules: i915
```

从以上的打印出来的log发现，这个Xeon有2张A770的卡，但是显存大小是错误的，只有256M，A770显存是16GB。
```
[    6.995360] mei_pxp i915.mei-gsc.17664-fbf6fcf1-96cf-4e2e-a6a6-1bab8cbe36b1: bound 0000:45:00.0 (ops i915_pxp_tee_component_ops [i915])
[    7.124488] mei_pxp i915.mei-gsc.28928-fbf6fcf1-96cf-4e2e-a6a6-1bab8cbe36b1: bound 0000:71:00.0 (ops i915_pxp_tee_component_ops [i915])
Intel Corporation Device 56a0
 Memory at 203fe0000000 (64-bit, prefetchable) [size=256M]
```

## step2： 用户需要根据自己机器的port PCIE_ID 进行修改fix_arc_mod.sh，比如有两张Arc，需要修改4个值。
fix_arc_mod.sh 的 45   71    :6e    :42 的4个值

```
for i in 45 71
echo 1 > /sys/bus/pci/devices/0000\:6e\:01.0/remove
echo 1 > /sys/bus/pci/devices/0000\:42\:01.0/remove
```

56a0是A770的ID，“$ lspci -tvvn”看出:6e对应71，:42对应45

```
:~$ lspci -tvvn
……
 +-[0000:6e]-+-00.0  8086:09a2
 |           +-00.1  8086:09a4
 |           +-00.2  8086:09a3
 |           +-00.4  8086:0b23
 |           \-01.0-[6f-72]----00.0-[70-72]--+-01.0-[71]----00.0  8086:56a0
 |                                           \-04.0-[72]----00.0  8086:4f90
 +-[0000:42]-+-00.0  8086:09a2
 |           +-00.1  8086:09a4
 |           +-00.2  8086:09a3
 |           +-00.4  8086:0b23
 |           \-01.0-[43-46]----00.0-[44-46]--+-01.0-[45]----00.0  8086:56a0
 |                                           \-04.0-[46]----00.0  8086:4f90
```

## step 3: 运行脚本，使得显存识别成正确的16GB
```
:~$ sudo ./fix_arc_mod.sh
Current PF Bar size: 08
PF Bar size set to 16GB: 0e
Sguint_port: 0000:45:00.0
Current PF Bar size: 08
PF Bar size set to 16GB: 0e
Sguint_port: 0000:71:00.0
Remove ARC
Rescan

:~$ lspci -v | grep -A8 VGA
02:00.0 VGA compatible controller: ASPEED Technology, Inc. ASPEED Graphics Family (rev 52) (prog-if 00 [VGA controller])
        DeviceName: Onboard VGA
        Subsystem: ASPEED Technology, Inc. ASPEED Graphics Family
        Flags: medium devsel, IRQ 16, NUMA node 0
        Memory at 94000000 (32-bit, non-prefetchable) [size=16M]
        Memory at 95000000 (32-bit, non-prefetchable) [size=256K]
        I/O ports at 2000 [size=128]
        Capabilities: <access denied>
        Kernel driver in use: ast
        Kernel modules: ast
--
45:00.0 VGA compatible controller: Intel Corporation Device 56a0 (rev 08) (prog-if 00 [VGA controller])
        Subsystem: Device 1ef7:1334
        Flags: bus master, fast devsel, latency 0, IRQ 39, NUMA node 0
        Memory at aa000000 (64-bit, non-prefetchable) [size=16M]
        Memory at 202000000000 (64-bit, prefetchable) [size=16G]
        Expansion ROM at ab000000 [disabled] [size=2M]
        Capabilities: <access denied>
        Kernel driver in use: i915
        Kernel modules: i915
--
71:00.0 VGA compatible controller: Intel Corporation Device 56a0 (rev 08) (prog-if 00 [VGA controller])
        Subsystem: Device 1ef7:1334
        Flags: bus master, fast devsel, latency 0, IRQ 154, NUMA node 0
        Memory at bf000000 (64-bit, non-prefetchable) [size=16M]
        Memory at 203000000000 (64-bit, prefetchable) [size=16G]
        Expansion ROM at be800000 [disabled] [size=2M]
        Capabilities: <access denied>
        Kernel driver in use: i915
        Kernel modules: i915

:~$ uname -a
Linux adc-a770-0 5.19.0-50-generic #50-Ubuntu SMP PREEMPT_DYNAMIC Mon Jul 10 18:24:29 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux
```
