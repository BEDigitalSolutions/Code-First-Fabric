# Aviso de privacidad: telemetría de Code First Fabric

**Última actualización**: 04/08/2026

Code First Fabric (`cff`) recopila datos de uso seudónimos ("telemetría") para ayudarnos a mejorar el producto. Este aviso explica qué recopilamos, por qué y cómo desactivarlo. La telemetría está **activada por defecto**, pero la primera ejecución del CLI muestra este aviso y **no envía ningún dato**, de modo que puedes desactivarla antes de que se recopile nada.

## Cómo desactivar la telemetría

Este comando la desactiva de forma persistente:

```text
cff telemetry disable
```

También puedes desactivarla mientras permanezca definida cualquiera de estas variables de entorno:

```text
CFF_TELEMETRY_DISABLED=1
DO_NOT_TRACK=1
```

Puedes comprobar el estado en cualquier momento con `cff telemetry status` y ver exactamente qué identificadores genera tu instalación con `cff telemetry identity`. Los builds compilados desde el código fuente tienen la telemetría desactivada por defecto.

## Responsable del tratamiento

- **Responsable**: Consultores Tecnologías Digitales, SL
- **NIF** : B67009696
- **Contacto**: info@bdigitalsolutions.com
- **Dirección**:
Carrer París, 209, 3 2
08008 Barcelona
Spain

## Qué datos recopilamos

Cuando ejecutas un comando reconocido de `cff`, el CLI envía un único evento con estos campos:

| Campo | Contenido | Ejemplo |
|---|---|---|
| `eventId` | Identificador aleatorio único de este evento | `uuid` |
| `installationId` | Identificador aleatorio de la instalación, generado localmente la primera vez | `uuid` |
| `userHash` | Huella seudónima de tu cuenta: hash SHA-256 del identificador de tenant y de objeto de tu sesión de Azure. No contiene ni permite obtener directamente tu nombre, correo ni identidad | `a3f1…` o vacío |
| `principalType` | Si la sesión es de un usuario, un service principal o desconocida | `user` |
| `command` | El nombre del comando ejecutado, **sin argumentos ni contenido** | `sql run query` |
| `invocationType` | Si fue una ejecución o una consulta de ayuda | `execute` |
| `productVersion` | Versión del ejecutable | `2026.07.20` |
| `clientMode` | Tipo de distribución | `standalone-exe` |
| `origin` | Si el comando vino del terminal o de un proceso interno de `cff view` | `terminal` |
| `workspaceIds` | Identificadores GUID de los workspaces de Fabric implicados, **nunca sus nombres ni descripciones** | `["guid"]` |

Al recibir el evento, nuestro servidor añade dos campos:

- `receivedAtUtc`: fecha y hora de recepción.
- `country`: código de país de dos letras (por ejemplo `ES`), derivado de la dirección de origen de tu conexión en el momento de la recepción. **Esa dirección se utiliza únicamente de forma transitoria en memoria para obtener el código de país y se descarta de inmediato: no se escribe en nuestra base de datos ni en ningún registro, y no se emplea para ninguna otra finalidad.** El país es un dato **aproximado**, se usa solo para estadísticas agregadas y nunca para tomar decisiones sobre ti; si la dirección de origen no está disponible o no puede resolverse, el campo queda vacío. No recopilamos ciudad, región ni ninguna ubicación más precisa que el país. Nuestro control antiabuso funciona de forma agregada y **no utiliza tu dirección**.

## Qué datos no envía el CLI ni almacena el servicio

Los siguientes datos no forman parte del evento ni se guardan en la base de datos de telemetría:

- Tu nombre, correo electrónico ni ningún identificador humano directo.
- Tokens de acceso ni credenciales de ningún tipo.
- Los identificadores originales de tenant u objeto (solo su hash).
- Argumentos de comandos, consultas SQL, código ni contenido de notebooks.
- Rutas de archivos locales o remotas, variables de entorno, stdout, stderr ni mensajes de error de tus comandos.
- Nombres o descripciones de workspaces.
- Nombre de equipo, usuario local ni identificadores de hardware.
- Tu dirección IP no se almacena: solo se procesa de forma transitoria en memoria para derivar el código de país y se descarta acto seguido; no se escribe en la base de datos ni en ningún registro, no se usa para el control antiabuso y no se conserva de ninguna forma, ni siquiera derivada.

## Registros técnicos

