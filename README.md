<p align="center">
  <a href="https://ag.tavardt.com/mx/">
    <img src="https://ag.tavardt.com/img/tavardt-banner.png" alt="TAVARDT" width="1024" />
  </a>
</p>

# Framework Consent Mode v2 y Conformidad Técnica LFPDPPP

[![Diagnóstico Técnico](https://img.shields.io/badge/TAVARDT-Diagn%C3%B3stico%20T%C3%A9cnico-5b3cf5.svg)](https://tools.tavardt.com/mx/validador-consent-mode-v2-lfpdppp/)
[![JavaScript](https://img.shields.io/badge/JavaScript-Node.js-yellow.svg)](https://nodejs.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

***

Implementación técnica de Google Consent Mode v2, bloqueo previo de scripts de seguimiento y conformidad regulatoria desarrollada por **TAVARDT**, en cumplimiento con la Ley Federal de Protección de Datos Personales en Posesión de los Particulares (LFPDPPP).

Para garantizar la conformidad estricta con la normativa de privacidad, inserte el script de inicialización en el `<head>` del documento antes de cargar Google Tag Manager. La ejecución temprana define el estado denegado por defecto antes de que cualquier etiqueta escriba almacenamiento local o capture identificadores.

***

## Capacidades Principales y Arquitectura Defensiva

* **Estado Denegado por Defecto (Default Denied)**: Configura de forma inmediata `ad_storage`, `ad_user_data`, `ad_personalization` y `analytics_storage` en modo denegado antes del despliegue de scripts.
* **API de Actualización Orientada a Eventos**: Proporciona la función global `window.tavardtUpdateConsent` para reflejar las decisiones de cualquier CMP en el `dataLayer`.
* **Redacción Automática de Identificadores Publicitarios**: Habilita `ads_data_redaction` para suprimir parámetros como GCLID de las peticiones cuando no exista consentimiento.
* **Atribución de Tráfico sin Cookies**: Activa `url_passthrough` para mantener la medición entre páginas sin almacenamiento persistente en el dispositivo del usuario.
* **Cero Sobrecarga de Dependencias**: Desarrollado en JavaScript puro (`consent-mode-v2.js`), ejecutándose en menos de 1 milisegundo.

***

## Vectores de Riesgo e Impacto Operacional

Implementar etiquetas de publicidad y analítica sin control técnico de consentimiento expone a las organizaciones a sanciones administrativas y fallos de medición. El paquete neutraliza cuatro riesgos operativos:

* **Activación Indebida de Etiquetas sin Consentimiento**: Píxeles publicitarios escribiendo cookies antes de la autorización del usuario, provocando infracciones legales directas.
* **Pérdida de Modelado y Atribución en Campañas**: Falta de señales de Consent Mode v2, generando interrupciones en la optimización de Google Ads y GA4.
* **Filtración de Parámetros de Clic**: Envío inadvertido de identificadores de usuario en peticiones de red sin base legítima de consentimiento.
* **Condiciones de Carrera en el Despliegue de Tags**: Etiquetas de medición ejecutándose antes de que la plataforma CMP registre las preferencias del visitante.

***

## Guía de Implementación e Integración

Inserte el script en la sección superior del `<head>` del sitio antes de cualquier contenedor de etiquetas:

```html
<script src="consent-mode-v2.js"></script>
```

### Script Execution Snippet

```javascript
// Programmatic consent update triggered by CMP callback
window.tavardtUpdateConsent({
    marketing: true,
    analytics: true,
    preferences: false
});
```

***

## Preguntas Técnicas Frecuentes

### ¿Qué parámetros concretos de consentimiento introduce Google Consent Mode v2 para cumplir con la privacidad?

Consent Mode v2 incorpora los parámetros ad_user_data y ad_personalization junto a los clásicos ad_storage y analytics_storage. Estas señales granulares determinan si los datos personales pueden transferirse a plataformas publicitarias para modelado de conversiones y remarketing.

### ¿Por qué debe registrarse el estado denegado por defecto antes de que cargue Google Tag Manager?

Definir los permisos como denegados antes de ejecutar el gestor de etiquetas asegura que ningún píxel capture identificadores en la visita inicial. Cualquier etiqueta que se dispare prematuramente sin consentimiento previo vulnera la normativa e invalida la trazabilidad de la sesión.

### ¿De qué forma protege la privacidad la directiva ads_data_redaction manteniendo la atribución?

Activar ads_data_redaction elimina los identificadores de clic como GCLID y DCLID de las solicitudes de red cuando ad_storage esté denegado. Combinado con url_passthrough, el sistema permite enviar señales anónimas entre páginas, facilitando el modelado estadístico sin persistencia en el dispositivo.

### ¿Cómo sincroniza el framework las preferencias del usuario con las etiquetas de medición?

La función window.tavardtUpdateConsent recoge las selecciones de la CMP y ejecuta el comando gtag consent update para actualizar el dataLayer. Las reglas configuradas en Google Tag Manager detectan el cambio y desbloquean en tiempo real únicamente los scripts autorizados.

### ¿Cómo pueden los equipos de ingeniería verificar que las etiquetas operan sin fugas de datos?

Los ingenieros pueden inspeccionar el tráfico de red en las herramientas de desarrollo para comprobar los parámetros gcs y gcd en las solicitudes de Google. Las pruebas automatizadas certifican que los píxeles permanecen inactivos hasta que se recibe una señal afirmativa de consentimiento.

***

## Enlaces Útiles

* **Portal Corporativo:** https://ag.tavardt.com/mx/
* **Suite de Diagnósticos:** https://tools.tavardt.com/mx/
* **Contacto Técnico:** https://ag.tavardt.com/mx/contacto/

***

### Licencia
Distribuido bajo la Licencia MIT. Consulte [LICENSE](LICENSE) para obtener detalles completos.

***

© 2026 TAVARDT. Todos los derechos reservados.
