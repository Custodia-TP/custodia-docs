# Marco legal de Custodia: requisitos, decisiones y textos

Historias que consumen estos textos: E1-HU-01, E1-HU-02, E3-HU-09, E4-HU-13, E6-HU-05, E7-HU-08, E8-HU-07, E11-HU-11 

## 0. Propósito

Este documento registra las normas argentinas que investigamos, qué le exige cada una a Custodia y qué decisiones de diseño y de redacción tomamos para cumplirlas. Termina con los textos que la aplicación muestra al usuario, cada uno con los requisitos legales que cubre.

La lógica es siempre la misma: **la norma exige X (artículos), por eso Custodia hace Y, y por eso mostramos el texto Z.**

> Todas las normas se leyeron en su texto oficial (InfoLEG o Boletín Oficial) el 2026-09-18.

---

## 1. Normas investigadas

| Norma | Qué regula | Cómo toca a Custodia |
| --- | --- | --- |
| Ley 25.326 y Decreto 1558/2001 | Protección de datos personales | Consentimiento, información al titular, datos sensibles, seguridad, confidencialidad, cesión, transferencia internacional y derechos del titular |
| Resolución AAIP 14/2018 | Información al titular | Leyenda obligatoria sobre el órgano de control |
| Resolución AAIP 47/2018 | Medidas de seguridad recomendadas | Marco de referencia para las medidas técnicas |
| Ley 26.529 y Decreto 1089/2012 | Derechos del paciente e historia clínica | Titularidad del paciente, autorización para compartir, confidencialidad del profesional, guarda por el efector |
| Ley 27.706 y Decreto 393/2023 | Historia clínica electrónica | Niveles de acceso, trazabilidad, validación de profesionales, firma de la historia clínica |
| Ley 25.506 | Firma digital y electrónica | Cómo nombramos lo que carga un profesional |
| Disposición ANMAT 64/2025 | Software como producto médico | Límite de lo que puede hacer la IA |
| Código Civil y Comercial, art. 26 | Capacidad de las personas menores de edad | Edad mínima de uso |
| Código Penal, art. 156 | Secreto profesional | Contenido del aviso al profesional |
| Proyectos de reforma de la Ley 25.326 | Régimen futuro de datos personales | Criterio de diseño a futuro |

---

## 2. Requisitos y decisiones por norma

### 2.1 Ley 25.326 de Protección de los Datos Personales y su reglamentación

**Nuestros datos son sensibles.** El art. 2 define como datos sensibles a la información referente a la salud. Eso ubica a Custodia en la categoría de mayor protección de la ley y ordena todo lo que sigue.

**Consentimiento (art. 5 inc. 1; Decreto 1558/2001, Anexo I, art. 5).** El tratamiento requiere consentimiento libre, expreso e informado, por escrito o por un medio que se le equipare. Si se presta junto con otras declaraciones, debe figurar en forma expresa y destacada. La reglamentación agrega que la explicación debe ser adecuada al nivel social y cultural del titular, y que el consentimiento puede revocarse en cualquier momento, sin efecto retroactivo.

> Decisión D-01. El consentimiento para datos de salud es una pantalla propia, anterior al formulario de alta y separada de cualquier otro texto. La casilla no viene marcada y el botón de continuar se habilita solo al marcarla. Está escrito en lenguaje llano. La aplicación guarda identificador, versión, hash del texto exacto y fecha y hora de cada aceptación. Revocar equivale a eliminar la cuenta. **Texto: `CONS-ALTA` (sección 3.1).**

**Información obligatoria (art. 6).** Antes de recabar datos hay que informar: a) finalidad y destinatarios; b) existencia del banco de datos e identidad y domicilio del responsable; c) carácter obligatorio o facultativo de los datos; d) consecuencias de darlos, no darlos o darlos inexactos; e) derechos de acceso, rectificación y supresión.

> Decisión D-02. `CONS-ALTA` cubre los cinco incisos, cada uno en un punto numerado. La tabla de la sección 3.1 muestra qué punto cubre cada inciso.

