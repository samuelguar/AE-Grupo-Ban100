# 📄 Informe Técnico del Taller

## Nombre del Taller
_Taller 4 - Infraestructura: Mapa Híbrido AS-IS, diagnóstico de riesgos y modelo matemático MRAE del plazo B2G_

## Integrantes del equipo
- Santiago Barrera Rueda
- Krish Purmessur Moros
- Samuel Guerrero Arcos 

**Equipo:** Ban100 — Grupo de Arquitectura Empresarial · **Cliente:** Ban100 S.A.

## Descripción general del trabajo
Se representó la infraestructura **híbrida AS-IS** de la plataforma digital de libranza (nube pública Kubernetes, centro de datos On-Premise en Bogotá, SOC 24/7 y conectividad con pagadurías), se marcaron en rojo `⚠️` los tres riesgos diagnosticados y se incorporó el **modelo matemático del MinTIC** (`MRAE.ADM.01`) para estimar el plazo de adopción de las contrapartes B2G.

## Proceso de desarrollo
1. **Componentes** de cinco zonas: clientes y canales, borde y seguridad, nube pública, centro de datos On-Premise y ecosistema externo B2G.
2. **Agrupación** por zona (contenedores punteados): *Zona 1: Clientes y Canales (965–1.000+ Municipios)*, *Zona 2: Borde y Seguridad (WAF / Balanceador / SOC 24/7)*, *Zona 3: Nube Pública (Clúster Kubernetes — Servicios Digitales)*, *Zona 4: Centro de Datos On-Premise Bogotá (Core Bancario y MDM)* y *Zona 5: Ecosistema Externo B2G (Pagadurías G1-G5 y Proveedores)*.
3. **Conexiones** con el protocolo de cada enlace y dirección del tráfico.
4. **Redundancia** indicada en cada componente (`Instancia única` o `Cluster HA Activo-Pasivo`).
5. **Diagnóstico** de tres riesgos (rojo `#c0392b` con `⚠️`) clasificados por categoría.

## Análisis del modelo propuesto
### Diagnóstico de riesgos
| Componente | Riesgo diagnosticado | Categoría | Impacto si ocurre | Prioridad |
|---|---|---|---|---|
| **R1** ⚠️ Conector de Pagadurías Territoriales | Acoplamiento síncrono frente a 850–880 municipios en Grupos MRAE 3, 4 y 5 (puntaje de arquitectura 40,5–56,3) | Rendimiento / Escalabilidad | La visación depende de la pagaduría más lenta; se pierde la meta de < 15 min y se acumulan solicitudes desistidas por falta de cupo | Alta |
| **R2** ⚠️ Enlace síncrono μS Originación ↔ Core Bancario On-Premise | Ventana de mantenimiento y cuello de botella transaccional | Disponibilidad / Rendimiento | Una caída o ventana del Core detiene la originación digital 100 % en línea | Alta |
| **R3** ⚠️ Borde público IPv4 sin Dual-Stack IPv6 completo | Brecha frente a `MGGTI.LI.ST.14` (5,85 % del esfuerzo MRAE: 54 h a 414,4 h) | Escalabilidad / Interoperabilidad estatal | Imposibilidad de interoperar con entidades públicas que adopten IPv6 y hallazgo de conformidad | Media |

### Redundancia declarada (supuestos del equipo por documentación pública y arquitectura AS-IS)
| Componente | Redundancia |
|---|---|
| WAF y Balanceador de Carga | Cluster HA Activo-Pasivo |
| API Gateway [Kong] | Cluster HA Activo-Pasivo |
| μS Originación / Ban-I Bot (Kubernetes) | Réplicas K8s (Cluster HA) |
| Core Bancario Transaccional | Activo-Pasivo con DRP |
| Cliente 360 MDM | **Instancia única** (On-Premise) |
| Oficinas físicas (10) | **Instancia única** por oficina |

## Diagrama final entregado
[Ver mapa de infraestructura AS-IS en draw.io](./mapa-final.drawio)

## Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| WAF y Balanceador de Carga | Dispositivo / Nodo | Borde público de todos los canales | Infraestructura |
| SOC 24/7 | Nodo | Monitoreo y ciberseguridad continuos | Seguridad |
| API Gateway [Kong] | Nodo | Enrutamiento TLS 1.3 | Infraestructura |
| Clúster Kubernetes | Nodo | Aloja Ban-I Bot, Módulo de Pagos y μS Originación | Plataforma |
| Core Bancario / Cliente 360 MDM | Nodo On-Premise | Sistemas centrales en Bogotá | TI |
| Pagadurías G1–G2 / G3–G5 | Externo | Contraparte B2G con integración estandarizable o asíncrona | Convenios B2G |

## Investigación complementaria
### Tema investigado:
Modelo MinTIC de plazos por grupo de entidades (`MRAE.ADM.01`) y su implicación B2G para Ban100.

### Resumen:
El MinTIC agrupó las entidades públicas por similitud estructural con **K-means** sobre los **1.101 municipios** (minimizando la varianza intraclúster) y eligió el número de clústeres con el **índice de Dunn**.

**1. Agrupamiento K-means.**
$$V_{C_K} = \sum_{i=1}^{m} \left(x_i^k - \mu_k\right)^2$$

**2. Selección de $K$.** Sobre seis variables (población DANE, ingresos DNP, % de hogares con internet MinTIC, Índice de Desempeño Institucional DAFP, densidad por km² DANE e Índice de Desempeño Fiscal DNP) el índice de Dunn alcanza su máximo global en **$K = 3$** ($DI_3 \approx 0{,}040$, esto es, ≈ 0,040): **Clúster 1 Avanzado (124 municipios)**, **Clúster 2 Intermedio (416)** y **Clúster 3 Básico (561)**.
$$DI_K = \min_{1 \le i \le K} \left\{ \min_{1 \le j \le K,\ j \ne i} \left\{ \frac{\delta(X_i, X_j)}{\max_{1 \le k \le K} \Delta(X_k)} \right\} \right\}$$

**3. Índice sintético e interpolación del esfuerzo.** Entre el escenario optimista ($t_l = 27$ meses $= 2.271$ h al 50 % de dedicación, jornadas de 8 h por 22 días hábiles al mes) y el pesimista ($t_h = 67$ meses $= 5.734$ h):
$$S_g = \frac{1}{N_g K} \sum_{n=1}^{N_g} \sum_{k=1}^{K} \left( \frac{V_{n,k} - V_{k\min}}{V_{k\max} - V_{k\min}} \right), \qquad t_g = \left( 1 - \frac{S_g - S_{\min}}{S_{\max} - S_{\min}} \right)(t_h - t_l) + t_l$$

**4. Plazo real con aprendizaje tecnológico.** Para una tasa de aprendizaje $r_g$ se cumple $t_g = P_g (r_g + 1)^{P_g}$; derivando implícitamente se obtiene la ecuación diferencial que se integra numéricamente con **Runge-Kutta de 4.º orden (RK4)**:
$$\frac{dP_g}{dt_g} = \frac{1}{(r_g + 1)^{P_g} \left( \ln(r_g + 1)\, P_g + 1 \right)}$$

RK4 avanza con $k_1 = f(t, P)$, $k_2 = f(t + h/2,\ P + hk_1/2)$, $k_3 = f(t + h/2,\ P + hk_2/2)$, $k_4 = f(t + h,\ P + hk_3)$ y $P_{n+1} = P_n + \tfrac{h}{6}(k_1 + 2k_2 + 2k_3 + k_4)$. Los valores de $r_g$ y $S_g$ por grupo corresponden al modelo oficial del MinTIC y no se reproducen aquí; se usan sus plazos publicados.

**5. Segmentación oficial** (179 entidades nacionales en 3 grupos y 3.428 territoriales en 5 grupos; hoja `Plazos_mrae` de `articles-204807_recurso_5.xlsx`, plazos al 40 % / 70 % / 100 %) e **implicación B2G para Ban100**:

