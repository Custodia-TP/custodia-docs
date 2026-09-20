# Marco legal de Custodia: requisitos, decisiones y textos

Historias que consumen estos textos: E1-HU-01, E1-HU-02, E3-HU-09, E4-HU-13, E6-HU-05, E7-HU-08, E8-HU-07, E11-HU-11 

## 0. Propósito

Este documento tiene en cuenta las normas argentinas que se refieren a los distintos aspectos de este trabajo por lo cual nosotros las investigamos: qué le exige cada una a Custodia y qué decisiones de diseño y de redacción tomamos para cumplirlas. Termina con los textos que la aplicación muestra al usuario, cada uno con los requisitos legales que cubre.

La lógica es siempre la misma: **la norma dice X (cita textual, con su artículo), por eso Custodia hace Y, y como conclusión llegamos al texto Z.**

Las normas se citan entre comillas y de forma textual. Cuando se omite una parte del artículo se marca con [...]. Lo que está fuera de comillas es nuestra lectura.

> Todas las normas se leyeron en su texto oficial (InfoLEG o Boletín Oficial) el 2026-09-18.

> Las citas textuales se contrastaron el 2026-09-20 contra InfoLEG, Argentina.gob.ar y el Boletín Oficial. Los arts. 25 y 26 del Código Civil y Comercial y el art. 156 del Código Penal se tomaron de reproducciones del texto vigente en sitios secundarios (sección 5), y conviene cotejarlos contra InfoLEG.

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
| Disposición ANMAT 64/2025 y comunicado de ANMAT del 10/09/2026 | Registro de productos médicos, y su aplicación a software | Límite de lo que puede hacer la IA |
| Código Civil y Comercial, arts. 25 y 26 | Capacidad de las personas menores de edad | Edad mínima de uso |
| Código Penal, art. 156 | Secreto profesional | Contenido del aviso al profesional |
| Proyectos de reforma de la Ley 25.326 | Régimen futuro de datos personales | Criterio de diseño a futuro |

---

## 2. Requisitos y decisiones por norma

### 2.1 Ley 25.326 de Protección de los Datos Personales y su reglamentación

**Nuestros datos son sensibles (Ley 25.326, art. 2).** El artículo define: "Datos sensibles: Datos personales que revelan origen racial y étnico, opiniones políticas, convicciones religiosas, filosóficas o morales, afiliación sindical e información referente a la salud o a la vida sexual." Eso ubica a Custodia en la categoría de mayor protección de la ley y ordena todo lo que sigue.

**Consentimiento (Ley 25.326, art. 5 inc. 1; Decreto 1558/2001, Anexo I, art. 5).** La ley dice: "El tratamiento de datos personales es ilícito cuando el titular no hubiere prestado su consentimiento libre, expreso e informado, el que deberá constar por escrito, o por otro medio que permita se le equipare, de acuerdo a las circunstancias. El referido consentimiento prestado con otras declaraciones, deberá figurar en forma expresa y destacada, previa notificación al requerido de datos, de la información descrita en el artículo 6° de la presente ley." La reglamentación agrega: "El consentimiento informado es el que está precedido de una explicación, al titular de los datos, en forma adecuada a su nivel social y cultural, de la información a que se refiere el artículo 6º de la Ley Nº 25.326." Y también: "El consentimiento dado para el tratamiento de datos personales puede ser revocado en cualquier tiempo. La revocación no tiene efectos retroactivos."

> Decisión D-01. El consentimiento para datos de salud es una pantalla propia, anterior al formulario de alta y separada de cualquier otro texto. La casilla no viene marcada y el botón de continuar se habilita solo al marcarla. Está escrito en lenguaje llano. La aplicación guarda identificador, versión, hash del texto exacto y fecha y hora de cada aceptación. Revocar equivale a eliminar la cuenta. **Texto: `CONS-ALTA` (sección 3.1).**