**Nadie puede ser obligado a dar datos sensibles (art. 7 inc. 1).**

> Decisión D-03. Ningún campo de salud es obligatorio: ni la ficha, ni las entradas, ni los adjuntos. La aplicación funciona con lo que el usuario quiera cargar, y así lo dice `CONS-ALTA` punto 6.

**Seguridad (art. 9; Resolución AAIP 47/2018).** El responsable debe adoptar las medidas técnicas y organizativas necesarias para garantizar la seguridad y confidencialidad de los datos y evitar su adulteración, pérdida, consulta o tratamiento no autorizado.

> Decisión D-04. Cifrado extremo a extremo con claves derivadas en el dispositivo del usuario (Anexo A del anteproyecto). El operador almacena solo contenido cifrado y no posee ninguna clave que abra una bóveda. Es la forma más fuerte que encontramos de cumplir el art. 9: la confidencialidad no depende de una política interna sino de una imposibilidad técnica, verificable por la prueba automatizada de ceguera del servidor.

**Confidencialidad (art. 10).** Todas las personas que intervienen en el tratamiento están obligadas al secreto profesional, aun después de terminada su relación.

> Decisión D-05. El equipo del proyecto asume el deber de secreto sobre los datos técnicos que conoce. El profesional que accede asume el suyo al aceptar `AVISO-PROF`.

**Cesión (art. 11 incs. 1 y 2).** Los datos solo pueden cederse con consentimiento previo del titular, informándole la finalidad e identificando al cesionario; ese consentimiento es revocable.

> Decisión D-06. Cada acceso es una autorización explícita del titular, con alcance, permisos y vigencia definidos por él, e identidad del profesional mostrada antes de conceder. Se puede cancelar en cualquier momento con efecto inmediato. Custodia no cede datos a nadie más.

**Transferencia internacional (art. 12).** Está prohibida hacia países sin nivel de protección adecuado.

> Decisión D-07. Toda la infraestructura, incluido el procesamiento con IA, es propia del proyecto y no usa servicios externos. Cualquier despliegue fuera del país se limita a datos sintéticos. `CONS-ALTA` punto 5 lo informa.

**Derechos del titular (arts. 14 y 16).** Acceso dentro de los 10 días corridos, gratuito cada 6 meses; rectificación, actualización o supresión dentro de los 5 días hábiles.

> Decisión D-08. El titular ejerce la mayoría de sus derechos por sí mismo desde la aplicación: exportación completa (acceso), edición (rectificación y actualización) y borrado o eliminación de la cuenta (supresión). Para los datos técnicos que el operador sí conoce se ofrece un correo de contacto con los plazos legales. `CONS-ALTA` punto 8.

**Leyenda del órgano de control (Resolución AAIP 14/2018, art. 3).** Debe incluirse textualmente un aviso sobre la atribución de la AAIP para atender denuncias.

> Decisión D-09. La leyenda va al pie de `CONS-ALTA`, con el texto literal de la resolución.

**Consentimiento por documento para la transcripción asistida.** La transcripción es el único punto en que un documento sale del dispositivo sin cifrar. Eso cambia el tratamiento respecto de lo informado en el alta, por lo que aplican otra vez los arts. 5 y 6 (consentimiento informado, finalidad y consecuencias) y el art. 9 (seguridad).

> Decisión D-10. Antes de cada transcripción se pide un consentimiento específico para ese documento, sin opción de "no volver a preguntar". El texto informa qué se envía, a dónde, que no se guarda copia y que el resultado es un borrador que el usuario revisa. El servicio de extracción no persiste nada, no registra contenido y no tiene salida a internet. **Texto: `CONS-EXTR` (sección 3.2).**

### 2.2 Ley 26.529 de Derechos del Paciente y Decreto 1089/2012

**Titularidad (art. 14).** El paciente es el titular de su historia clínica y puede pedir copia en cualquier momento.

> Decisión D-11. Es el fundamento del producto: Custodia le da al titular un lugar donde reunir las copias que la ley le reconoce y controlarlas.

**Información a terceros solo con autorización (art. 4) y profesionales legitimados con autorización expresa (art. 19 inc. c).**

