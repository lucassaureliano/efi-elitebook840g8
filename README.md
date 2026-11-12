# EFI OpenCore – HP EliteBook 840 G8

EFI do OpenCore para rodar macOS no HP EliteBook 840 G8 (Tiger Lake).

**Estado:** em uso no dia a dia. A maior parte do hardware funciona. Ainda há limitações em microfone interno, Thunderbolt e leitor de digital.

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

## Aceleração gráfica: instale o WhateverXe Graphics

A kext WhateverXe sozinha não basta. Depois do primeiro boot, instale o pacote [WhateverXe Graphics](https://github.com/b00t0x/WhateverXe-Graphics/releases) na **mesma versão** indicada acima e reinicie. Ao atualizar, troque a kext e o pacote juntos.

## O que funciona

Itens verificados com o sistema rodando:

- **Aceleração gráfica (Iris Xe):** funciona com Metal 2, usando WhateverXe e AppleIntelTGLCompat. A GPU aparece com 1536 MB de VRAM dinâmica.
- **Tela:** funciona em 1920x1080.
- **Brilho da tela e teclas de brilho:** funcionam com BrightnessKeys e SSDT-PNLF.
- **Wi-Fi:** funciona com ForbiddenItlwm (itlwm 2.4.1). Conecta em 2,4 GHz e 5 GHz, até 802.11ac. Inclui AirDrop. Os boot-args `-itlawdl*` habilitam o AWDL.
- **Bluetooth:** funciona com IntelBluetoothFirmware, BlueToolFixup, IntelBTPatcher e BTLEAdvFixup.
- **Teclado:** funciona com VoodooPS2.
- **Trackpad:** funciona com VoodooI2C e VoodooI2CHID, incluindo os gestos de múltiplos dedos.
- **Webcam (HP HD Camera):** é reconhecida via USB.
- **Áudio pelos alto-falantes e pela saída de fone:** funciona com SimpleHDA, AppleALC e `layout-id` 88.
- **Áudio USB:** funciona.
- **Bateria:** mostra porcentagem, ciclos e status de carregamento (SMCBatteryManager e ECEnabler).
- **Sensores de CPU:** funcionam com SMCProcessor e SMCSuperIO.
- **Portas USB:** mapeadas com USBToolBox e UTBMap.
- **SSD NVMe:** funciona com NVMeFix.
- **Suspensão (sleep):** funciona com S0ixStandby e SSDT-DEEPIDLE (S0ix / Modern Standby). Entra em suspensão por inatividade ou ao fechar a tampa, e acorda pelo botão de energia, pelo teclado ou ao abrir a tampa.

## O que não funciona ou tem limitações

- **Microfone interno:** não aparece no sistema. É um microfone digital (DMIC), o que geralmente não tem suporte em hackintosh. Use um microfone USB ou Bluetooth.
- **Thunderbolt 4:** o sistema não reconhece um controlador Thunderbolt. As portas USB-C funcionam só como USB.
- **Leitor de impressões digitais:** não funciona, e não há suporte possível no macOS.
- **Saída HDMI e saídas de vídeo por USB-C:** não testadas.

## Observações sobre a configuração

- **SIP:** está parcialmente desativado (`csr-active-config` = `03 0A 00 00`). Isso é necessário para AMFIPass e para os patches de GPU.
- **SecureBootModel:** `Disabled`.
- **Boot-args:** `-disablegfxfirmware -igfxdvmt -allow3d` são usados para a Iris Xe, e `-s0ixd3 -s0ixacnortc` pelo S0ixStandby.
- **Suspensão:** usada com `hibernatemode 0` e `standby 0` no `pmset`.
- **NVRAM:** o RestrictEvents mostra o nome real da CPU, configurado com `revpatch=sbvmm,cpuname`.
