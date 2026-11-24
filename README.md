# EFI OpenCore – HP EliteBook 840 G8

EFI do OpenCore para rodar macOS no HP EliteBook 840 G8 (Tiger Lake).

## Hardware

- **Notebook:** HP EliteBook 840 G8
- **CPU:** Intel Core i5-1145G7 (11ª geração, Tiger Lake)
- **GPU:** Intel Iris Xe (integrada)
- **Wi-Fi e Bluetooth:** Intel AX201 (ID 8086:0070)
- **Trackpad:** Synaptics I2C-HID (06CB:CE08)
- **Áudio:** Realtek HDA

## Software

- **macOS:** 26.7.3 (25G342)
- **OpenCore:** 1.0.9
- **SMBIOS:** `MacBookPro16,2`

## O que funciona

- **Aceleração gráfica (Iris Xe):** Metal 2, com WhateverXe. Exige o pacote [WhateverXe Graphics](https://github.com/b00t0x/WhateverXe-Graphics/releases) instalado no sistema, na versão correspondente à kext (veja a lista de kexts).
- **Tela:** 1920x1080.
- **Brilho da tela e teclas de brilho:** BrightnessKeys e SSDT-PNLF.
- **Wi-Fi:** ForbiddenItlwm, com Wi-Fi 6 (802.11ax) em 2,4 GHz e 5 GHz, e AirDrop.
- **Bluetooth:** IntelBluetoothFirmware, BlueToolFixup e BTLEAdvFixup.
- **Teclado:** VoodooPS2.
- **Trackpad:** VoodooI2C e VoodooI2CHID, com gestos de múltiplos dedos.
- **Webcam (HP HD Camera):** reconhecida via USB.
- **Alto-falantes e fone P2:** SimpleHDA e AppleALC com `layout-id` 71. A saída troca sozinha entre alto-falantes e fone ao conectar o P2.
- **Microfone interno:** TGLDmic (microfone digital DMIC do Tiger Lake).
- **Áudio USB:** funciona, por exemplo com EarPods USB-C.
- **Bateria:** porcentagem, ciclos e status de carregamento (SMCBatteryManager e ECEnabler).
- **Sensores de CPU:** SMCProcessor.
- **Portas USB:** mapeadas com USBToolBox e UTBMap.
- **SSD NVMe:** NVMeFix.
- **Suspensão (sleep):** S0ixStandby e SSDT-DEEPIDLE (Deep Idle / S0ix). Entra em suspensão por inatividade, pelo menu ou ao fechar a tampa, e acorda pelo botão de energia.

## O que não funciona ou tem limitações

- **Acordar pelo teclado ou ao abrir a tampa:** não funciona. Só o botão de energia acorda o notebook. É uma limitação conhecida do S0ixStandby no 840 G8 ([detalhes](https://github.com/labrouss/S0ixStandby#readme)).
- **Entrada "Microfone Integrado" extra:** o `layout-id` 71 cria uma entrada de microfone que não capta nada nesta máquina. O microfone interno real é o "Internal Microphone (TGLDmic)".
- **Thunderbolt 4:** o sistema não reconhece um controlador Thunderbolt. As portas USB-C funcionam só como USB.
- **Leitor de impressões digitais:** não funciona, e não há suporte possível no macOS.
- **Saída HDMI e saídas de vídeo por USB-C:** não testadas.

## Kexts

| Kext | Versão | Repositório |
|---|---|---|
| Lilu | 1.7.3 | [acidanthera/Lilu](https://github.com/acidanthera/Lilu) |
| VirtualSMC | 1.3.9 | [acidanthera/VirtualSMC](https://github.com/acidanthera/VirtualSMC) |
| SMCProcessor | 1.3.9 | [acidanthera/VirtualSMC](https://github.com/acidanthera/VirtualSMC) |
| SMCBatteryManager | 1.3.9 | [acidanthera/VirtualSMC](https://github.com/acidanthera/VirtualSMC) |
| SMCLightSensor | 1.3.9 | [acidanthera/VirtualSMC](https://github.com/acidanthera/VirtualSMC) |
| ECEnabler | 1.0.6 | [1Revenger1/ECEnabler](https://github.com/1Revenger1/ECEnabler) |
| RestrictEvents | 1.1.7 | [acidanthera/RestrictEvents](https://github.com/acidanthera/RestrictEvents) |
| AMFIPass | 1.4.1 | [dortania/OpenCore-Legacy-Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher/tree/main/payloads/Kexts/Acidanthera) |
| WhateverXe | 0.8.5 | [b00t0x/WhateverXe](https://github.com/b00t0x/WhateverXe) |
| WhateverXe Graphics (pacote, não é kext) | 0.4.5 | [b00t0x/WhateverXe-Graphics](https://github.com/b00t0x/WhateverXe-Graphics) |
| AppleALC | 1.9.9 | [acidanthera/AppleALC](https://github.com/acidanthera/AppleALC) |
| SimpleHDA | 1.0.2 | [laobamac/SimpleHDA](https://github.com/laobamac/SimpleHDA) |
| TGLDmic | 0.5.0 | [labrouss/TGLDmic](https://github.com/labrouss/TGLDmic) |
| ForbiddenItlwm | 0.6.0-beta.4 | [retropineaple/ForbiddenItlwm](https://github.com/retropineaple/ForbiddenItlwm) |
| BTLEAdvFixup | 0.9.4 | [retropineaple/ForbiddenItlwm](https://github.com/retropineaple/ForbiddenItlwm) |
| IntelBluetoothFirmware | 2.5.0 | [OpenIntelWireless/IntelBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) |
| BlueToolFixup | 2.7.3 | [acidanthera/BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM) |
| VoodooPS2Controller | 2.3.8 | [acidanthera/VoodooPS2](https://github.com/acidanthera/VoodooPS2) |
| VoodooPS2Keyboard | 2.3.8 | [acidanthera/VoodooPS2](https://github.com/acidanthera/VoodooPS2) |
| VoodooI2C | 2.9.1 | [VoodooI2C/VoodooI2C](https://github.com/VoodooI2C/VoodooI2C) |
| VoodooI2CHID | 1.0 | [VoodooI2C/VoodooI2C](https://github.com/VoodooI2C/VoodooI2C) |
| VoodooGPIO | 1.1 | [VoodooI2C/VoodooI2C](https://github.com/VoodooI2C/VoodooI2C) |
| VoodooI2CServices | 1.0 | [VoodooI2C/VoodooI2C](https://github.com/VoodooI2C/VoodooI2C) |
| VoodooInput | 1.1.7 | [acidanthera/VoodooInput](https://github.com/acidanthera/VoodooInput) |
| BrightnessKeys | 1.0.4 | [acidanthera/BrightnessKeys](https://github.com/acidanthera/BrightnessKeys) |
| USBToolBox | 1.2.0 | [USBToolBox/kext](https://github.com/USBToolBox/kext) |
| UTBMap | 1.1 | gerado para esta máquina com o [USBToolBox/tool](https://github.com/USBToolBox/tool) |
| XHCI-unsupported | 0.9.2 | [RehabMan/OS-X-USB-Inject-All](https://github.com/RehabMan/OS-X-USB-Inject-All) |
| NVMeFix | 1.1.4 | [acidanthera/NVMeFix](https://github.com/acidanthera/NVMeFix) |
| S0ixStandby | 0.5.8 | [labrouss/S0ixStandby](https://github.com/labrouss/S0ixStandby) |
