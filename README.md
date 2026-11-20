# Framework Consent Mode v2 & Privacidad LFPDPPP | TAVARDT México

[![Validador de Consentimento](https://img.shields.io/badge/TAVARDT-Diagn%C3%B3stico%20T%C3%A9cnico-5b3cf5.svg)](https://tools.tavardt.com/mx/validador-consent-mode-v2-lfpdppp/)
[![Conformidade](https://img.shields.io/badge/Jurisdi%C3%A7%C3%A3o-México-00C853.svg)](https://ag.tavardt.com/mx/ciberseguridad/)

Implementación técnica de Google Consent Mode v2, gobernanza de etiquetas y cumplimiento de las medidas de seguridad bajo la LFPDPPP e INAI en México.

Desenvolvido e mantido pela divisão de privacidade digital e engenharia de dados da **[TAVARDT México](https://ag.tavardt.com/mx/)**.

---

## 1. Arquitectura y Orden de Inserción

Para garantizar la protección de datos y el consentimiento informado, este módulo debe cargarse en el <head> de la página web antes de los scripts de Google Tag Manager:

```html
<script src="consent-mode-v2.js"></script>
<!-- O contentor do Google Tag Manager ou scripts de medição seguem aqui -->
```

---

## 2. Especificaciones Técnicas

* **Estado 'Denied' por Defecto:** Suspende el almacenamiento de cookies publicitarias y de analítica antes de la confirmación del usuario.
* **Gestión de Actualización de Consentimiento:** Dispone de la función window.tavardtUpdateConsent() con emisión del evento tavardt_consent_updated.
* **Redacción de Parámetros de Publicidad:** Activa ads_data_redaction para depurar identificadores de clics ante la negativa de consentimiento.
* **Paso Seguro entre Dominios:** Configura url_passthrough para atribución de conversiones sin almacenamiento local indebido.

---

## 3. Checklist de Seguridad y Privacidad

Consulte a lista detalhada de requisitos técnicos para este país:

* [Checklist Técnico de Conformidade](checklist.md)

---

## 4. Herramientas Técnicas Online (México)

Audite a conformidade das suas etiquetas e proteja o seu domínio com ferramentas online verificadas:

* [Validador de Consent Mode v2 y LFPDPPP](https://tools.tavardt.com/mx/validador-consent-mode-v2-lfpdppp/)
* [Verificador de Cabeceras de Seguridad](https://tools.tavardt.com/mx/analisis-cabeceras-seguridad/)
* [Verificador DMARC contra Suplantación](https://tools.tavardt.com/mx/verificador-dmarc-correo/)
* [Escáner de Archivos Sensibles Expuestos](https://tools.tavardt.com/mx/escaneo-archivos-expuestos/)
* [Portal de Diagnóstico Técnico México](https://tools.tavardt.com/mx/)

---

## 5. Consultoría y Seguridad de Datos

Para auditorías de tagueo, remediación de fugas de datos y consultoría en privacidad digital en México, contacte con **[TAVARDT México](https://ag.tavardt.com/mx/contacto/)**.