> Decisión D-12. Un profesional accede únicamente a través de un acceso que el paciente le concede expresamente. No existe ninguna vía de acceso sin autorización del titular.

**Confidencialidad (art. 2 inc. d; Decreto 1089/2012, Anexo I, art. 2 inc. d).** Toda persona que accede a la documentación clínica debe guardar reserva; la reglamentación lo extiende expresamente a cualquier persona que acceda.

> Decisión D-13. Antes de ver contenido, el profesional acepta un aviso que le recuerda ese deber. Todo lo que ve lleva una marca de agua con su nombre, matrícula, fecha, hora e identificador del acceso, y cada apertura queda en la bitácora. **Texto: `AVISO-PROF` (sección 3.3).**

**Guarda por el efector (art. 18).** El establecimiento o el profesional es depositario de su propia historia clínica durante al menos 10 años.

> Decisión D-14. Custodia no reemplaza esa obligación ni entrega copias al profesional: el visor es de solo lectura. El aviso al profesional le recuerda registrar la atención en su propio sistema.

### 2.3 Ley 27.706 de Historia Clínica Electrónica y Decreto 393/2023

Esta ley rige el Sistema Único de Registro de Historias Clínicas Electrónicas de los efectores. Custodia no es parte de ese sistema, pero adoptamos sus definiciones como estándar de diseño, porque describen lo que el Estado espera de un sistema de información clínica.

**Niveles de acceso (art. 7 inc. a).** La ley define tres niveles: consulta; consulta y actualización; consulta, actualización y modificación.

> Decisión D-15. Custodia implementa los permisos "ver" (consulta) y "cargar" (actualización, sin acceso a lo existente si no se concede "ver"). Ningún profesional puede modificar ni borrar lo que ya existe; lo que carga llega como pendiente y el titular decide si lo incorpora.

**Seguridad y trazabilidad (arts. 6 inc. b y 7 incs. d y e).** La información debe tratarse con seguridad, integridad, autenticidad y trazabilidad, entendida como que toda acción quede asociada de modo inequívoco a un individuo o entidad, dejando rastro del acceso.

> Decisión D-16. Bitácora de solo inserción con encadenamiento por hash, visible y exportable por el titular. Registra identificación del profesional, apertura, cada elemento visto, cargas, cambios de vigencia, vencimiento e intentos posteriores, sin ningún dato clínico.

**Validación de profesionales (Decreto 393/2023, Anexo, art. 6 inc. c).** La identificación de los profesionales se realiza conforme a las matrículas vigentes en la Red Federal de Registros de Profesionales de la Salud (REFEPS), y la autenticación de personas se articula con RENAPER, entre otros.

> Decisión D-17. La identidad declarada del profesional se contrasta contra servicios que reproducen REFEPS y RENAPER (épica E8). Como esos organismos no ofrecen una interfaz abierta, durante el Trabajo Profesional los servicios son simulados y operan con datos sintéticos; la interfaz lo declara (LIM-07).

**Firma de la historia clínica (Ley 27.706, art. 8; Decreto 393/2023, Anexo, art. 8).** La historia clínica electrónica se refrenda con firma digital o electrónica en los términos de la Ley 25.506. Ver 2.4.

### 2.4 Ley 25.506 de Firma Digital

La ley define "firma digital" (art. 2) como un procedimiento que requiere información de exclusivo conocimiento y control del firmante, verificable por terceros, y "firma electrónica" (art. 5) como la que carece de alguno de esos requisitos. Son términos con efectos jurídicos propios.

> Decisión D-18. Lo que carga un profesional se marca como **"Realizado por"**, seguido de su nombre, matrícula, jurisdicción, estado de verificación, fecha y hora. No usamos "firma" ni "firmado" en la interfaz, en las historias de usuario ni en el informe, para no atribuirle a esa marca un valor legal que no tiene. La interfaz aclara que no equivale a una firma digital (LIM-07).

### 2.5 Disposición ANMAT 64/2025 sobre software como producto médico

