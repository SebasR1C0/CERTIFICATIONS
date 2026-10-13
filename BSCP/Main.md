Fase 1: Base (todo lo demás depende de esto)

1. Information disclosure: es fácil y te entrena a fijarte en errores, comentarios y archivos expuestos. Probabilidad media.
2. Path traversal: es la base para leer archivos, que necesitarás en la etapa 3. Media.
3. Access control: es la clave de la etapa 2. Alta.
4. Authentication: brute force, 2FA y reseteo de contraseñas, típico de la etapa 1. Muy alta.
5. SQL injection: aparece mucho en la etapa 2 para sacar la contraseña del admin. Muy alta.

Fase 2: Lado cliente (etapa 1, robar sesiones)
6. Cross-site scripting (XSS): es la categoría más probable de todo el examen. Domina el robo de cookies y los bypass de filtros. Muy alta.
7. DOM-based vulnerabilities: depende de XSS. Alta.
8. CSRF: requiere entender bien sesiones y cookies. Alta.
9. CORS: media-baja.
10. Clickjacking: baja, pero se aprende rápido.

Fase 3: Lado servidor (etapa 3, leer el archivo)
11. OS command injection: media-alta.
12. File upload vulnerabilities: depende de path traversal y de command injection. Alta.
13. SSRF: alta. Úsala también para llegar a paneles admin internos.
14. XXE: depende de SSRF y de lectura de archivos. Alta.
15. Server-side template injection (SSTI): muy alta en la etapa 3.
16. Insecure deserialization: alta y difícil. Aprende a usar ysoserial y PHPGGC.

Fase 4: Avanzado (muy frecuente en el examen)
17. HTTP Host header attacks: el password reset poisoning sale mucho en la etapa 1. Alta.
18. Web cache poisoning: depende de Host header y de XSS. Alta.
19. HTTP request smuggling: muy probable y de los temas más difíciles. No lo dejes al final del todo.
20. JWT attacks: alta en la etapa 2.
21. OAuth authentication: media-alta.
22. Prototype pollution: media.

Fase 5: Menor probabilidad (repasa si te sobra tiempo)
23. Business logic vulnerabilities: media-baja.
24. NoSQL injection: media-baja.
25. API testing y GraphQL API vulnerabilities: baja-media.
26. WebSockets: baja.
27. Race conditions: baja.
28. Web cache deception: baja.
29. Web LLM attacks: muy baja o no aparece.