| Grupo | Entidades | Composición | Métrica | Plazos (meses) | Implicación B2G para Ban100 |
|---|---:|---|---|---|---|
| Nacional G1 | 37 | Ministerios, Deptos. Administrativos, UAE sin personería | Trámites 87,8 | 10 / 17 / 23 | Interoperabilidad estándar X-Road / Lenguaje Común para nóminas centrales |
| Nacional G2 | 44 | Superintendencias con personería (SFC, DIAN, UPIT) | Trámites 85,2 | 11 / 18 / 25 | Reportes ágiles de supervisión SFC y validación tributaria/identidad |
| Nacional G3 | 98 | Establecimientos Públicos, EICE, Soc. de Economía Mixta (FDN, Fiducoldex) | Trámites 81,0 | 12 / 20 / 27 | Homologación de APIs en fondos y pagadurías nacionales descentralizadas |
| Territorial G1 | 250 | Distrito Capital, 32 Gobernaciones (incl. Caquetá), Alcaldías Clúster 1 (124) e Instituciones Universitarias | Subíndice Arq. 77,9 | 13 / 21 / 29 | Núcleo primario de pagadurías territoriales apto para Web Services / APIs REST (~2,4 años) |
| Territorial G2 | 418 | Áreas Metropolitanas, Establecimientos Públicos y ESE Departamentales, Soc. de Economía Mixta | Subíndice Arq. 63,1 | 17 / 28 / 36 | Núcleo descentralizado intermedio (hasta 3 años) |
| Territorial G3 | 1.573 (45,9 %) | Alcaldías Clúster 2 (416) y Clúster 3 (561), IPS/UAE Salud, ESP Oficiales Avanzadas | Subíndice Arq. 56,3 | 19 / 30 / 40 | **Cuello de botella de capilaridad:** Ban100 opera en 850 a 880 municipios |
| Territorial G4 | 657 | ESE Municipales y Departamentales, EICE Básicas | Subíndice Arq. 51,4 | 20 / 32 / 42 | Alta fragmentación de nómina en hospitales públicos regionales |
| Territorial G5 | 530 | ESP Domiciliarios Oficiales, Establecimientos Públicos, Asociaciones de Municipios | Subíndice Arq. 40,5 | 23 / 36 / 47 | **Rezago crítico de TI** (~4 años); sin integración API directa en el corto plazo |

**Lectura para el diagnóstico.** Los riesgos R1 y R2 se derivan de esta tabla: los Grupos Territoriales 3, 4 y 5 concentran la mayor parte de los municipios donde Ban100 opera y tienen plazos de 40 a 47 meses para alcanzar el 100 % de los lineamientos, por lo que el diseño no puede asumir APIs en la contraparte. Esto sustenta el **Desacoplamiento Asimétrico B2G de Dos Velocidades** del Taller 7.

### Homologación MRAE v3.0 del taller
`MAE.LI.AT.01` (catálogo de infraestructura), `AT.02` (conectores de interoperabilidad), `AT.03` (diagrama de despliegue con continuidad y disponibilidad) y `AT.04` (arquitecturas de referencia tecnológica, nuevo en v3.0); `MGGTI.LI.ST.03` (nube como primera opción), `ST.05` (alta disponibilidad, 2,65 % = 33 h a 179,2 h), `ST.09` (mantenimiento preventivo y evolutivo), `ST.11` (respaldo y recuperación) y `ST.14` (implementación de IPv6, 5,85 % del total del MRAE). Las ventanas de mantenimiento acotadas a 30 minutos nocturnos cumplen `ST.05` y `ST.09`.

### Vista ArchiMate equivalente
Zona = Node (agrupación); componente = Node / Device; riesgo = Gap en el Taller 7 (R1 → Gap 1, R2 → Gap 2, R3 → Gap 3).

## Referencias
Ver [`referencias.md`](./referencias.md).

---

_Este documento hace parte de la entrega del taller 4 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