Es producto médico todo software cuyo uso previsto por el fabricante sea el diagnóstico, prevención, tratamiento o mitigación de una patología o afección específica, y como tal requiere registro ante ANMAT.

> Decisión D-19. El uso previsto de Custodia es guardar, ordenar, transcribir y compartir información. La IA transcribe los valores tal como figuran en el documento y reproduce el diagnóstico textual; no califica valores, no usa colores ni íconos que los valoren, no diagnostica y no recomienda. Ese uso previsto se declara en la bienvenida, en `CONS-EXTR` y en LIM-02.

### 2.6 Código Civil y Comercial, art. 26 [S]

Entre los 13 y los 16 años se presume que el adolescente puede decidir sobre tratamientos no invasivos, y desde los 16 se lo considera adulto para las decisiones sobre el cuidado de su propio cuerpo. Los niños ejercen sus derechos por medio de sus representantes.

> Decisión D-20. Durante el Trabajo Profesional, Custodia admite solo personas mayores de 18 años. La gestión de la información de terceros (hijos, adultos mayores a cargo) queda como trabajo futuro.

### 2.7 Código Penal, art. 156 [S]

Reprime a quien, teniendo noticia de un secreto por razón de su profesión, lo revela sin justa causa.

> Decisión D-21. Sostiene el punto 4 de `AVISO-PROF` sobre el secreto profesional. No se cita el artículo en la interfaz.

### 2.8 Reforma de la Ley 25.326 [S]

Hay proyectos de reforma integral en trámite, sin sanción (entre ellos el 3397-D-2026, que prevé notificar incidentes a la autoridad dentro de las 72 horas).

> Decisión D-22. Diseñamos con minimización de datos, privacidad por diseño y portabilidad (exportación FHIR), que son los ejes comunes de todos los proyectos. Así, una reforma no obliga a rehacer la arquitectura.

---

## 3. Textos que mostramos y por qué

Reglas comunes: cada texto tiene identificador y versión; un cambio de contenido sube la versión mayor y obliga a aceptar de nuevo. Ningún texto afirma que el contenido sea imposible de copiar. Los textos de interfaz no citan artículos. `[COMPLETAR: ...]` se define antes de la v1.0; `{...}` lo completa la aplicación.

### 3.1 `CONS-ALTA` v0.2 · Consentimiento para el tratamiento de datos de salud

**Por qué existe:** Ley 25.326, arts. 5, 6, 7 inc. 1, 11 y 12; Decreto 1558/2001, art. 5; Resolución AAIP 14/2018. Decisiones D-01 a D-09.

| Requisito | Dónde lo cubre el texto |
| --- | --- |
| Art. 6 a) finalidad y destinatarios | Puntos 1 y 5 |
| Art. 6 b) existencia del banco, responsable y domicilio | Puntos 2 y 10 |
| Art. 6 c) carácter facultativo | Punto 6 |
| Art. 6 d) consecuencias | Puntos 6 y 7 |
| Art. 6 e) derechos | Punto 8 |
| Revocación sin efecto retroactivo | Punto 9 |
| Leyenda de la AAIP | Pie |