**Información obligatoria (Ley 25.326, art. 6).** La ley dice: "Cuando se recaben datos personales se deberá informar previamente a sus titulares en forma expresa y clara: a) La finalidad para la que serán tratados y quiénes pueden ser sus destinatarios o clase de destinatarios; b) La existencia del archivo, registro, banco de datos, electrónico o de cualquier otro tipo, de que se trate y la identidad y domicilio de su responsable; c) El carácter obligatorio o facultativo de las respuestas al cuestionario que se le proponga, en especial en cuanto a los datos referidos en el artículo siguiente; d) Las consecuencias de proporcionar los datos, de la negativa a hacerlo o de la inexactitud de los mismos; e) La posibilidad del interesado de ejercer los derechos de acceso, rectificación y supresión de los datos."

> Decisión D-02. `CONS-ALTA` cubre los cinco incisos, cada uno en un punto numerado. La tabla de la sección 3.1 muestra qué punto cubre cada inciso.

**Nadie puede ser obligado a dar datos sensibles (Ley 25.326, art. 7 inc. 1).** La ley dice: "Ninguna persona puede ser obligada a proporcionar datos sensibles."

> Decisión D-03. Ningún campo de salud es obligatorio: ni la ficha, ni las entradas, ni los adjuntos. La aplicación funciona con lo que el usuario quiera cargar, y así lo dice `CONS-ALTA` punto 6.

**Seguridad (Ley 25.326, art. 9 inc. 1; Resolución AAIP 47/2018, art. 2).** La ley dice: "El responsable o usuario del archivo de datos debe adoptar las medidas técnicas y organizativas que resulten necesarias para garantizar la seguridad y confidencialidad de los datos personales, de modo de evitar su adulteración, pérdida, consulta o tratamiento no autorizado, y que permitan detectar desviaciones, intencionales o no, de información, ya sea que los riesgos provengan de la acción humana o del medio técnico utilizado." La Resolución 47/2018 dispone: "Apruébese el documento denominado “MEDIDAS DE SEGURIDAD RECOMENDADAS PARA EL TRATAMIENTO Y CONSERVACION DE LOS DATOS PERSONALES EN MEDIOS INFORMATIZADOS”, cuyo texto forma parte integrante de la presente como Anexo I (IF-2018-34800234-APN-AAIP)." El contenido de ese Anexo no pudimos leerlo (se publica solo en la edición web del Boletín Oficial), por lo que no lo citamos.

> Decisión D-04. Cifrado extremo a extremo con claves derivadas en el dispositivo del usuario (Anexo A del anteproyecto). El operador almacena solo contenido cifrado y no posee ninguna clave que abra una bóveda. Es la forma más fuerte que encontramos de cumplir el art. 9: la confidencialidad no depende de una política interna sino de una imposibilidad técnica, verificable por la prueba automatizada de ceguera del servidor.

**Confidencialidad (Ley 25.326, art. 10 inc. 1).** La ley dice: "El responsable y las personas que intervengan en cualquier fase del tratamiento de datos personales están obligados al secreto profesional respecto de los mismos. Tal obligación subsistirá aun después de finalizada su relación con el titular del archivo de datos."

> Decisión D-05. El equipo del proyecto asume el deber de secreto sobre los datos técnicos que conoce. El profesional que accede asume el suyo al aceptar `AVISO-PROF`.

**Cesión (Ley 25.326, art. 11 incs. 1 y 2).** La ley dice: "Los datos personales objeto de tratamiento sólo pueden ser cedidos para el cumplimiento de los fines directamente relacionados con el interés legítimo del cedente y del cesionario y con el previo consentimiento del titular de los datos, al que se le debe informar sobre la finalidad de la cesión e identificar al cesionario o los elementos que permitan hacerlo." Y: "El consentimiento para la cesión es revocable."

> Decisión D-06. Cada acceso es una autorización explícita del titular, con alcance, permisos y vigencia definidos por él, e identidad del profesional mostrada antes de conceder. Se puede cancelar en cualquier momento con efecto inmediato. Custodia no cede datos a nadie más.

**Transferencia internacional (Ley 25.326, art. 12 inc. 1).** La ley dice: "Es prohibida la transferencia de datos personales de cualquier tipo con países u organismos internacionales o supranacionales, que no propocionen [sic] niveles de protección adecuados."

> Decisión D-07. Toda la infraestructura, incluido el procesamiento con IA, es propia del proyecto y no usa servicios externos. Cualquier despliegue fuera del país se limita a datos sintéticos. `CONS-ALTA` punto 5 lo informa.

