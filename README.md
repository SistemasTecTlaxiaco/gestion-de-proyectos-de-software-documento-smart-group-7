# Documento Detallado: Objetivo SMART y Análisis de Viabilidad Multidimensional (Grupo 7)

## Infraestructura Descentralizada para la Preservación y Consulta Inmutable de Recursos Jurídicos en la Región Mixteca

> **Institución:** Instituto Tecnológico de Tlaxiaco (TecNM)  
> **Carrera:** Ingeniería en Sistemas Computacionales  
> **Asignatura:** Gestión de Proyectos de Software (SCG-1009)  
> **Unidad 3:** Planificación del Proyecto  
> **Iniciativa / Ecosistema:** Open Hub Tec (Instituto Tecnológico de Tlaxiaco)  
> **Marco de Trabajo:** eduScrum (Sprint 3)  
> **Equipo Evaluado:** Grupo 7  
> **Repositorio de Referencia Técnica:** [`gestion-de-proyectos-de-software-informe-de-estandares-de-ca-group-4`](https://github.com/SistemasTecTlaxiaco/gestion-de-proyectos-de-software-informe-de-estandares-de-ca-group-4.git)  
> **Repositorio Oficial del Entregable:** [`gestion-de-proyectos-de-software-documento-smart-group-7`](https://github.com/SistemasTecTlaxiaco/gestion-de-proyectos-de-software-documento-smart-group-7.git)  
> **eduScrum Master:** Lizeth Nallely López García  
> **Fecha:** 14 Octubre 2026  

---

## 🧭 Índice del Entregable

El documento oficial de planificación se encuentra estructurado en el archivo técnico principal:
📁 **[`docs/planificacion-smart-viabilidad.md`](./docs/planificacion-smart-viabilidad.md)**

A continuación, se presenta la especificación íntegra y detallada del objetivo SMART y el análisis de viabilidad multidimensional:

---

## 1. Formulación del Objetivo SMART

> **Objetivo del Proyecto:**  
> "Desarrollar y validar un Producto Mínimo Viable (MVP) con arquitectura *offline-first*, almacenamiento local cifrado (SQLCipher) y contratos inteligentes en Soroban (Stellar) para registrar la autoría e inmutabilidad de al menos **30 recursos jurídicos y agrarios estratégicos** (amparos, actas comunales, peritajes territoriales) con respaldo colegiado (*Web of Trust*) de **5 núcleos agrarios y comités de bienes comunales** de la Mixteca Alta oaxaqueña, alcanzando un tiempo de respuesta de consulta local inferior a **1.5 segundos en dispositivos móviles Android Go**, sincronización diferencial con cargas útiles inferiores a **25 KB en redes 2G/EDGE** y una tasa de éxito transaccional del **98%**, en un periodo de **14 semanas (Sprints 1 al 4)** bajo el marco eduScrum."

### Desglose de Dimensiones SMART:

* **Specific (Específico):** Construcción de un protocolo descentralizado, soberano y tolerante a desconexión prolongada que combina indexación local cifrada en reposo con SQLCipher (AES-256), purga forzosa de metadatos y datos de identificación personal (PII) en el dispositivo de origen, identidades autosoberanas efímeras (W3C DID `did:key` sobre ed25519), registro inmutable de hashes SHA-256 y CIDs v1 en contratos Soroban (Stellar) con política de rentas TTL (*State Archival*), y esquemas de validación multifirma colegiada (EIP-712 / Soroban Auth) que reflejan fielmente los acuerdos de la Asamblea General de Comuneros según los Usos y Costumbres de los pueblos mixtecos.
* **Measurable (Medible):**
  1. Certificación e indexación inmutable de **30 recursos jurídicos y agrarios reales** (amparos indirectos, resoluciones del Tribunal Unitario Agrario, peritajes topográficos/antropológicos y actas ejidales).
  2. Vinculación y validación mediante quórum multifirma de **5 núcleos agrarios / Comisariados de Bienes Comunales** de la región.
  3. Latencia de búsqueda y filtrado local **≤ 1.5 segundos** en base de datos local SQLite/SQLCipher sobre colecciones de más de 2,000 precedentes en procesadores móviles de gama de entrada.
  4. Carga útil (*payload*) de sincronización incremental diferencial **≤ 25 KB** mediante archivos CAR / HTTP Range.
  5. Tasa de éxito transaccional del **98%** en condiciones de conectividad rural degradada (redes simuladas 2G/EDGE a 50 kbps con 50% de pérdida de paquetes).
  6. Costo por transacción on-chain fijado en la tarifa base mínima de **100 stroops (0.00001 XLM ≈ $0.0000012 USD)**.
* **Achievable (Alcanzable):** Respaldado por el dimensionamiento riguroso del backlog de ingeniería: 31 puntos de historia de usuario distribuidos en cinco historias críticas (US-01 a US-05), 33.0 horas hombre de aseguramiento de calidad (Costo de la Calidad - CoQ) y una arquitectura 100% local de costo cero (Soroban CLI sandbox, IPFS Kubo embebido, SQLite) distribuible en las 10 a 12 horas semanales por integrante de un equipo eduScrum universitario.
* **Relevant (Relevante):** Erradica la vulnerabilidad e indefensión jurídica de las comunidades agrarias e indígenas frente a megaproyectos extractivistas, minería a cielo abierto y despojo de agua; anula la alteración o falsificación de sentencias agrarias; salvaguarda la vida e integridad de defensores territoriales mediante la eliminación absoluta de metadatos de autoría y prescinde de intermediarios gubernamentales o notariales que pueden ser cooptados.
* **Time-bound (Temporalizado):** Planificado y ejecutado en un ciclo semestral de **14 semanas académicas**, articulado en **4 Sprints eduScrum** (Sprint 1: Núcleo Criptográfico & Contrato Soroban; Sprint 2: Base de Datos Local Offline & Búsqueda Rápida; Sprint 3: Privacidad Defensiva, DID & Multifirma Comunitaria; Sprint 4: Pruebas de Resiliencia 2G, Simulación de Cortes y Cierre de Informe).

---

## 2. Trazabilidad con Sprints 1 y 2 (Backlog y Costo de la Calidad)

El presente plan de viabilidad se sustenta rigurosamente en las métricas de ingeniería de software, estándares ISO/IEC 25010 y criterios de aceptación (CA-1.1 al CA-5.4) consolidados en los ciclos previos:

### A. Trazabilidad con Historias de Usuario (Sprint 1)

* **US-01 (Registro e Inmutabilidad de Recursos Jurídicos - 8 pts):** Almacenamiento inmutable del CID v1 y hash SHA-256 en contrato Soroban (Rust) con almacenamiento persistente (`Persistent Storage` TTL) y emisión de eventos indexados `LegalResourceRegistered`. Bloqueo absoluto de sobreescritura (`require(!storage.has(&cid))`) garantizando no repudio (CA-1.1 a CA-1.4).
* **US-02 (Consulta y Filtrado Seguro de Precedentes - 5 pts):** Búsqueda y filtrado ultrarrápido contra catálogo local embebido con índices B-Tree en SQLite sobre tipo de amenaza agraria (minería, agua, tala) y tenencia de la tierra, respondiendo en < 1.5 s de forma desconectada. Descarga P2P comunitaria por cercanía vía mDNS y Bitswap en routers locales (CA-2.1 a CA-2.4).
* **US-03 (Publicación Anónima Protegida con DID - 8 pts):** Sanitización local de binarios PDF/imágenes purgando metadatos EXIF, firmas de software y datos de geolocalización (PII). Autenticación descentralizada con llaves efímeras W3C DID (`did:key` ed25519) sin correos ni celulares, y enrutamiento por relés seguros para evitar triangulación celular en antenas 2G (CA-3.1 a CA-3.4).
* **US-04 (Respaldo y Validación Comunitaria Web of Trust - 5 pts):** Acreditación y firma colegiada basada en el estándar EIP-712 / Soroban Auth que refleja el quórum asambleario del Comisariado y Consejo de Vigilancia. Arquitectura sin llave de administración maestra (*ownerless smart contract*), eliminando backdoors o censura centralizada (CA-4.1 a CA-4.4).
* **US-05 (Sincronización Offline-First y Resiliencia en Red 2G - 5 pts):** Persistencia en cliente cifrada en reposo mediante AES-256 (SQLCipher), verificación matemática local del hash SHA-256 sin conexión y sincronización incremental diferencial ultraligera (payloads ≤ 25 KB) tolerante a caídas de red y 50% de pérdida de paquetes (CA-5.1 a CA-5.4).

**Total Backlog Base:** **31 Puntos de Historia (Story Points)**.

```
[US-01: Inmutabilidad Soroban] ---> CA-1.1 a CA-1.4: WASM, SHA-256, Anti-overwrite
[US-02: Búsqueda Local B-Tree] ----> CA-2.1 a CA-2.4: SQLite embebido (<1.5s), P2P LAN
[US-03: Privacidad DID / PII] -----> CA-3.1 a CA-3.4: Despojo local PII, did:key ed25519
[US-04: Respaldo Comunitario] ----> CA-4.1 a CA-4.4: Multifirma EIP-712, Quórum Usos/Costumbres
[US-05: Sincronización 2G] -------> CA-5.1 a CA-5.4: SQLCipher AES-256, Diff Sync ≤ 25 KB
```

---

### B. Insumos del Costo de la Calidad (Sprint 2 - CoQ)

A partir de la auditoría de calidad realizada a una tarifa estándar de **$150.00 MXN / hora** para el equipo de desarrollo universitario del IT Tlaxiaco:

* **Inversión en Prevención (56.06% / 18.5 h): $2,775.00 MXN**
  * *Actividades:* Diseño formal de contratos Soroban en Rust con tipado estático estricto y cero comportamiento indefinido; configuración de reglas de linteo en CI (`cargo clippy -- -D warnings`); diseño del algoritmo de purga previa de metadatos (EXIF/XMP/PII); modelado de pruebas de invariantes matemáticas (`proptest`) para bloqueo de colisiones; estructuración de índices B-Tree en SQLite local y diseño de esquemas de expiración TTL (*State Archival*).
* **Inversión en Corrección / Evaluación (43.94% / 14.5 h): $2,175.00 MXN**
  * *Actividades:* Pruebas de estrés y simulación de conectividad degradada 2G/EDGE (50 kbps con 50% de descarte de paquetes); pruebas forenses de inyección de metadatos GPS para certificar despojo de PII; pruebas de fuzzing contra Soroban SDK verificando reversión de sobreescrituras; optimización de índices de consulta SQLite en terminales Android Go (RAM < 3 GB); y gestión de excepciones y reconexión ante timeouts de RPC de Stellar.
* **Costo Total de Calidad del Backlog Base:** **$4,950.00 MXN (33.0 horas hombre)**.

> Esta relación prevención-corrección demuestra realismo operativo: el 56% del esfuerzo previene fallas catastróficas de inmutabilidad y seguridad de vida antes del despliegue, mientras que el 44% valida y ajusta el comportamiento frente a la hostilidad del entorno rural de la Mixteca, evitando supuestos irreales de "cero defectos".

---

## 3. Análisis de Viabilidad Técnica y Operativa

### A. Viabilidad Técnica en el Entorno Mixteco

1. **Infraestructura de Conectividad Intermitente y Modo Offline-First:**
   * La orografía accidentada de la Mixteca Alta provoca desconexiones habituales de 48 a 96 horas continuas y pérdidas de paquetes del 35% al 65% en conexiones móviles.
   * La arquitectura desacopla por completo la interfaz de usuario de las llamadas remotas. El cliente ligero consulta, indexa y verifica firmas localmente sobre una base de datos embebida cifrada con **SQLCipher (AES-256)**.
   * Al transitar por zonas con enlace celular mínimo (2G/EDGE) o WiFi comunitario en cabeceras municipales, se ejecuta una sincronización incremental en segundo plano empaquetada en bloques diferenciales (*CAR files / Merkle Trees*) con cargas útiles inferiores a **25 KB**, enviando transacciones firmadas localmente hacia el RPC de Stellar sin bloquear la interfaz.
2. **Limitaciones de Hardware Local y Eficiencia Energética:**
   * El 85% de las autoridades y defensores comunitarios utiliza teléfonos inteligentes básicos (frecuentemente **Android Go** con 2 GB a 3 GB de RAM y procesadores quad-core modestos), además de computadoras recicladas en los Comisariados de Bienes Comunales.
   * El sistema se estructura como una **PWA ultraligera** (HTML5, Tailwind y TypeScript estándar) prescindiendo de emuladores pesados y dependencias monolíticas. El procesamiento criptográfico (SHA-256 y TweetNaCl < 50 KB) se ejecuta en hilos secundarios (*Web Workers*) sin superar el 15% de CPU, protegiendo la carga de la batería durante cortes eléctricos causados por tormentas serranas.
3. **Abstracción Criptográfica y Soberanía Comunitaria:**
   * Las comunidades agrarias no requieren comprar criptomonedas, gestionar llaves maestras complejas ni interactuar con bolsas de cambio (*exchanges*).
   * La red Stellar provee costos mínimos e inmutables (100 stroops por transacción ≈ $0.0000012 USD). Con un fondo comunitario de $1.00 USD pueden anclarse más de 800,000 registros.
   * La gobernanza del contrato inteligente no admite roles `onlyOwner` centralizados; los respaldos se validan colegiadamente mediante el estándar de firmas **EIP-712 / Soroban Auth**, subordinando la tecnología a los consensos de la Asamblea General y respetando el Artículo 2 de la Constitución Política mexicana.

---

### B. Viabilidad Operativa en el Marco eduScrum

* **Estructura del Equipo Multidisciplinario (4 Integrantes):**
  * **Estudiante 1 (Líder de Smart Contracts & Web3):** Lógica del contrato en Soroban (Rust), almacenamiento persistente TTL, invariantes de inmutabilidad y pruebas en sandbox local.
  * **Estudiante 2 (Desarrollador Frontend & Offline-First):** Cliente ligero PWA, base de datos local SQLite/SQLCipher, módulo de búsqueda < 1.5 s e interfaz bilingüe sobria (Español / *Tu'un Sávi*).
  * **Estudiante 3 (Ingeniero de QA, Seguridad y Redes):** Pipeline de CI/CD en GitHub Actions, pruebas de red 2G/EDGE degradada, módulo de purga forense de PII y auditoría con `cargo clippy`.
  * **Estudiante 4 (Documentador, Contexto Agrario & Drips):** Vinculación con núcleos agrarios, modelado de gobernanza comunal, integración de contratos de streaming en Drips v2 y matriz de criterios de aceptación.
* **Capacidad de Carga y Disponibilidad:**
  * Cada integrante dispone de **10 a 12 horas semanales** dedicadas a la materia (40 a 48 horas semanales de esfuerzo global de equipo).
  * La carga total del proyecto (~120 horas de desarrollo global + 33 horas de aseguramiento de calidad = **~153 horas totales**) requiere un promedio de solo 11 horas de equipo a la semana, encajando holgadamente en el calendario académico semestral sin sobrecargar a los estudiantes.
* **Supervisión y Ritmo eduScrum:**
  * Ciclos de sprints quincenales regidos por la *Definition of Done* (DoD): código libre de advertencias (`-D warnings`), pruebas unitarias ejecutadas en local con costo cero, verificación cruzada por pares (*Pull Requests*) y validación continua con el Product Owner del Open Hub Tec.

---

## 4. Análisis de Viabilidad Financiera Web3 y Dictamen Go / No-Go

### A. Estructura de Costos del Proyecto (Estimación a 6 Meses)

| Rubro Presupuestal | Concepto / Detalle Técnico | Costo en MXN | Costo en USD |
| :--- | :--- | :---: | :---: |
| **Desarrollo y Calidad (Ingeniería)** | 120 h de desarrollo + 33 h de CoQ a tarifa estándar universitaria de $150.00 MXN/h (*Tequio Tecnológico Remunerado*) | $18,000.00 MXN | ~$950.00 USD |
| **Infraestructura de Pruebas y Nodos** | Pruebas en Testnet Stellar, sandbox local, dominios comunitarios y soporte local para nodos IPFS Kubo | $3,600.00 MXN | ~$190.00 USD |
| **Validación en Campo y Vinculación** | Memorias USB cifradas para transporte físico, tarjetas SIM prepago para pruebas en celdas 2G/EDGE y traslados a asambleas comunales (Tlaxiaco y municipios circunvecinos) | $5,500.00 MXN | ~$290.00 USD |
| **COSTO TOTAL ESTIMADO** | **Presupuesto integral para la validación y despliegue del MVP** | **$27,100.00 MXN** | **~$1,430.00 USD** |

---

### B. Mecanismos de Financiamiento Web3

1. **Stellar Community Fund (SCF - Tranches de Subvención no Dilutiva):**
   * Convocatoria orientada a infraestructura abierta, bienes públicos e impacto en activos del mundo real (RWA).
   * Modelo de desembolso vinculado estrictamente a **hitos verificables de calidad de software** (*Milestone-Gated Releases*):
     * *Fase 1 (Kickoff):* Contrato Soroban en testnet con cobertura unitaria >90% en Rust (CA-1.1, CA-1.4) $\rightarrow$ **$10,000 USD**.
     * *Fase 2 (Build):* Cliente Offline-First con SQLCipher y pruebas de red 2G (CA-2.1, CA-5.1, CA-5.2) $\rightarrow$ **$15,000 USD**.
     * *Fase 3 (Hardening):* Módulo DID con purga de metadatos y multifirma EIP-712 (CA-3.1, CA-4.1) $\rightarrow$ **$15,000 USD**.
     * *Fase 4 (Launch):* Validación en campo en la Mixteca con sincronización diferencial 2G (CA-5.3, CA-5.4) $\rightarrow$ **$10,000 USD**.
   * El tramo inicial básico ($5,000 a $15,000 USD en USDC/XLM) cubre entre el **350% y el 1,000%** del costo total estimado del proyecto.
2. **Drips Protocol v2 (Streaming Continuo de Capital y Splits Solidarios):**
   * Transmisión continua on-chain segundo a segundo direccionada al repositorio en GitHub (`SistemasTecTlaxiaco/...`) mediante el contrato `RepoDriver`.
   * Matriz programada de reparto solidario determinista (*Drips Splits*):
     * **40% Operación de Nodos Comunitarios:** Mantenimiento de routers locales, baterías solares y almacenamiento IPFS en Comisariados de Bienes Comunales.
     * **25% Becas de Mantenimiento para Estudiantes del IT Tlaxiaco:** Retribución meritocrática para estudiantes que brinden soporte continuo, QA y actualización de dependencias (*Tequio Tecnológico Profesional*).
     * **20% Fondo de Litigio Agrario y Peritajes:** Transferencia directa a abogados y peritos comunitarios en Tribunales Unitarios Agrarios (TUA).
     * **15% Traducción Lingüística y Protección de Emergencia:** Intérpretes en *Tu'un Sávi* (Mixteco) y fondo de contingencia para la protección inmediata de defensores en riesgo.

```
                              +----------------------------------+
                              |    STREAMING DRIPS v2 (100%)     |
                              |  Fondos de Justicia Ambiental    |
                              +----------------------------------+
                                               |
                                               v
                              +----------------------------------+
                              |      DRIPS SPLITS CONTRACT       |
                              +----------------------------------+
                                               |
        +----------------------+---------------+----------------------+
        |                      |                              |       |
        v                      v                              v       v
+----------------+   +-------------------+          +----------------+   +------------------+
|   40% Nodos    |   |  25% Estudiantes  |          |   20% Fondo    |   |  15% Traducción  |
|  Comunitarios  |   |  IT Tlaxiaco      |          |    Jurídico    |   |  Tu'un Sávi      |
| - Routers 2G   |   | - Becas tequio    |          | - Peritajes    |   | - Intérpretes    |
| - Baterías CFE |   | - QA continuo     |          | - Asesoría TUA |   | - Socorro defen. |
+----------------+   +-------------------+          +----------------+   +------------------+
```

---

### C. Dictamen Formal de Viabilidad

| Dimensión | Evaluación | Justificación Resumida |
| :--- | :---: | :--- |
| **Técnica** | **VIABLE** | Arquitectura nativa *Offline-First* con SQLite/SQLCipher (AES-256), contratos deterministas en Rust/Soroban, paquetes diferenciales de sincronización ≤ 25 KB en redes 2G/EDGE y despojo local forense de PII para resguardar la vida. |
| **Operativa** | **VIABLE** | Backlog calibrado en 31 puntos de historia y 33.0 horas de calidad (CoQ), absorbible en 14 semanas por 4 estudiantes eduScrum con disponibilidad de 10-12 h/semana utilizando un stack de desarrollo 100% libre y local. |
| **Financiera** | **VIABLE** | Costo presupuestal total de $1,430 USD cubierto en más de un 350% por la subvención de Stellar Community Fund ($5,000–$15,000 USD) y garantizado a perpetuidad mediante el streaming de capital en Drips Protocol v2. |

> ### DICTAMEN FINAL: **GO (PROYECTO VIABLE Y APROBADO)**  
> Se autoriza formalmente el paso a la fase de ejecución integral del **Sprint 3 del marco eduScrum**. El proyecto satisface con excelencia las exigencias de impacto social y defensa territorial en los núcleos agrarios de la Región Mixteca, viabilidad técnica bajo aislamiento de red e infraestructura energética austera, y sostenibilidad económica descentralizada sin intermediarios financieros convencionales.

---

## 5. Gestión del Equipo y Gobernanza eduScrum

* **Product Owner:** Supervisión de criterios de aceptación (CA-1.1 a CA-5.4), priorización del Product Backlog y alineación estratégica con la iniciativa comunitaria Open Hub Tec del Instituto Tecnológico de Tlaxiaco.
* **eduScrum Master:** Lizeth Nallely López García (Facilitación de impedimentos, monitoreo del tablero de tareas, cadencia de ceremonias ágiles y cumplimiento estricto del *Definition of Done*).
* **Equipo de Desarrollo (Grupo 7 / Grupo 4):** Autogestión de tareas técnicas, desarrollo guiado por pruebas (TDD), revisiones por pares mediante *Pull Requests*, auditorías automatizadas de linteo y dependencias (`cargo clippy`, `cargo audit`, purga de metadatos) y apego irrestricto a los estándares éticos y de software libre.
