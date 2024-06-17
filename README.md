# Sistema de Declaración Patrimonial y de Intereses

Sistema informático diseñado por la Secretaría Ejecutiva del Sistema Nacional Anticorrupción, con el objetivo de permitir la captura de declaraciones patrimoniales y de intereses por parte de los Servidores Públicos de acuerdo con los formatos aprobados por el Comité Coordinador del SNA.

# 🚀 Alcances y limitaciones 

El Sistema de Declaraciones es una herramienta que permite a los órganos públicos competentes para recibir declaraciones patrimoniales y de intereses poner a disposición de los declarantes cumpliendo con el [Formato aprobado por el Comité Coordinador del Sistema Nacional Anticorrupción](https://www.dof.gob.mx/nota_detalle.php?codigo=5573194&fecha=23/09/2019), resguardando la información en modelos de datos compatibles con los estándares de datos de la Plataforma Digital Nacional.

No obstante, los entes públicos que hagan uso del Sistema de Declaraciones deberán contar con la infraestructura necesaria para albergar al sistema, así como encargarse de la incorporación de las declaraciones a la Plataforma Digital Nacional, conforme a normatividad aplicable y de acuerdo con los protocolos para el Sistema 1 de la PDN, disponibles en la siguiente dirección web:

- https://www.plataformadigitalnacional.org/especificaciones/s1

## ⚠️ Precauciones 
Nunca exponga los puertos de los componentes internos del Sistema de declaraciones a Internet. Los módulos internos del Sistema de Declaraciones como elasticsearch y el módulo de reportes, pueden ser propensos a sufrir ataques informáticos si se exponen abiertamente en Internet.

Si es posible, utilice el Sistema de Declaraciones a través de una red de área local. Se decide exponer el Sistema de Declaraciones a Internet, revise que únicamente se exponen la dirección del Frontend y el Backend a través de HTTPS.

Evite exponer puertos 9200 (elasticsearch) y 3001 (reporteador) que son usados internamente por el backend del Sistema de Declaraciones.

## 📦 Descarga 
El software necesario para instalar y desplegar el Sistema de Declaraciones
se encuentra disponible a través de tres repositorios de código que
se describen en la siguiente tabla.

| Módulo   | Descripción | Recurso  |
| -------- | ----------- | -------- |
| Frontend | Interfaz Web. | [Repositorio](https://github.com/PDNMX/SistemaDeclaraciones_frontend)|
| Backend  | Lógica de negocio y conexión con bases de datos. | [Repositorio](https://github.com/PDNMX/SistemaDeclaraciones_backend)|
| Reportes | Generación de documentos PDF. | [Repositorio](https://github.com/PDNMX/SistemaDeclaraciones_reportes)|

## 📖 Manuales del Sistema 

| Manual            | Descripción | Recurso |
| ----------------- | ----------- | --------|
| Manual de usuario | Manual para usuarios del Sistema de Declaraciones (declarantes y usuarios administrativos). | [Manual](manuales/manual_usuario.pdf)|
| Manual de instalación | Manual orientado al personal encargado de la instalación y soporte técnico del Sistema de Declaraciones. | [Manual](https://docs.google.com/document/d/1HAOwKuZcrTzISx5BKaFIzJQ__-puTPbiLRmR9XACZow/edit?usp=sharing)|

## 	✉️ Dudas y comentarios 
Si tienes dudas sobre la instalación del Sistema de Declaración Patrimonial y de Intereses de la PDN comunicate con alguno de los miembros de la [Red Nacional de Capacitadores (RNC)](https://docs.google.com/spreadsheets/d/16pmdC_gxw3-4SJpqoPpQUV4U0J_X-GADMFeG554xbGU).