**Derechos del titular (Ley 25.326, arts. 14 y 16).** Sobre el acceso, el art. 14 dice: "El responsable o usuario debe proporcionar la información solicitada dentro de los diez días corridos de haber sido intimado fehacientemente." Y: "El derecho de acceso a que se refiere este artículo sólo puede ser ejercido en forma gratuita a intervalos no inferiores a seis meses, salvo que se acredite un interés legítimo al efecto." Sobre la rectificación, actualización y supresión, el art. 16 dice: "Toda persona tiene derecho a que sean rectificados, actualizados y, cuando corresponda, suprimidos o sometidos a confidencialidad los datos personales de los que sea titular, que estén incluidos en un banco de datos." Y: "El responsable o usuario del banco de datos, debe proceder a la rectificación, supresión o actualización de los datos personales del afectado, realizando las operaciones necesarias a tal fin en el plazo máximo de cinco días hábiles de recibido el reclamo del titular de los datos o advertido el error o falsedad."

> Decisión D-08. El titular ejerce la mayoría de sus derechos por sí mismo desde la aplicación: exportación completa (acceso), edición (rectificación y actualización) y borrado o eliminación de la cuenta (supresión). Para los datos técnicos que el operador sí conoce se ofrece un correo de contacto con los plazos legales. `CONS-ALTA` punto 8.

**Leyenda del órgano de control (Resolución AAIP 14/2018, art. 3).** La resolución dice: "Establécese que además de la información referida en el artículo precedente deberán incluir el siguiente texto informativo: “LA AGENCIA DE ACCESO A LA INFORMACIÓN PÚBLICA, en su carácter de Órgano de Control de la Ley N° 25.326, tiene la atribución de atender las denuncias y reclamos que interpongan quienes resulten afectados en sus derechos por incumplimiento de las normas vigentes en materia de protección de datos personales”."

> Decisión D-09. La leyenda va al pie de `CONS-ALTA`, con el texto literal de la resolución.

**Consentimiento por documento para la transcripción asistida.** La transcripción es el único punto en que un documento sale del dispositivo sin cifrar. Eso cambia el tratamiento respecto de lo informado en el alta, por lo que se aplican otra vez los arts. 5 y 6 (consentimiento informado, finalidad y consecuencias) y el art. 9 (seguridad).

> Decisión D-10. Antes de cada transcripción se pide un consentimiento específico para ese documento, sin opción de "no volver a preguntar". El texto informa qué se envía, a dónde, que no se guarda copia y que el resultado es un borrador que el usuario revisa. El servicio de extracción no persiste nada, no registra contenido y no tiene salida a internet. **Texto: `CONS-EXTR` (sección 3.2).**

### 2.2 Ley 26.529 de Derechos del Paciente y Decreto 1089/2012

**Titularidad (Ley 26.529, art. 14).** La ley dice: "El paciente es el titular de la historia clínica. A su simple requerimiento debe suministrársele copia de la misma, autenticada por autoridad competente de la institución asistencial. La entrega se realizará dentro de las cuarenta y ocho (48) horas de solicitada, salvo caso de emergencia."

> Decisión D-11. Es el fundamento del producto: Custodia le da al titular un lugar donde reunir las copias que la ley le reconoce y controlarlas.

**Información a terceros solo con autorización (Ley 26.529, art. 4) y profesionales legitimados con autorización expresa (art. 19 inc. c).** El art. 4 dice: "La información sanitaria sólo podrá ser brindada a terceras personas, con autorización del paciente." El art. 19 dice: "Establécese que se encuentran legitimados para solicitar la historia clínica: [...] c) Los médicos, y otros profesionales del arte de curar, cuando cuenten con expresa autorización del paciente o de su representante legal."

> Decisión D-12. Un profesional accede únicamente a través de un acceso que el paciente le concede expresamente. No existe ninguna vía de acceso sin autorización del titular.

