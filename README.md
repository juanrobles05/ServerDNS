# ServerDNS

## Conexión SSH a Instancia EC2 de AWS

Este documento describe cómo conectarse a una instancia EC2 en AWS utilizando una llave privada `.pem`.

## Requisitos

- Tener la **llave privada `ServerDns.pem`** que descargaste al crear la instancia EC2.
- Conocer la **IP pública** de tu instancia EC2.
- Tener instalado el cliente **SSH** (en Linux/macOS viene por defecto; en Windows puedes usar PowerShell o WSL).

---

## Comando
``` bash
ssh -i ServerDns ubuntu@3.149.27.132
´´´