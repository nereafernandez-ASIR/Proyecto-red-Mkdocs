# Conclusiones

Después de completar este proyecto, entender el como usar redes y configurarlas, se hizo mucho más fácil. Aquí resumo lo que he conseguido y qué podría mejorar en el futuro.

---

## Resumen del Proyecto

He diseñado y configurado una **red empresarial completa** en Cisco Packet Tracer con:

-  **Segmentación en 4 VLANs** (Ordenadores, Impresoras, AP, Router)
-  **19 dispositivos** funcionando: 11 PCs, 3 impresoras, 3 portátiles, 1 AP, 1 router, 1 switch
-  **Enrutamiento Inter-VLAN** con switch de capa 3
-  **Seguridad mediante ACLs** para proteger recursos internos
-  **Red WiFi segura** con WPA2-PSK
-  **Monitorización SNMP** del router
-  **Spanning Tree Protocol** para evitar bucles
-  **Port-security** en los puertos críticos

---

## ¿Qué se ha aprendido?

### Sobre las VLANs

Entender su uso y su importancia. Pensaba que era más fácil tener todo en la misma red. Pero ahora veo que:

- Las VLANs **organizan mejor la red** - Es mucho más fácil gestionar 4 redes pequeñas que una grande
- **Mejoran la seguridad** - Puedes controlar quién accede a qué
- **Mejoran el rendimiento** - Menos tráfico de broadcast innecesario

!!! quote "Mi experiencia"
    A la hora de crear las Vlans, el trabajo de configurar todas las ACL, y procedimientos, se me hizo mas ágil y fácil.

### Sobre el Enrutamiento Inter-VLAN

Configurar el switch de capa 3 para que las VLANs pudieran comunicarse fue complicado al principio. Los puntos clave que aprendí:

1. **Hay que activar `ip routing`** - Sin esto el switch no enruta nada
2. **Las interfaces SVI son los gateways** - Cada VLAN necesita su gateway (.1 en mi caso)
3. **Los dispositivos deben saber su gateway** - Si no se configuran bien, no funciona

### Sobre las ACLs

A la hora de crear las "Listas de Control de Acceso" (ACLs), hay que tener muchos pasos en cuenta:

- **Problemas que tuve:**
  - Me olvidé de poner `permit ip any any` → Todo se bloqueaba
  - Puse la ACL en dirección "out" en vez de "in" → No funcionaba

- **Lo que aprendí:**
  - Las ACLs se leen de arriba hacia abajo
  - El orden de las reglas importa mucho
  - Hay que aplicarlas en la interfaz correcta y dirección correcta

!!! warning "Error común"
    Si te olvidas de poner `access-list 100 permit ip any any` al final, toda la comunicación que NO has bloqueado explícitamente también se bloqueará. Esto me pasó y tardé un rato en darme cuenta.

### Sobre SNMP

SNMP fue interesante porque permite ver información del router desde otro dispositivo. En una red real esto sería muy útil para:

- Saber si los dispositivos están encendidos
- Ver cuánto tiempo llevan funcionando
- Detectar problemas antes de que fallen

### Sobre Packet Tracer

Trabajar con Packet Tracer me ha gustado, pero también he visto sus limitaciones:

**Bueno:** 

- Es muy visual y fácil de entender
- Te deja practicar los comandos CLI de Cisco

**Malo:** 

- A veces se bugea y hay que reiniciar
- No tiene todas las funciones de un router/switch real

---

## Ventajas de Este Diseño

Que ventajas tiene esta red:

###  Seguridad

- Las ACLs protegen los recursos internos (PCs e impresoras) del WiFi
- Port-security evita que conecten dispositivos no autorizados
- WiFi con WPA2-PSK (no está abierto)
- Cada departamento en su propia VLAN

###  Rendimiento

- Las VLANs reducen el tráfico de broadcast
- El switch de capa 3 enruta más rápido que un router
- STP evita bucles que saturarían la red

###  Gestión

- Todo centralizado en un switch de capa 3
- Fácil de expandir (solo añades más puertos/VLANs)
- SNMP permite monitorización remota
- Los comandos show permiten ver el estado en tiempo real

###  Escalabilidad

Si la empresa crece, puedo:

- Añadir más PCs/impresoras sin cambiar nada
- Crear nuevas VLANs fácilmente
- Conectar más switches si hace falta
- Ampliar el direccionamiento IP

---

## Posibles Mejoras Futuras

Que se podría mejorar a futuro:

### 1. Añadir Switches de Capa 2

!!! tip "Mejora Principal"
    **Problema:** Ahora todos los dispositivos están conectados directamente al switch de capa 3, lo que satura sus puertos.
    
    **Solución:** Añadir switches de capa 2 en cada planta/departamento:
    
    - Un switch L2 para los PCs (VLAN 10)
    - Otro switch L2 para las impresoras (VLAN 20)
    - Conectar estos switches al switch L3 central con puertos trunk
    
    **Ventaja:** El switch L3 solo se usa para enrutamiento, no para conectar dispositivos finales.

### 2. DHCP en el Switch

Ahora todas las IPs son estáticas (las configuré a mano). Podría configurar un servidor DHCP en el switch para que asigne IPs automáticamente.

Ventajas:

- Menos trabajo manual al conectar nuevos dispositivos
- Menos errores (no hay que acordarse de qué IPs están libres)
- Gestión centralizada

### 3. Mejorar SNMP a SNMPv3

SNMPv2c que usé no es muy seguro (las passwords van sin cifrar). SNMPv3 sería mejor porque:

- Cifra los datos
- Autenticación más segura
- Control de acceso más fino

### 4. Más Servicios

Podría añadir:

- **Servidor DNS** interno
- **VLANs adicionales** (gestión, VoIP para teléfonos IP)
- **Firewall** entre el router y internet

### 5. Port-Security en Todos los Puertos

Ahora solo la configuré en algunos puertos de ejemplo. Debería ponerla en todos los puertos de acceso para máxima seguridad.

---

## Valoración Final

Este diseño permite **gestionar toda la red de manera eficiente, segura y con capacidad de crecimiento**.

Los dispositivos están divididos en segmentos usando VLANs, lo que facilita su administración y ayuda a mantener la infraestructura más segura.

Además, la configuración hecha ahora permite ampliar la red en el futuro sin tener que hacer cambios complicados en la estructura existente.

!!! success "Objetivo cumplido"
    se ha conseguido crear una red empresarial funcional, segura y bien documentada. Aunque hay cosas que mejorar (como añadir switches L2 y redundancia), el proyecto cumple su objetivo y funciona correctamente.

---

## Capturas Finales

Aquí algunas capturas de pantalla del proyecto funcionando:

![Topología completa en Packet Tracer](assets/images/topologia-completa.png)

![Prueba de ping exitosa](assets/images/ping-exitoso.png)

![SNMP funcionando](assets/images/snmp-browser.png)

---

**Gracias por leer mi documentación. Espero que le haya gustado!!!.** 

---

**Proyecto realizado por:** Nerea Fdez Fernández  
**Asignatura:** Laboratorio Integral de Redes de Datos  
**Fecha:** Junio 2025  
**Herramienta:** Cisco Packet Tracer
