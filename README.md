# Proyecto de Configuración de Red - Topología Completa

## 📋 Descripción
Configuración completa de una red empresarial con múltiples VLANs, enrutamiento, HSRP, DHCP, agregación de enlaces y redes inalámbricas.

## 🎯 Tareas Implementadas

### 1. Configuración SSH
- Usuario: `20242286` / Contraseña: `Fe2024`
- Usuario: `opelegrino` / Contraseña cifrada: `Fe2024`

### 2. Configuración de VLANs
| VLAN | Nombre   | Red              |
|------|----------|------------------|
| 300  | Vlan300  | 172.16.300.0/24  |
| 500  | Vlan500  | 172.16.500.0/24  |
| 999  | Vlan999  | 172.16.999.0/24  |

### 3. Enrutamiento entre VLANs
- Router-on-a-stick configurado
- Interfaces troncales establecidas

### 4. HSRP (First Hop Redundancy Protocol)
- **R4**: Router Activo para VLANs 300, 500, 999
- **R1**: Router en espera
- **Gateway virtual**: Primera IP utilizable
- **R1**: Segunda IP utilizable
- **R4**: Tercera IP utilizable

### 5. Spanning Tree Protocol
- **SW1**: Root Bridge para VLANs 300, 500, 999
- Prioridad configurada: 4096

### 6. Direccionamiento IP
- Direcciones estáticas según tabla
- Switches con IPs de gestión en VLAN 999

### 7. Servidor DHCP en R2
- Pools configurados para todas las redes
- Exclusión de direcciones fijas

### 8. Agregación de Enlaces (LACP)
- EtherChannel entre switches
- Protocolo: LACP (modo active)

### 9. Enrutamiento Estático
- Rutas configuradas para conectividad total
- Rutas por defecto donde aplica

### 10. Redes Inalámbricas
| Access Point | Perfiles SSID    |
|--------------|------------------|
| BIBLIOTECA   | Duarte, Sánchez  |
| LOBBY        | Mella, Duarte    |

### 11. Seguridad Wireless
- WPA2-Personal en todos los SSID
- Contraseña: `Cisco123`
- Usuario Admin configurado

### 12. Verificación de Conectividad
- Ping exitoso entre todos los dispositivos
- Conectividad switch-switch verificada

### 13. Guardado de Configuraciones
- Configuraciones guardadas en todos los equipos

## 🔧 Configuraciones por Equipo

### Routers
- **R1**: SSH, VLANs, HSRP (standby), enrutamiento
- **R2**: DHCP, enrutamiento, servidor central
- **R3**: Enrutamiento, conectividad inter-VLAN
- **R4**: SSH, VLANs, HSRP (active), enrutamiento

### Switches
- **SW1**: VLANs, Root Bridge, LACP, gestión
- **SW2**: VLANs, LACP, trunking
- **SW3**: VLANs, LACP, trunking
- **SW4**: VLANs, LACP, trunking

### Access Points
- **AP-BIBLIOTECA**: SSID Duarte y Sánchez
- **AP-LOBBY**: SSID Mella y Duarte

## 📊 Esquema de Direccionamiento

### VLAN 300 (Departamentos)
- Red: 172.16.300.0/24
- Gateway: 172.16.300.1
- R1: 172.16.300.2
- R4: 172.16.300.3
- DHCP: 172.16.300.10-254

### VLAN 500 (Servidores)
- Red: 172.16.500.0/24
- Gateway: 172.16.500.1
- R1: 172.16.500.2
- R4: 172.16.500.3
- DHCP: 172.16.500.10-254

### VLAN 999 (Gestión)
- Red: 172.16.999.0/24
- Gateway: 172.16.999.1
- R1: 172.16.999.2
- R4: 172.16.999.3
- Switches: 172.16.999.10-20

## ✅ Verificación

### Comandos de Verificación
```bash
# Ver estado de VLANs
show vlan brief

# Ver estado HSRP
show standby brief

# Ver bindings DHCP
show ip dhcp binding

# Ver EtherChannel
show etherchannel summary

# Ver rutas
show ip route

# Ver spanning-tree
show spanning-tree vlan 300,500,999