**Confidencialidad (Ley 26.529, art. 2 inc. d; Decreto 1089/2012, Anexo I, art. 2 inc. d).** La ley dice: "Confidencialidad. El paciente tiene derecho a que toda persona que participe en la elaboración o manipulación de la documentación clínica, o bien tenga acceso al contenido de la misma, guarde la debida reserva, salvo expresa disposición en contrario emanada de autoridad judicial competente o autorización del propio paciente". La reglamentación agrega: "El deber de confidencialidad es extensivo a toda persona que acceda a la documentación clínica, incluso a quienes actúan como aseguradores o financiadores de las prestaciones."

> Decisión D-13. Antes de ver contenido, el profesional acepta un aviso que le recuerda ese deber. Todo lo que ve lleva una marca de agua con su nombre, matrícula, fecha, hora e identificador del acceso, y cada apertura queda en la bitácora. **Texto: `AVISO-PROF` (sección 3.3).**

**Guarda por el efector (Ley 26.529, art. 18).** La ley dice: "Los establecimientos asistenciales públicos o privados y los profesionales de la salud, en su calidad de titulares de consultorios privados, tienen a su cargo su guarda y custodia, asumiendo el carácter de depositarios de aquélla [...]". Y: "La obligación impuesta en el párrafo precedente debe regir durante el plazo mínimo de DIEZ (10) años de prescripción liberatoria de la responsabilidad contractual. Dicho plazo se computa desde la última actuación registrada en la historia clínica [...]".

> Decisión D-14. Custodia no reemplaza esa obligación ni entrega copias al profesional: el visor es de solo lectura. El aviso al profesional le recuerda registrar la atención en su propio sistema.

### 2.3 Ley 27.706 de Historia Clínica Electrónica y Decreto 393/2023

Esta ley rige el Sistema Único de Registro de Historias Clínicas Electrónicas de los efectores. Custodia no es parte de ese sistema, pero adoptamos sus definiciones como estándar de diseño, porque describen lo que el Estado espera de un sistema de información clínica.

**Niveles de acceso (Ley 27.706, art. 7 inc. a).** La ley dice: "Existen por lo menos tres (3) niveles de acceso: el de consulta, el de consulta y actualización y por último el de consulta, actualización y modificación de la información, de conformidad con lo establecido en la presente ley".

> Decisión D-15. Custodia implementa los permisos "ver" (consulta) y "cargar" (actualización, sin acceso a lo existente si no se concede "ver"). Ningún profesional puede modificar ni borrar lo que ya existe; lo que carga llega como pendiente y el titular decide si lo incorpora.

**Seguridad y trazabilidad (Ley 27.706, arts. 6 inc. b y 7 incs. d y e).** El art. 6 inc. b dice: "La información clínica contenida en el Sistema Único de Registro de Historias Clínicas Electrónicas, su registro, actualización o modificación y consulta se efectúan en estrictas condiciones de seguridad, integridad, autenticidad, confiabilidad, exactitud, inteligibilidad, conservación, disponibilidad, acceso y trazabilidad". El art. 7 define: "Seguridad: preservación de la confidencialidad, integridad y disponibilidad de la información, además de otras propiedades, como autenticidad, responsabilidad, no repudio y fiabilidad". Y: "Trazabilidad: cualidad que permite que todas las acciones realizadas sobre la información y/o sistema de tratamiento de la información sean asociadas de modo inequívoco a un individuo o entidad, dejando rastro del respectivo acceso."

> Decisión D-16. Bitácora de solo inserción con encadenamiento por hash, visible y exportable por el titular. Registra identificación del profesional, apertura, cada elemento visto, cargas, cambios de vigencia, vencimiento e intentos posteriores, sin ningún dato clínico.

**Validación de profesionales (Decreto 393/2023, Anexo, art. 6 inc. c).** El decreto dice: "[...] deberá coordinar y articular con las autoridades competentes los mecanismos necesarios para la autenticación de las personas, agentes, profesionales y auxiliares de la salud que intervengan en los Sistemas de Historias Clínicas Electrónicas, tales como el REGISTRO NACIONAL DE LAS PERSONAS (RENAPER), la SUPERINTENDENCIA DE SERVICIOS DE SALUD, Colegios Profesionales o autoridades jurisdiccionales con gobierno de la matrícula profesional y otros, de corresponder. La identificación y validación de los y las profesionales de la salud, a los efectos de la utilización de la “LICENCIA SANITARIA FEDERAL” creada por el artículo 3° del Decreto N° 98 del 27 de febrero de 2023, se realizará conforme los datos de matrículas vigentes en la “Red Federal de Registros de Profesionales de la Salud” (REFEPS)."

