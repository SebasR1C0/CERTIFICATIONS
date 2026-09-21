Fase 1 — Los pilares (altísima probabilidad en el BSCP)

1. SQL injection — el más clásico, y el modelo mental de "inyección" que reutilizarás en NoSQLi, command injection, SSTI, etc.
2. Authentication (fuerza bruta, 2FA bypass, lógica de login rota)
3. Path traversal
4. OS command injection
5. Access control (IDOR, privilege escalation) — depende conceptualmente de entender autenticación primero
6. Business logic vulnerabilities — mejor dejarlo después de auth/access control porque requiere pensar en el flujo completo de la app
7. Information disclosure
8. File upload vulnerabilities — a veces se combina con path traversal o RCE, por eso va después de esos dos
   
Fase 2 — Muy frecuentes, algo más técnicos

9. SSRF — conviene saber HTTP a fondo (headers, protocolos) antes
10. XXE injection
11. Cross-site scripting (XSS) — independiente de lo anterior, pero es prerequisito conceptual para CSRF, clickjacking y CORS
12. CSRF
13. CORS
14. Clickjacking

Fase 3 — Importantes, aparecen con buena frecuencia últimamente

15. Insecure deserialization
16. SSTI (Server-side template injection) — se apoya en la lógica de inyección que ya viste en SQLi/command injection
17. Race conditions — tema que ha ganado mucho peso en exámenes recientes
18. DOM-based vulnerabilities (requiere ya dominar XSS)
19. WebSockets

Fase 4 — Relevantes pero algo menos frecuentes en el BSCP clásico

20. JWT attacks
21. OAuth authentication
22. GraphQL API vulnerabilities
23. NoSQL injection
24. API testing (mapa mental de todo lo anterior aplicado a APIs)

Fase 5 — Especializados / menos probables pero no descartables

25. HTTP request smuggling — requiere entender HTTP a bajo nivel; suele ser de los últimos porque es denso
26. Web cache poisoning
27. Web cache deception
28. HTTP Host header attacks
29. Prototype pollution
30. Web LLM attacks (tema nuevo, baja probabilidad todavía en el examen "clásico")


<img width="889" height="251" alt="image" src="https://github.com/user-attachments/assets/f086c2f2-3501-43c3-96f8-f1f3202c4867" />

<img width="524" height="529" alt="image" src="https://github.com/user-attachments/assets/3c9336cc-a8ae-45b7-9d1f-1921a9ea43c7" />