> **Antes de crear tu bóveda**
>
> **Custodia es un prototipo académico.** Forma parte de un Trabajo Profesional de Ingeniería en Informática de la Facultad de Ingeniería de la Universidad de Buenos Aires. Mientras dure el proyecto, usala únicamente con información inventada. No cargues datos de salud reales, ni tuyos ni de otras personas. *(Párrafo exclusivo de la versión del Trabajo Profesional.)*
>
> **1. Para qué sirve.** Custodia te permite guardar en un solo lugar tu información de salud (tu ficha, tus consultas, internaciones y estudios, y los documentos que los respaldan), ordenarla, y compartir la parte que elijas con los profesionales que elijas, por el tiempo que elijas.
>
> **2. Qué datos se tratan.**
> a) La información de salud que cargues vos o que un profesional cargue con tu autorización. La ley la considera un dato sensible.
> b) Los datos de tu cuenta: tu correo electrónico.
> c) Datos técnicos necesarios para que el servicio funcione: identificadores, tamaños y fechas de los archivos, el registro de actividad de tu bóveda, y tu dirección IP transformada de forma que no se pueda reconstruir.
>
> **3. Quién puede leer tu información de salud.** Se cifra en tu dispositivo, antes de salir de él, con claves que se generan a partir de tu frase de acceso. Quienes operamos Custodia no tenemos esas claves y no podemos leer el contenido. Pueden leerlo vos y los profesionales a los que les des un acceso, y solo lo que incluyas en ese acceso, mientras esté vigente.
> Hay una única excepción: si pedís que la aplicación transcriba un documento, ese documento se procesa sin cifrar en un servicio del proyecto, de forma temporal y solo después de que lo autorices para ese documento en particular.
>
> **4. Qué sí conocemos.** Conocemos los datos técnicos del punto 2 c), incluido quién compartió con quién y cuándo, aunque no qué se compartió.
>
> **5. Con quién se comparte.** Solo con los profesionales a los que vos les des acceso. No vendemos, no cedemos y no transferimos tus datos a terceros ni a otros países.
>
> **6. Nada es obligatorio.** Ningún dato de salud es obligatorio. Si no cargás algo, la aplicación funciona igual con lo que tengas. Lo que cargás vos queda identificado como realizado por vos; Custodia no verifica si es exacto.
>
> **7. Si perdés tu frase y tu clave de recuperación, perdés tu bóveda.** Como no tenemos tus claves, no podemos recuperarla por vos. Vas a recibir una clave de recuperación en el paso siguiente: guardala.
>
> **8. Tus derechos.** Podés acceder a tus datos, corregirlos, actualizarlos y eliminarlos. Casi todo lo podés hacer desde la aplicación: exportar tu historial completo, editar, borrar entradas o eliminar la cuenta. Sobre los datos técnicos que sí conocemos, podés escribirnos a `[COMPLETAR: correo de contacto]`. Respondemos los pedidos de acceso dentro de los 10 días corridos y los de corrección o eliminación dentro de los 5 días hábiles. Cuando borrás algo, el contenido se destruye y queda solo la constancia de que se borró, sin información de salud.
>
> **9. Podés retirar este consentimiento cuando quieras,** eliminando tu cuenta. Retirarlo no afecta lo que ya se hizo antes.
>
> **10. Responsable.** `[COMPLETAR: nombre del responsable y domicilio]`. Contacto: `[COMPLETAR: correo]`.
>
> LA AGENCIA DE ACCESO A LA INFORMACIÓN PÚBLICA, en su carácter de Órgano de Control de la Ley N° 25.326, tiene la atribución de atender las denuncias y reclamos que interpongan quienes resulten afectados en sus derechos por incumplimiento de las normas vigentes en materia de protección de datos personales.
>
> ☐ Leí esta información y doy mi consentimiento libre, expreso e informado para que Custodia trate mis datos de salud con las finalidades descriptas.
>
> [ Continuar ]

Registro: evento `consent.accepted` con `text_id`, `version`, `text_sha256` y fecha y hora, sin datos clínicos.

### 3.2 `CONS-EXTR` v0.2 · Consentimiento por documento para la transcripción asistida

**Por qué existe:** Ley 25.326, arts. 5, 6 y 9; Disposición ANMAT 64/2025. Decisiones D-10 y D-19. Se muestra cada vez que el usuario toca "Completar con IA" (E4-HU-13), sin opción de omitirlo.

> **Transcribir "{nombre del documento}"**
>
> Para leer este documento, Custodia tiene que enviarlo sin cifrar a su servicio de transcripción.
>
> - Se envía solo este documento.
> - Se procesa en infraestructura operada por el equipo del proyecto, sin servicios externos y sin salida a internet.
> - No se guarda ninguna copia: el archivo se borra al terminar, también si ocurre un error.
> - El resultado es un borrador. Nada se guarda en tu historial hasta que lo revises y lo confirmes.
>
> La transcripción copia lo que dice el documento. No interpreta valores, no indica si algo está bien o mal, no diagnostica y no recomienda nada. Puede leer mal algún dato: revisá cada campo antes de confirmar.
>
> [ Cancelar ]  [ Enviar este documento ]