> Decisión D-17. La identidad declarada del profesional se contrasta contra servicios que reproducen REFEPS y RENAPER (épica E8). Como esos organismos no ofrecen una interfaz abierta, durante el Trabajo Profesional los servicios son simulados y operan con datos sintéticos; la interfaz lo declara (LIM-07).

**Firma de la historia clínica (Ley 27.706, art. 8; Decreto 393/2023, Anexo, art. 8).** La ley dice que la historia clínica electrónica es el documento digital "[...] en el que constan todas las actuaciones de asistencia a la salud efectuadas por profesionales y auxiliares de la salud a cada paciente, refrendadas con la firma digital del responsable." El decreto reglamentario dice: "La Historia Clínica Electrónica podrá ser refrendada con firma digital y/o electrónica, en los términos de la Ley de Firma Digital N° 25.506 y sus modificaciones." Es decir que la ley habla de firma digital y la reglamentación admite también la electrónica. Ver 2.4.

### 2.4 Ley 25.506 de Firma Digital

La Ley 25.506 define la firma digital en su art. 2: "Se entiende por firma digital al resultado de aplicar a un documento digital un procedimiento matemático que requiere información de exclusivo conocimiento del firmante, encontrándose ésta bajo su absoluto control. La firma digital debe ser susceptible de verificación por terceras partes, tal que dicha verificación simultáneamente permita identificar al firmante y detectar cualquier alteración del documento digital posterior a su firma." Y define la firma electrónica en su art. 5: "Se entiende por firma electrónica al conjunto de datos electrónicos integrados, ligados o asociados de manera lógica a otros datos electrónicos, utilizado por el signatario como su medio de identificación, que carezca de alguno de los requisitos legales para ser considerada firma digital. En caso de ser desconocida la firma electrónica corresponde a quien la invoca acreditar su validez."

Los requisitos legales de la firma digital no se agotan en el art. 2. El art. 9 dice: "Una firma digital es válida si cumple con los siguientes requisitos: [...] c) Que dicho certificado haya sido emitido o reconocido, según el artículo 16 de la presente, por un certificador licenciado."

Son términos con efectos jurídicos propios. El art. 7 dice: "Se presume, salvo prueba en contrario, que toda firma digital pertenece al titular del certificado digital que permite la verificación de dicha firma." En cambio, para la firma electrónica rige lo que dice el art. 5: quien la invoca debe acreditar su validez.

> Decisión D-18. Lo que carga un profesional se marca como **"Realizado por"**, seguido de su nombre, matrícula, jurisdicción, estado de verificación, fecha y hora. No usamos "firma" ni "firmado" en la interfaz, en las historias de usuario ni en el informe, para no atribuirle a esa marca un valor legal que no tiene. La interfaz aclara que no equivale a una firma digital (LIM-07).

### 2.5 Disposición ANMAT 64/2025 y software como producto médico

**Qué dice la disposición.** La Disposición ANMAT 64/2025 (Boletín Oficial del 13/01/2025) dispone en su art. 1: "Incorpórase al ordenamiento jurídico nacional la Resolución GMC Nº 25/21 “Reglamento Técnico Mercosur de Registro de Productos Médicos (Derogación de la Resolución GMC N° 40/00)”, que consta en el documento IF-2024-142529439-APN-DRI#ANMAT, que como Anexo forma parte de la presente disposición." La parte que pudimos leer no define "software": esas definiciones están en su Anexo, que no pudimos leer.

**Qué dice ANMAT sobre software.** El comunicado de ANMAT del 10/09/2026 dice: "[...] debido a la incorporación de definiciones y reglas de clasificación específicas para software como productos médicos, vigentes a partir de la implementación de la Disposición ANMAT N° 64/25." Y: "Se establece que todo software cuyo uso previsto por el fabricante sea el diagnóstico, prevención, tratamiento o mitigación de una patología o afección específica, y que desempeña sus funciones sin ser parte del hardware de un producto médico, adquiere formalmente la categorización de Software como Dispositivo Médico (SaMD, por sus siglas en inglés)." Sobre las consecuencias, agrega: "[...] deberán someterse de manera obligatoria al proceso de registro y autorización sanitaria correspondiente ante esta autoridad de aplicación."

