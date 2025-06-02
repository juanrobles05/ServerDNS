# ServerDNS

# README - Implementación de Servidor DNS con BIND9

## Introducción
Este proyecto consistió en la implementación de un servidor DNS utilizando BIND9 en un entorno virtualizado, cumpliendo con los requisitos especificados en el proyecto final. Se configuraron zonas DNS directas e inversas, se implementaron medidas de seguridad básicas y se validó el funcionamiento correcto del servicio.

## Video demostrativo
Enlace de descarga de video de sustentación:
[Video demostrativo](./sustentación.mp4)

## Desarrollo

### 1. Configuración del Entorno
- **Sistema Operativo**: Ubuntu Server 22.04 LTS
- **Software instalado**:
    ``` bash
        sudo apt update && sudo apt install bind9 bind9-utils dnsutils

        Archivo de zona directa (/etc/bind/zones/grupo5.local.db)
        $TTL 86400
        @       IN SOA ns1.grupo5.local. admin.grupo5.local. (
                2025053001 ; Serial
                3600       ; Refresh
                1800       ; Retry
                1209600    ; Expire
                86400 )    ; Minimum TTL

        @       IN NS ns1.grupo5.local.
        @       IN A 3.149.27.132
        ns1     IN A 3.149.27.132
        web     IN A 3.149.27.132
        www     IN CNAME grupo5.local.

        Archivo de zona inversa (/etc/bind/zones/27.149.3.in-addr.arpa.db):
        $TTL 86400
        @ IN SOA ns1.grupo5.local. admin.grupo5.local. (
        2025053001 ; Serial
        3600       ; Refresh
        1800       ; Retry
        1209600    ; Expire
        86400 )    ; Minimum TTL

        @ IN NS ns1.grupo5.local.
        132 IN PTR grupo5.local.
        132 IN PTR ns1.grupo5.local.

        Se modificó /etc/bind/named.conf.local para incluir las zonas:
        zone "grupo5.local" {
            type master;
            file "/etc/bind/zones/grupo5.local.db";
        };

        zone "27.149.3.in-addr.arpa" {
            type master;
            file "/etc/bind/zones/27.149.3.in-addr.arpa.db";
        };

        Se modificó /etc/bind/named.conf.options para incluir estas opciones:
        options {
            allow-transfer { none; };
            allow-query { any; };
        };

## Conexión SSH a Instancia EC2 de AWS

Este documento describe cómo conectarse a una instancia EC2 en AWS utilizando una llave privada `.pem`.

## Requisitos

- Tener la **llave privada `ServerDns.pem`** que descargaste al crear la instancia EC2.
- Conocer la **IP pública** de tu instancia EC2.
- Tener instalado el cliente **SSH** (en Linux/macOS viene por defecto; en Windows puedes usar PowerShell o WSL).

---

## Comando
``` bash
ssh -i ServerDns.pem ubuntu@3.149.27.132
