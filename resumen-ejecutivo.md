# Resumen Ejecutivo — Ban100

> Este archivo debe ser una copia del resumen ejecutivo del **Taller 9 (Presentación Final)**. Como el equipo aún no ha llegado a ese taller, por ahora este es un adelanto basado en la Visión de Arquitectura (Taller 0), para que el área de negocio tenga algo que leer mientras se completa el proyecto.

## ¿Cuál es el problema?

Ban100 (antes Credifinanciera), banco enfocado en inclusión financiera con más de 250.000 clientes en 900+ municipios, enfrenta cuatro problemas centrales: demoras de días en el desembolso de créditos de libranza, información de clientes fragmentada en silos por producto, un core bancario monolítico difícil de integrar con nuevos ecosistemas de pago, y una infraestructura on-premise que exige ventanas de mantenimiento y no cumple del todo con las exigencias de ciberseguridad de la Superintendencia Financiera.

## ¿Qué se propone?

Una arquitectura empresarial objetivo, bajo el marco MRAE v3.0 de MinTIC, que desacopla el core bancario en microservicios expuestos vía API Gateway, integra biometría y firma electrónica con Truora, conecta al sistema de pagos inmediatos Bre-B del Banco de la República bajo el estándar ISO 20022, y adopta un modelo de datos maestro (MDM) junto con una arquitectura de seguridad Zero Trust.

## ¿Cómo se implementa?

En 3 horizontes de una hoja de ruta de transformación (ver `07-opportunities-solutions/` y `09-presentacion-final/` cuando estén disponibles), comenzando por el proceso de mayor impacto: la originación digital de crédito de libranza, que se busca reducir de 3-5 días a menos de 15 minutos.

## ¿Dónde profundizar?

Ver la tabla de contenidos en el [`README.md`](./README.md) de este repositorio.