> Decisión D-19. El uso previsto de Custodia es guardar, ordenar, transcribir y compartir información. La IA transcribe los valores tal como figuran en el documento y reproduce el diagnóstico textual; no califica valores, no usa colores ni íconos que los valoren, no diagnostica y no recomienda. Ese uso previsto se declara en la bienvenida, en `CONS-EXTR` y en LIM-02.

### 2.6 Código Civil y Comercial, arts. 25 y 26 [S]

**Mayoría de edad (art. 25).** El artículo dice: "Menor de edad es la persona que no ha cumplido dieciocho años."

**Ejercicio de los derechos por la persona menor de edad (art. 26).** El artículo dice: "La persona menor de edad ejerce sus derechos a través de sus representantes legales." Y sobre las decisiones de salud: "Se presume que el adolescente entre trece y dieciséis años tiene aptitud para decidir por sí respecto de aquellos tratamientos que no resultan invasivos, ni comprometen su estado de salud o provocan un riesgo grave en su vida o integridad física." Y: "A partir de los dieciséis años el adolescente es considerado como un adulto para las decisiones atinentes al cuidado de su propio cuerpo."

> Decisión D-20. Durante el Trabajo Profesional, Custodia admite solo personas mayores de 18 años. La gestión de la información de terceros (hijos, adultos mayores a cargo) queda como trabajo futuro.

### 2.7 Código Penal, art. 156 [S]

**Código Penal, art. 156.** El artículo dice: "Será reprimido con multa de pesos mil quinientos a pesos noventa mil e inhabilitación especial, en su caso, por seis meses a tres años, el que teniendo noticia, por razón de su estado, oficio, empleo, profesión o arte, de un secreto cuya divulgación pueda causar daño, lo revelare sin justa causa."

> Decisión D-21. Sostiene el punto 4 de `AVISO-PROF` sobre el secreto profesional. No se cita el artículo en la interfaz.

### 2.8 Reforma de la Ley 25.326 [S]

Hay proyectos de reforma integral en trámite, sin sanción. Uno de ellos es el expediente 3397-D-2026, presentado el 16/07/2026 en la Cámara de Diputados. Como es un proyecto y no una norma vigente, no lo citamos textualmente: no leímos el expediente en su fuente oficial. Según los resúmenes de estudios jurídicos que lo analizan (sección 5), su art. 21 prevé notificar los incidentes de seguridad a la autoridad dentro de las 72 horas.

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
| D-20 | Solo mayores de 18 años durante el TP | Código Civil y Comercial arts. 25 y 26 |
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
- ANMAT, comunicado oficial sobre software como dispositivo médico, en el marco de la Disposición 64/2025 (10/09/2026). https://www.argentina.gob.ar/noticias/anmat-actualiza-los-criterios-regulatorios-para-software-como-dispositivo-medico-samd . Disposición en el Boletín Oficial: https://www.boletinoficial.gob.ar/detalleAviso/primera/319522/20250113
- Código Civil y Comercial de la Nación (Ley 26.994), arts. 25 y 26, tomados de reproducciones del texto vigente: https://leyes-ar.com/codigo_civil_y_comercial/26.htm , https://leyes-ar.com/download.php?id=3832 y https://www.rpba.gob.ar/files/Normas/Leyes/CCCN0026.pdf
- Código Penal, art. 156, tomado de una reproducción del texto vigente: https://leyes-ar.com/codigo_penal/156.htm
- Proyecto de ley 3397-D-2026, según resúmenes de estudios jurídicos (no se leyó el expediente en la fuente oficial): https://abogados.com.ar/nuevo-proyecto-de-ley-de-proteccion-de-datos-personales/39762 y https://allende.com/privacidad-y-ciberseguridad/se-reintroduce-en-el-congreso-el-proyecto-de-reforma-integral-del-regimen-argentino-de-proteccion-de-datos-personales-08-12-2026/