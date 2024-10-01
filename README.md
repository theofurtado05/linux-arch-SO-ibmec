Grupo: Théo Furtado Maurício e João Lucas Curvelo


# Relatório de Configuração do Arch Linux

Este README documenta os passos e as principais configurações realizadas durante a inicialização e configuração do Arch Linux em uma arquitetura ARM64 (virtualizada usando QEMU).

## 1. Inicialização do Kernel
- O sistema iniciou o **kernel Linux versão 5.18.1-1** na arquitetura ARM64.
- As tabelas hash foram inicializadas para protocolos como **MPTCP**, **UDP** e **UDP-Lite**.
- Os módulos **RPC** para comunicação remota (UDP/TCP) foram registrados.
- O subsistema **PCI** foi habilitado, e vários dispositivos PCI foram inicializados com sucesso.

## 2. Configuração do Sistema de Arquivos
- O sistema tentou desempacotar a imagem **rootfs** como **initramfs**.
- Os drivers **NFSv4** foram registrados para o gerenciamento de layout de arquivos, incluindo suporte ao **NFS Flexfile Layout**.
- O driver **NTFS3** foi inicializado no modo somente leitura, com suporte para compressão **LZX/Xpress**.
- O sistema de arquivos **XFS** com ACLs, atributos de segurança e gerenciamento de cotas foi carregado.

## 3. Registro de Subsistemas de Hardware
- Drivers de hardware importantes, como dispositivos **USB**, **SCSI** e **HID** foram registrados.
- Diversos controladores de host USB (**EHCI**, **OHCI**, **xHCI**) foram configurados, e dispositivos conectados às portas USB foram detectados e inicializados.
- O **dispositivo de bloco** `/dev/vda` (provavelmente um disco virtual) foi detectado com partições.

## 4. Inicialização de Recursos Críticos
- Módulos importantes como **zbud** (compressão de memória) e suporte ao sistema de arquivos **XFS** foram ativados.
- Protocolos de rede como **IPv6**, **Mobile IPv6** e **Segment Routing** foram inicializados.

## 5. Inicialização do `systemd`
- O **systemd 251.4-1** foi iniciado no modo de sistema, detectando virtualização via QEMU.
- O `systemd` configurou várias **slices** para diferentes serviços, como `getty`, `modprobe` e gerenciadores de usuários/sessões.

## 6. Montagem e Verificação do Sistema de Arquivos
- O sistema executou o comando **fsck** (file system check) no disco `/dev/vda2` para garantir a integridade dos dados.
- O sistema de arquivos **EXT4** foi montado com sucesso, e o diretório `/boot` também foi montado corretamente.

## 7. Carregamento de Módulos e Serviços do Kernel
- Módulos essenciais do kernel, como **fuse** (Filesystem in Userspace), **drm** (Direct Rendering Manager) e **configfs** foram carregados.
- A configuração de rede foi gerada com base nos parâmetros fornecidos ao kernel.
- O sistema começou a configurar os arquivos de dispositivos estáticos e ativou serviços de gerenciamento de dispositivos usando o **udev**.

## 8. Configuração de Dispositivos USB e Rede
- Dispositivos USB como teclado e mouse virtuais (**QEMU USB**) foram detectados e configurados.
- A interface de rede `enp0s1` foi renomeada e configurada com sucesso, estabelecendo a conexão.

## 9. Ativação de Serviços Essenciais
- Serviços como o daemon **OpenSSH** foram ativados, permitindo login remoto.
- O serviço de resolução de nomes de rede (**DNS**) foi iniciado, juntamente com a sincronização de tempo via **NTP**.

## 10. Finalização e Login
- O sistema alcançou o alvo da **interface gráfica** (`Graphical Interface`), concluindo a inicialização do ambiente de usuário.
- O login foi efetuado com sucesso na sessão root utilizando o terminal `ttyAMA0`.
- A configuração inicial foi concluída, e o sistema estava pronto para uso.