Registro: evento `extraction.requested` con el identificador opaco del documento, `text_id` y `version`.

### 3.3 `AVISO-PROF` v0.2 · Aviso de uso para profesionales

**Por qué existe:** Ley 26.529, arts. 2 inc. d, 4, 18 y 19 inc. c; Decreto 1089/2012, art. 2 inc. d; Ley 25.326, art. 10; Ley 27.706, art. 7 inc. e; Código Penal, art. 156. Decisiones D-12 a D-16 y D-21. Se muestra después de la identificación y del código, antes de cualquier contenido (E6-HU-05).

**Variante con permiso de consulta (`AVISO-PROF-VER`)**

> **Antes de ver la información**
>
> Estás por consultar información de salud que pertenece a la persona que te dio este acceso, que es la titular de su historia clínica. Al continuar, aceptás lo siguiente:
>
> 1. Podés consultar esta información mientras el acceso esté vigente y solo para atender a esta persona.
> 2. No debés copiarla, capturarla, fotografiarla ni compartirla. Todo lo que se muestra lleva tu nombre, tu matrícula, la fecha y la hora, y cada cosa que abrís queda registrada con tu identidad. La persona puede ver ese registro.
> 3. Custodia no reemplaza tu propia historia clínica. Lo que necesites conservar de esta atención registralo en el sistema de tu institución o de tu consultorio.
> 4. Rigen tu deber de confidencialidad y tu secreto profesional sobre todo lo que veas.
> 5. Si el acceso te permite cargar, lo que cargues queda marcado como realizado por vos y le llega a la persona como pendiente. No podés modificar ni borrar nada de lo que ya existe.
>
> Estás actuando como: **{nombre y apellido} · {matrícula} · {jurisdicción}** · {estado de verificación}
>
> ☐ Leí y acepto estas condiciones.  [ Continuar ]

**Variante solo carga (`AVISO-PROF-CARGA`)**

> **Antes de cargar información**
>
> Vas a cargar información en el historial de salud de la persona que te dio este acceso. No vas a poder ver nada de lo que ya contiene.
>
> 1. Lo que cargues queda marcado como realizado por vos y le llega a la persona como pendiente; ella decide si lo incorpora.
> 2. No podés modificar ni borrar nada de lo que ya existe.
> 3. Custodia no reemplaza tu propia historia clínica. Lo que corresponda a esta atención registralo también en el sistema de tu institución o de tu consultorio.
>
> Estás actuando como: **{nombre y apellido} · {matrícula} · {jurisdicción}** · {estado de verificación}
>
> ☐ Leí y acepto estas condiciones.  [ Continuar ]

Registro: evento `grant.notice_accepted` con `text_id`, `version`, identidad del profesional y `grant_id`.

### 3.4 Límites declarados

**Por qué existen:** el consentimiento informado (Ley 25.326, arts. 5 y 6) exige que el titular conozca las consecuencias del tratamiento, incluidas las que el sistema no puede evitar. Declararlos es parte de informar, y evita prometer garantías que la tecnología no da.

