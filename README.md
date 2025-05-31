# Introducción
Los servicios DNS son esenciales para el funcionamiento eficiente y seguro de las redes, por esta razón, muchas empresas desarrollan sus propios DNS. En este proyecto usamos los conceptos fundamentales de DNS mediante la instalación, configuración y validación de un servidor BIND en un entorno virtualizado

Para su implementación, se eligió el uso de Amazon Web Services (AWS) con una instancia EC2 ejecutando Ubuntu Server, lo que permitió desarrollar habilidades prácticas en una infraestructura real basada en la nube

# Objetivo
Diseñar, implementar y probar un entorno funcional que incluya un servidor DNS BIND configurado con archivos de zona directa e inversa, validando la correcta resolución de nombres. Esto se logró utilizando una instancia EC2 en AWS, replicando un escenario real de infraestructura de red

### Logrados
- Instalar el servicio BIND y herramientas asociadas
- Modificar el archivo de configuración principal del servicio para incluir la información
del dominio simulado (por ejemplo, grupoX.local)
- Crear los archivos de zona directa e inversa con registros adecuados (A, PTR, SOA,
NS)
- Establecer permisos adecuados a los archivos de configuración
- Activar y habilitar el servicio para que inicie automáticamente
- Validar la configuración utilizando herramientas como dig o nslookup
- Investigar cómo configurar el servicio BIND en modo chroot o "modo jaula" y explicar
sus ventajas
- La configuración de red y del servidor DNS (VirtualBox o AWS)
- El contenido de los archivos de zona directa e inversa
- Las pruebas exitosas de resolución de nombres

### No logrados
- Nos habría gustado implementar el servicio BIND en modo chroot

# Conclusiones
- El proyecto nnos permitió ver de una manera más práctica el servidor DNS y el servicio BIND9, además de concretar nuestros conocimientos
- Se logró desplegar un servidor DNS funcional en la nube, superando retos de configuración y validación
- Aunque no se utilizó el modo chroot, se aprendió sobre su funcionalidad y ventajas como mejora de seguridad

# Instancia EC2 AWS
### Nombre, subred y direcciones, pública y privada

![image](https://github.com/user-attachments/assets/9e299907-17ef-4189-ab6c-546c1615ef3b)

### Subred publica de la VPC conectada a Internet GateWay.

![image](https://github.com/user-attachments/assets/8eb72652-c746-4aaf-82fb-fa9c46c9c083)

### Grupo de seguridad de la red con puertos habilitados

![image](https://github.com/user-attachments/assets/9686689f-2f98-4fe8-92a1-923391f6e9b9)

### Firewall

![image](https://github.com/user-attachments/assets/a25aa861-8cc4-4d9c-ba7b-0fa1baa61114)

# Servidor-DNS

### Configuración del archivo Options
![Imagen de WhatsApp 2025-05-30 a las 20 47 54_31e27a62](https://github.com/user-attachments/assets/d867b938-52d5-44b6-9500-c7c0eba66ea2)

### Configuración del archivo Local (Zonas directa e inversa)
![Imagen de WhatsApp 2025-05-30 a las 20 48 41_cdf53791](https://github.com/user-attachments/assets/2b0e59e1-e23e-4f1b-a980-814b6a5191f7)

### Chequeo de nombres y archivos
![Imagen de WhatsApp 2025-05-30 a las 20 49 46_6fcc1aad](https://github.com/user-attachments/assets/3c9fd6c4-fe64-4ee6-ad1c-2eae1908a17b)



### Dig Zona Directa
![Imagen de WhatsApp 2025-05-30 a las 20 47 07_3828161a](https://github.com/user-attachments/assets/2506f130-b125-4635-b8d3-509565bd15ed)

### Dig Zona Inversa
![Imagen de WhatsApp 2025-05-30 a las 20 46 49_c738541a](https://github.com/user-attachments/assets/a4682f4c-2e18-4413-9f5a-c8021f701501)


# ¿Qué es el modo chroot?

Configurar el servicio BIND en modo chroot es una práctica común de seguridad en servidores DNS. 
### ¿Qué significa? 
Restringe el entorno en el que se ejecuta BIND a un directorio específico del sistema de archivos, de este modo, el proceso no puede acceder a recursos fuera de ese entorno, únicamente puede acceder a archivos dentro de esa "jaula".
### Ventajas :)
- Mayor seguridad -> Si un atacante pone en riesgo el servicio DNS, estará limitado al entrono chroot, por lo cual no podrá acceder a todo el sistema.
- Minimización de daños -> Los archivos del sistema que se encuentran fuera de la "jaula" permanecen inaccesibles para el servicio DNS.
- Buena práctica -> Es una práctica recomendada para servicios de red expuestos
- Facilidad para realizar pruebas y aislamiento -> Se puede probar la configuración de DNS en un entorno aislado sin afectar el sistema en conjunto.