El servicio no ingiere registros de aplicación: no se recogen mensajes, trazas, detalles de excepción, identificadores de invocación ni ningún otro registro generado por el código que procesa tu evento. La aplicación no escribe en ningún registro el cuerpo de la petición, las cabeceras, tu dirección IP, el país ni los campos del evento de uso.

Microsoft Azure genera, como parte del funcionamiento de su plataforma, métricas operativas agregadas del servicio, por ejemplo recuentos de ejecución o estado de disponibilidad. Esas métricas no contienen datos de tu evento ni identificadores tuyos, y se conservan conforme a las condiciones de la propia plataforma.

## Finalidad

Usamos estos datos exclusivamente para:

- saber cuántas personas e instalaciones usan Code First Fabric y en qué países, de forma agregada;
- saber qué comandos y versiones se usan, para priorizar mejoras y decidir cuándo retirar versiones antiguas;
- dimensionar el proyecto y detectar problemas de adopción.

**No** usamos estos datos para publicidad, para venderlos o cederlos a terceros, para autorización o facturación, ni para vigilar o evaluar a personas concretas o su desempeño laboral. Las métricas son aproximadas por diseño y se tratan siempre como tales.

## Base jurídica

Tratamos estos datos sobre la base de nuestro **interés legítimo** (art. 6.1.f RGPD) en comprender y mejorar el uso del producto, tras evaluar que el impacto sobre los usuarios es mínimo: los datos son seudónimos, de bajo volumen, sin contenido de trabajo, con retención corta y con un mecanismo de oposición inmediato y gratuito (la desactivación descrita arriba). Puedes oponerte al tratamiento en cualquier momento desactivando la telemetría o escribiéndonos.

Iniciar sesión con `az login` es un mecanismo de autenticación de Azure ajeno a este proyecto y **no constituye consentimiento** a esta telemetría.

## Seudonimización, no anonimización

El campo `userHash` es un dato **seudónimo, no anónimo**: quien conozca tu tenant ID y object ID podría recalcular el hash y correlacionarlo. Por eso lo tratamos como dato personal a todos los efectos, con acceso restringido y las garantías descritas en este aviso.

## Dónde se almacenan los datos y quién los trata

Los datos de telemetría se almacenan en **Microsoft Azure, región West Europe (Unión Europea)**. Microsoft actúa como encargado del tratamiento conforme a sus condiciones de servicios en línea.

El tráfico entre tu equipo y nuestro servidor se envía directamente a la URL nativa de la Function App en `azurewebsites.net`, cifrado con TLS gestionado por Microsoft, a nuestro servicio alojado en Microsoft Azure, región West Europe. No intervienen otros encargados intermedios ni se realizan transferencias internacionales fuera del Espacio Económico Europeo como parte del funcionamiento normal del servicio. Si en el futuro incorporamos una red de distribución, gateway o servicio de protección delante del endpoint, actualizaremos este aviso antes de aplicar el cambio.

La resolución del código de país se realiza dentro de nuestro propio servicio, con una base de datos local incluida en el despliegue. No se consulta ningún servicio externo de geolocalización ni se comunica tu dirección a ningún tercero.

## Retención

- **Eventos de telemetría**: se eliminan automáticamente a los **90 días** como máximo (la purga se ejecuta con corte a 89 días).
- **Copias de seguridad**: la base de datos mantiene copias de recuperación durante **7 días adicionales**, por lo que un dato borrado puede persistir en backups hasta ese plazo antes de desaparecer definitivamente.
- **Direcciones de origen**: no se conservan; se descartan en memoria tras derivar el código de país.
- **Registros de aplicación**: no existen, según se describe en el apartado de registros técnicos.

## Tus derechos

Tienes derecho a acceder a tus datos, a que los borremos y a oponerte al tratamiento. Para ejercerlos, escribe a info@bdigitalsolutions.com. Como no conocemos tu identidad real, para localizar tus datos necesitarás indicarnos tu `userHash` o `installationId`, que puedes obtener con:

```text
cff telemetry identity
```

Ten en cuenta que necesitaremos una verificación razonable y proporcionada de que esos identificadores te corresponden; conocer un hash no acredita por sí solo la titularidad. También tienes derecho a presentar una reclamación ante la autoridad de control competente; en España, la Agencia Española de Protección de Datos (www.aepd.es).

## Cambios en este aviso

Si cambiamos qué datos se recopilan o con qué finalidad, actualizaremos este aviso y la fecha de cabecera antes de aplicar el cambio, y lo señalaremos en las notas de la versión correspondiente del CLI.