| ID | Límite | Texto para la interfaz | Dónde se muestra |
| --- | --- | --- | --- |
| LIM-01 | Copia por fuera de la aplicación | Custodia no permite descargar, imprimir ni copiar lo que compartís, pero no puede impedir que alguien fotografíe la pantalla con otro dispositivo o haga una captura en una computadora. Por eso todo lo que ve un profesional lleva su nombre y su matrícula. En la aplicación Android, además, el sistema bloquea las capturas. | Bienvenida, armado de acceso |
| LIM-02 | Sin interpretación clínica | Custodia ordena y transcribe tu información. No interpreta resultados, no indica si un valor es normal y no diagnostica ni recomienda. | Bienvenida, `CONS-EXTR` |
| LIM-03 | Cliente web | En la versión web, tu seguridad depende de que el código que te entrega el servidor sea el publicado. Lo protegemos con controles del navegador y con código abierto verificable. En la aplicación Android el código viaja firmado dentro del paquete instalado. | Página de seguridad |
| LIM-04 | Transcripción sin cifrar | Si pedís transcribir un documento, ese documento se procesa sin cifrar, de forma temporal, en un servicio del proyecto. | `CONS-EXTR` |
| LIM-05 | Pérdida irreversible | Si perdés a la vez tu frase de acceso y tu clave de recuperación, tu bóveda se pierde para siempre. Nadie puede recuperarla. | Bienvenida, `CONS-ALTA`, clave de recuperación |
| LIM-06 | Metadatos de tráfico | El servidor no puede leer tu información, pero sí sabe con quién compartiste y cuándo. | Bienvenida, `CONS-ALTA` |
| LIM-07 | Identidad del profesional | Durante este proyecto, la matrícula del profesional se coteja contra un servicio simulado con datos ficticios, así que no acredita nada oficialmente. Además, que algo figure como "Realizado por" un profesional no equivale a una firma digital ni forma parte de su historia clínica institucional. | Bienvenida, bandeja de pendientes, detalle de entrada |
| LIM-08 | Alcance de la actividad | El registro de actividad muestra qué se abrió dentro de Custodia y con qué identidad. No muestra qué hizo el profesional con esa información fuera de la aplicación. | Vista de actividad |

### 3.5 Avisos breves de interfaz

| ID | Contexto (historia) | Norma o decisión | Texto |
| --- | --- | --- | --- |
| `AV-COMPARTIR` | Confirmación de un acceso (E5-HU-04) | Ley 25.326 art. 11; D-06 | Vas a compartir {n} elementos con permiso de {ver / cargar / ver y cargar} durante {duración}. Podés extender, acortar o cancelar el acceso en cualquier momento. La persona que lo abra no podrá descargar nada, pero sí podría fotografiar la pantalla. |
| `AV-CODIGO` | Entrega remota (E5-HU-14) | Ley 25.326 art. 9; D-04 | Mandá el enlace y el código por canales distintos. Si alguien obtiene los dos, puede abrir el acceso mientras esté vigente. |
| `AV-DESCARGA` | Descarga del original por el titular (E3-HU-09) | Ley 25.326 art. 9 | El archivo se va a guardar sin cifrar en este dispositivo. Desde ese momento, Custodia ya no lo protege. |
| `AV-RECUPERACION` | Clave de recuperación (E1-HU-11) | Ley 25.326 art. 6 d; LIM-05 | Esta clave es la única forma de recuperar tu bóveda si olvidás tu frase. No la vamos a volver a mostrar. Guardala fuera de este dispositivo. |
| `AV-PENDIENTE` | Bandeja de pendientes (E7-HU-08) | Ley 25.506; D-18 | Realizado por {nombre} · {matrícula} · {jurisdicción} · {estado de verificación} · {fecha y hora}. Revisalo antes de incorporarlo a tu historial. |
| `AV-NO-VERIFICADO` | Registro no disponible (E8-HU-10) | Decreto 393/2023 art. 6 c; D-17 | No pudimos verificar la matrícula en este momento. Podés dar el acceso igual; va a quedar registrado como "identidad declarada, no verificada". |
| `AV-DISCORDANTE` | Datos discordantes (E8-HU-08) | Decreto 393/2023 art. 6 c; D-17 | Los datos que declaró este profesional no coinciden con el registro en: {campo}. Podés dar el acceso igual; tu decisión va a quedar registrada. |
| `AV-BORRADO` | Borrado (E2-HU-09) | Ley 25.326 art. 16 | Esto no se puede deshacer. El contenido se destruye y queda solo la constancia de que lo borraste, sin información de salud. |

---

## 4. Registro de decisiones

