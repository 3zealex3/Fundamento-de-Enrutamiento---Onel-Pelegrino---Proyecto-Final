Esquema de README - Proyecto de Configuración de Red
Descripción del Proyecto
Documentación técnica de la configuración de una red empresarial completa que incluye VLANs, enrutamiento, HSRP, DHCP, agregación de enlaces, redes inalámbricas y conectividad total.

Tabla de Contenidos
Topología de Red

Requisitos y Tareas

Configuraciones por Equipo

Diagrama de Direccionamiento IP

Procedimientos de Configuración

Verificación y Pruebas

Archivos de Configuración

Topología de Red
text
[Diagrama de la topología de red con equipos y conexiones]
- Routers: R1, R2, R3, R4
- Switches: SW1, SW2, SW3, SW4
- Access Points: AP-BIBLIOTECA, AP-LOBBY
- PCs: Múltiples segmentos
Requisitos y Tareas
✅ Tarea 1: Configuración de Acceso SSH
Usuario: matricula | Contraseña: Fe2024

Usuario: opelegrino | Contraseña cifrada: Fe2024

✅ Tarea 2: Configuración de VLANs
VLAN	Nombre	Red	Descripción
300	Vlan300	172.16.300.0/24	Red de departamento
500	Vlan500	172.16.500.0/24	Red de servidores
999	Vlan999	172.16.999.0/24	Red de gestión
✅ Tarea 3: Enrutamiento entre VLANs
Configurar router-on-a-stick o SVI según corresponda

Interfaces troncales entre switches

✅ Tarea 4: Configuración HSRP
R4: Router Activo para VLANs 300, 500, 999

R1: Router en espera

Gateway virtual: Primera dirección utilizable

R1 dirección: Segunda dirección utilizable

R4 dirección: Tercera dirección utilizable

✅ Tarea 5: Puente Raíz (Root Bridge)
SW1: Root Bridge para VLANs 300, 500, 999

Prioridad ajustada: 4096

✅ Tarea 6: Direccionamiento IP
Configurar direcciones según tabla proporcionada

Incluir switches con direcciones de gestión

✅ Tarea 7: Servidor DHCP en R2
Configurar pools DHCP para todas las redes

Excluir direcciones de gateway y dispositivos fijos

✅ Tarea 8: Agregación de Enlaces (LACP)
Configurar EtherChannel entre switches

Protocolo: LACP

Modo: active/active

✅ Tarea 9: Enrutamiento Estático
Configurar rutas estáticas para conectividad total

Rutas por defecto donde corresponda

✅ Tarea 10: Redes Inalámbricas
AP	Perfiles SSID
AP-BIBLIOTECA	Duarte, Sánchez
AP-LOBBY	Mella, Duarte
✅ Tarea 11: Seguridad Wireless
Protocolo: WPA2-Personal

Contraseña: Cisco123

Usuario Admin configurado

✅ Tarea 12: Verificación de Conectividad
Ping entre todos los dispositivos

Verificación de conectividad switch a switch

✅ Tarea 13: Guardar Configuraciones
copy running-config startup-config en todos los dispositivos

Configuraciones por Equipo
Routers
R1
cisco
! Configuración SSH, VLANs, HSRP, Enrutamiento
R2
cisco
! Configuración DHCP, Enrutamiento
R3
cisco
! Configuración Enrutamiento
R4
cisco
! Configuración HSRP activo, Enrutamiento
Switches
SW1 (Root Bridge)
cisco
! Configuración VLANs, STP, LACP, Direccionamiento
SW2, SW3, SW4
cisco
! Configuración VLANs, LACP, Trunking
Access Points
AP-BIBLIOTECA
cisco
! SSID: Duarte, Sánchez | Seguridad WPA2
AP-LOBBY
cisco
! SSID: Mella, Duarte | Seguridad WPA2
Diagrama de Direccionamiento IP
VLAN 300
Red: 172.16.300.0/24

Gateway virtual: 172.16.300.1

R1: 172.16.300.2

R4: 172.16.300.3

Rango DHCP: 172.16.300.10-254

VLAN 500
Red: 172.16.500.0/24

Gateway virtual: 172.16.500.1

R1: 172.16.500.2

R4: 172.16.500.3

Rango DHCP: 172.16.500.10-254

VLAN 999
Red: 172.16.999.0/24

Gateway virtual: 172.16.999.1

R1: 172.16.999.2

R4: 172.16.999.3

Switches: 172.16.999.10-20

Procedimientos de Configuración
1. Configuración Inicial
bash
enable
configure terminal
hostname [NOMBRE_DISPOSITIVO]
2. Configuración SSH
cisco
enable secret Fe2024
username matricula password Fe2024
username opelegrino secret Fe2024
ip domain-name ejemplo.com
crypto key generate rsa modulus 2048
line vty 0 15
 transport input ssh
 login local
3. Configuración de VLANs
cisco
vlan 300
 name Vlan300
vlan 500
 name Vlan500
vlan 999
 name Vlan999
4. Configuración HSRP
cisco
interface Vlan300
 ip address 172.16.300.3 255.255.255.0
 standby 1 ip 172.16.300.1
 standby 1 priority 150
 standby 1 preempt
5. Configuración DHCP en R2
cisco
ip dhcp pool Vlan300
 network 172.16.300.0 255.255.255.0
 default-router 172.16.300.1
 dns-server 8.8.8.8
Verificación y Pruebas
Comandos de Verificación
bash
# Verificar VLANs
show vlan brief

# Verificar HSRP
show standby brief

# Verificar DHCP
show ip dhcp binding

# Verificar EtherChannel
show etherchannel summary

# Verificar conectividad
ping [IP_DESTINO]

# Verificar rutas
show ip route

# Verificar STP
show spanning-tree vlan 300,500,999
Pruebas de Conectividad
PC VLAN300 → PC VLAN500 ✓

PC VLAN300 → Internet ✓

Switch → Router ✓

Wireless → Red cableada ✓