| ID | Decisión | Norma que la origina |
| --- | --- | --- |
| D-01 | Consentimiento en pantalla propia, casilla sin marcar, aceptación versionada | Ley 25.326 art. 5; Dec. 1558/2001 art. 5 |
| D-02 | El consentimiento cubre los cinco incisos de información obligatoria | Ley 25.326 art. 6 |
| D-03 | Ningún dato de salud obligatorio | Ley 25.326 art. 7 inc. 1 |
| D-04 | Cifrado extremo a extremo con claves en el dispositivo | Ley 25.326 art. 9; Res. AAIP 47/2018 |
| D-05 | Deber de secreto del equipo y del profesional | Ley 25.326 art. 10 |
| D-06 | Cada acceso es una autorización explícita, acotada y revocable | Ley 25.326 art. 11 |
| D-07 | Infraestructura propia, sin servicios externos ni transferencia al exterior | Ley 25.326 art. 12 |
| D-08 | Derechos ejercidos desde la aplicación, más contacto con plazos legales | Ley 25.326 arts. 14 y 16 |
| D-09 | Leyenda de la AAIP al pie del consentimiento | Res. AAIP 14/2018 art. 3 |
| D-10 | Consentimiento específico por cada documento a transcribir | Ley 25.326 arts. 5, 6 y 9 |
| D-11 | El titular controla su copia de la historia clínica | Ley 26.529 art. 14 |
| D-12 | Acceso del profesional solo con autorización expresa del titular | Ley 26.529 arts. 4 y 19 inc. c |
| D-13 | Aviso de confidencialidad, marca de agua nominal y registro de cada apertura | Ley 26.529 art. 2 inc. d; Dec. 1089/2012 art. 2 inc. d |
| D-14 | Visor de solo lectura; recordatorio de registrar en la historia clínica propia | Ley 26.529 art. 18 |
| D-15 | Permisos "ver" y "cargar", sin modificación | Ley 27.706 art. 7 inc. a |
| D-16 | Bitácora de solo inserción encadenada por hash | Ley 27.706 arts. 6 inc. b y 7 inc. e |
| D-17 | Verificación de matrícula contra REFEPS y RENAPER (simulados en el TP) | Dec. 393/2023 art. 6 inc. c |
| D-18 | "Realizado por" en lugar de "firma" | Ley 25.506 arts. 2 y 5; Ley 27.706 art. 8 |
| D-19 | La IA transcribe y no interpreta | Disp. ANMAT 64/2025 |
| D-20 | Solo mayores de 18 años durante el TP | Código Civil y Comercial art. 26 |
| D-21 | Aviso de secreto profesional al profesional | Código Penal art. 156 |
| D-22 | Minimización, privacidad por diseño y portabilidad | Proyectos de reforma de la Ley 25.326 |

---

## 5. Fuentes


- Ley 25.326, texto actualizado. https://servicios.infoleg.gob.ar/infolegInternet/anexos/60000-64999/64790/texact.htm
- Decreto 1558/2001, texto actualizado. https://servicios.infoleg.gob.ar/infolegInternet/anexos/70000-74999/70368/texact.htm
- Resolución AAIP 14/2018. https://servicios.infoleg.gob.ar/infolegInternet/anexos/305000-309999/307621/norma.htm
- Resolución AAIP 47/2018. https://www.boletinoficial.gob.ar/detalleAviso/primera/188654/20180725
- Ley 26.529, texto actualizado. https://servicios.infoleg.gob.ar/infolegInternet/anexos/160000-164999/160432/texact.htm
- Decreto 1089/2012. https://servicios.infoleg.gob.ar/infolegInternet/anexos/195000-199999/199296/norma.htm
- Ley 27.706. https://servicios.infoleg.gob.ar/infolegInternet/anexos/380000-384999/380710/norma.htm
- Decreto 393/2023 y su Anexo. https://servicios.infoleg.gob.ar/infolegInternet/anexos/385000-389999/387475/norma.htm
- Ley 25.506, texto actualizado. https://www.argentina.gob.ar/normativa/nacional/ley-25506-70749/actualizacion
- ANMAT, noticia oficial sobre la Disposición 64/2025 (10/09/2026). https://www.argentina.gob.ar/noticias/anmat-actualiza-los-criterios-regulatorios-para-software-como-dispositivo-medico-samd . Disposición en el Boletín Oficial: https://www.boletinoficial.gob.ar/detalleAviso/primera/319522/20250113

