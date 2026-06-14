# PS-P4 — UQ·CivicVote | Blockchain-Enhanced Electronic Voting System
### DD281 Programación Segura · Universidad Autónoma del Perú · 2026-1 · UQ AI SOLUTION COMPANY SAC

[![Grupo](https://img.shields.io/badge/Grupo-G4-blue?style=for-the-badge)]()
[![Stack](https://img.shields.io/badge/Stack-Python%20%7C%20Flask%20%7C%20Blockchain-orange?style=for-the-badge)]()
[![Journal](https://img.shields.io/badge/Target-Future_Gen_Computer_Systems_Q1-red?style=for-the-badge)]()
[![Demo](https://img.shields.io/badge/Demo-civicvote.uqaisolutions.com.pe-green?style=for-the-badge)]()

---

## 🏆 Los 5 Títulos Scopus Q1 del Curso DD281-2026-1

> Todos los grupos del curso publican su investigación en journals Scopus Q1 al término del ciclo.
> El docente es coautor y guía el proceso de publicación.

| Grupo | Proyecto | Título Scopus Q1 Optimizado | Journal Target | Q |
|:---:|---|---|---|:---:|
| G1 | UQ·SecureID | "Zero-Trust Behavioral Authentication: A Machine Learning-Enhanced Identity Verification Framework with Anomaly Detection for Continuous User Authentication in Cloud-Native Web Applications" | Computers & Security — Elsevier | Q1 |
| G2 | UQ·FinSecure | "SecureFinAPI: A Hybrid Machine Learning and Rule-Based Fraud Detection System for RESTful Banking APIs Compliant with OWASP API Security Top 10" | J. Information Security & Applications — Elsevier | Q1 |
| G3 | UQ·HealthShield | "PrivacyShield: An End-to-End Encrypted Electronic Health Record System with Attribute-Based Access Control for HIPAA and Ley N°29733 Compliance" | J. Biomedical Informatics — Elsevier | Q1 |
| **G4** | **UQ·CivicVote** | **"CryptoVote: A Blockchain-Enhanced Electronic Voting Protocol with Zero-Knowledge Proof Verification for Tamper-Resistant and Privacy-Preserving Democratic Processes"** | **Future Generation Computer Systems — Elsevier** | **Q1** |
| G5 | UQ·AuditAI | "AutoPenTest-AI: An Artificial Intelligence-Driven Automated Web Penetration Testing Framework with Natural Language Vulnerability Reporting Based on OWASP Top 10" | IEEE Access — IEEE | Q1 |

---

## 📄 Tu Proyecto: G4 — UQ·CivicVote

### Título Scopus Q1 Optimizado

> **"CryptoVote: A Blockchain-Enhanced Electronic Voting Protocol with Zero-Knowledge Proof Verification for Tamper-Resistant and Privacy-Preserving Democratic Processes"**
>
> 🎯 **Journal:** Future Generation Computer Systems — Elsevier — **Q1** — Impact Factor: 7.3
> 🔗 **Verificar cuartil:** https://www.scimagojr.com/journalsearch.php?q=Future+Generation+Computer+Systems

---

### ❗ Problema que Resuelve

La votación digital tiene tres propiedades que parecen contradictorias entre sí:
1. **Anonimato**: nadie debe saber por quién votó una persona
2. **Verificabilidad**: cada votante debe poder verificar que su voto fue contado
3. **Integridad**: nadie puede alterar, añadir ni eliminar votos

Los sistemas tradicionales fallan porque:
- **Bases de datos centralizadas**: una sola entidad controla todos los votos — se puede alterar
- **Sin verificabilidad**: el votante no tiene prueba de que su voto existe
- **Sin anonimato criptográfico**: los logs revelan quién votó qué

**UQ·CivicVote** resuelve esto con:
- Blockchain de encadenamiento SHA-256: alterar un voto invalida todos los bloques siguientes
- RSA 2048-bit para firmar el voto: el servidor nunca sabe el contenido, solo la firma
- Anonimización con HMAC-SHA256 del voter_id: verificar unicidad sin revelar identidad
- Proof of Work simplificado: agregar votos requiere trabajo computacional

---

### 🎯 Objetivo del Proyecto

**Objetivo General:**
Diseñar e implementar un sistema de votación electrónica que garantice las cinco propiedades fundamentales (unicidad, anonimato, integridad, verificabilidad y auditabilidad) mediante una blockchain personalizada con algoritmo SHA-256 y protocolo de firma RSA 2048-bit, aplicable a elecciones universitarias, municipales y corporativas de UQ AI SOLUTION COMPANY SAC.

**Objetivos Específicos:**
1. Implementar la blockchain con encadenamiento SHA-256 y Proof of Work (difficulty=2)
2. Diseñar el protocolo criptográfico de votación con RSA 2048-bit (firma del voto)
3. Construir el sistema de verificación pública anónima (cualquiera puede verificar sin ver el voto)
4. Prevenir el doble voto a nivel de blockchain y base de datos (constraint UNIQUE + verificación en cadena)
5. Desplegar en Azure App Services bajo `civicvote.uqaisolutions.com.pe`

---

## 📅 Plan de Desarrollo por Semanas (8 Semanas)

### Visión general

```
S1 → Diseño del protocolo criptográfico de votación
S2 → Blockchain: VoteBlock + hash encadenado
S3 → Protocolo de votación RSA + prevención doble voto
S4 ★ EP: Exposición 60%
S5 → Verificación pública + panel de auditoría
S6 → Azure Deploy + persistencia blockchain
S7 → Simulación de elección real + pentest G5
S8 ★ EF: Presentación Final 100%
```

---

### SEMANA 1 — Diseño del Protocolo Criptográfico

**Objetivo:** Entender y documentar el protocolo antes de implementarlo. Los errores de diseño en criptografía son irreparables.

**Tareas del equipo:**
- [ ] Hacer fork del repositorio: `https://github.com/RubenCarty/PS-P4-SecureVoting-System`
- [ ] Configurar Flask + cryptography + pytest
- [ ] Estudiar y documentar el protocolo de votación:
  ```
  REGISTRO → EMISION → BLOCKCHAIN → VERIFICACION → CONTEO
  ```
- [ ] Definir las 5 propiedades de seguridad y cómo se garantiza cada una
- [ ] Análisis de amenazas específico de votación (adversario activo vs. pasivo)
- [ ] Documentar en `docs/semana-01/protocolo_criptografico.md`
- [ ] Diseñar el modelo de datos: Election, Candidate, VoterKey, Ballot

**Branch a crear:**
```bash
git checkout -b feature/S1-ApellidoNombre-protocolo-diseno
```

---

### SEMANA 2 — Implementación de la Blockchain

**Objetivo:** Cadena de bloques funcional que puede detectar cualquier alteración.

**Tareas del equipo:**
- [ ] Implementar `app/blockchain/block.py` — `VoteBlock` con `calculate_hash()`
- [ ] Implementar `app/blockchain/proof_of_work.py` — Proof of Work (difficulty=2)
- [ ] Implementar `app/blockchain/chain.py` — `VotingBlockchain`:
  - `add_vote(vote_hash, voter_id_hash, election_id)` → nuevo bloque minado
  - `is_chain_valid()` → verifica integridad completa
  - `verify_voter_participation()` → prevención doble voto
- [ ] Implementar `app/blockchain/validator.py` — validación externa de la cadena
- [ ] Tests: bloque génesis, agregar voto, cadena válida, cadena alterada detectada, doble voto

**Branch a crear:**
```bash
git checkout -b feature/S2-ApellidoNombre-blockchain-core
```

**Tests obligatorios:**
```python
def test_tampered_chain_is_invalid():  # Alterar bloque → cadena inválida
def test_double_vote_prevention():     # Mismo voter_hash → bloqueado
def test_proof_of_work_valid():        # Hash empieza con '00'
```

---

### SEMANA 3 — Protocolo RSA + Prevención Doble Voto

**Objetivo:** El votante firma su voto con su clave privada — el servidor nunca sabe por quién votó.

**Tareas del equipo:**
- [ ] Implementar `app/voting/ballot_crypto.py`:
  - `generate_voter_keypair()` → RSA 2048-bit (privada: al votante, pública: al servidor)
  - `sign_vote(candidate_id, private_key_pem)` → firma RSA-PSS
  - `verify_vote_signature(signature, vote_data, public_key_pem)` → verificación
  - `hash_vote_for_blockchain(signature)` → SHA256(firma) para la cadena
  - `anonymize_voter_id(voter_id, election_salt)` → HMAC-SHA256
- [ ] Implementar `app/voting/routes.py`:
  - `/election/{id}/register` → genera keypair, guarda pública, entrega privada una vez
  - `/election/{id}/vote` → verifica firma + blockchain + BD, emite voto
  - `/election/{id}/receipt` → comprobante del voto (solo una vez)
- [ ] Prevención de doble voto: verificar en BD (has_voted) + blockchain + constraint UNIQUE

**Branch a crear:**
```bash
git checkout -b feature/S3-ApellidoNombre-rsa-protocolo-voto
```

---

### SEMANA 4 ★ — EP: EVALUACIÓN PARCIAL (60% del proyecto)

**Entregables OBLIGATORIOS:**
1. **Pull Request** con avances S1–S4 integrados en `main`
2. **Demo en vivo** (15 minutos):
   - Crear una elección con 3 candidatos
   - Registrar 2 votantes → descargar clave privada RSA
   - Emitir 2 votos (cada votante con su clave privada)
   - Mostrar cadena pública `/public/chain` → bloques visibles
   - Intentar doble voto → debe ser rechazado
   - **Prueba de alteración**: modificar `vote_hash` de un bloque → `is_chain_valid()` retorna False
3. **Tests corriendo** en CI/CD

**Branch a crear:**
```bash
git checkout -b release/EP-S4-NombreGrupo
```

**Rúbrica EP (100 puntos):**
| Criterio | Puntos |
|---|:---:|
| Blockchain funcional (add + validate + detect tampering) | 30 |
| RSA para firma del voto (keypair + sign + verify) | 25 |
| Prevención de doble voto (blockchain + BD) | 20 |
| Vista pública de auditoría de la cadena | 10 |
| Tests con cobertura ≥ 60% | 15 |

---

### SEMANA 5 — Verificación Pública + Panel de Auditoría

**Objetivo:** Cualquier ciudadano puede verificar la integridad de la elección sin ver los votos.

**Tareas del equipo:**
- [ ] Endpoint público `/public/chain/{election_id}` — cadena completa sin información privada
- [ ] Herramienta de verificación: el votante puede verificar que su `block_hash` está en la cadena
- [ ] Panel de auditoría `/admin/elections/{id}/audit` — solo rol admin/auditor
- [ ] Estadísticas públicas: total de bloques, hash del último bloque, `is_valid`
- [ ] Resultados post-cierre: descifrar y contar votos (solo cuando `status='tallied'`)
- [ ] Exportar cadena en JSON para auditoría externa

**Branch a crear:**
```bash
git checkout -b feature/S5-ApellidoNombre-verificacion-publica
```

---

### SEMANA 6 — Azure Deploy + Persistencia de la Blockchain

**Objetivo:** App en `civicvote.uqaisolutions.com.pe` con blockchain persistida entre reinicios.

**Tareas del equipo:**
- [ ] Serializar/deserializar la blockchain a Azure SQL Database o Azure Table Storage
- [ ] Cargar blockchain desde BD al iniciar la app (`_blockchain = load_from_db()`)
- [ ] Crear Azure App Service (Python 3.11, westus3)
- [ ] Configurar HTTPS (SSL obligatorio — sistema de votación)
- [ ] CI/CD: tests → security scan → deploy
- [ ] Rate limiting en rutas de registro y votación (máx 3/hora por usuario)

**Branch a crear:**
```bash
git checkout -b feature/S6-ApellidoNombre-azure-persistencia
```

---

### SEMANA 7 — Simulación de Elección Real + PenTest G5

**Objetivo:** Simulación completa de una elección universitaria + análisis de seguridad externo.

**Tareas del equipo:**
- [ ] Simular elección estudiantil: 50 votantes ficticios (Faker), 3 candidatos, 2 horas
- [ ] Medir throughput: votos por segundo que puede procesar la blockchain
- [ ] Solicitar escaneo a G5 (AuditAI) sobre `civicvote.uqaisolutions.com.pe`
- [ ] Corregir hallazgos del reporte G5
- [ ] Documentar métricas para el paper: tiempo de minado por bloque, TPS, latencia de verificación

**Branch a crear:**
```bash
git checkout -b feature/S7-ApellidoNombre-simulacion-metricas
```

---

### SEMANA 8 ★ — EF: EVALUACIÓN FINAL (Proyecto 100%)

**Rúbrica EF (100 puntos):**
| Criterio | Puntos |
|---|:---:|
| Sistema completo desplegado en Azure | 25 |
| Blockchain con integridad verificable + métricas | 25 |
| Protocolo RSA completo (keypair + sign + verify + anon) | 20 |
| Verificación pública + panel de auditoría | 15 |
| Borrador paper Scopus Q1 | 10 |
| Presentación y defensa técnica | 5 |

---

## 🔧 Flujo de Trabajo GitHub (Obligatorio)

### 1. Fork del repositorio
```
GitHub → https://github.com/RubenCarty/PS-P4-SecureVoting-System → Fork
```

### 2. Configurar fork localmente
```bash
git clone https://github.com/TU-USUARIO/PS-P4-SecureVoting-System.git
cd PS-P4-SecureVoting-System
git remote add upstream https://github.com/RubenCarty/PS-P4-SecureVoting-System.git
git fetch upstream
```

### 3. Flujo semanal
```bash
git checkout main && git pull upstream main && git push origin main
git checkout -b feature/S2-ChavezLuis-blockchain-core
# trabajar...
git add app/blockchain/
git commit -m "feat(S2): implement VoteBlock with SHA-256 chaining and Proof of Work"
git push origin feature/S2-ChavezLuis-blockchain-core
# → PR hacia RubenCarty/PS-P4-SecureVoting-System:main
```

---

## 📚 Repositorios de Referencia

### Blockchain Educativo con Python
| Repositorio | Qué aprender |
|---|---|
| [dvf/blockchain](https://github.com/dvf/blockchain) | Blockchain mínima en Python — base para entender el concepto |
| [Savjee/SavjeeCoin](https://github.com/Savjee/SavjeeCoin) | Blockchain en JavaScript — lógica fácil de trasladar a Python |
| [topics/blockchain-python](https://github.com/topics/blockchain-python) | Proyectos blockchain en Python para referencia |

### Sistemas de Votación Electrónica
| Repositorio | Qué aprender |
|---|---|
| [ADAC-aisec/e-voting](https://github.com/topics/electronic-voting) | Proyectos de e-voting académicos |
| [belenios/belenios](https://github.com/belenios/belenios) | Sistema de votación con verificabilidad criptográfica (OCaml — ver el paper) |

### Criptografía RSA en Python
| Repositorio | Qué aprender |
|---|---|
| [pyca/cryptography](https://github.com/pyca/cryptography) | RSA key generation, RSA-PSS signing, key serialization |
| [Legrandin/pycryptodome](https://github.com/Legrandin/pycryptodome) | Alternativa — ejemplos de RSA y hashing |

### Seguridad en Sistemas de Votación (Papers y Referencias)
| Recurso | Qué estudiar |
|---|---|
| [OWASP Voting Guidelines](https://owasp.org/www-pdf-archive/OWASP_Voting_Requirements_v0.2.pdf) | Requisitos de seguridad para sistemas de votación |
| [Helios Voting](https://vote.heliosvoting.org/) | Sistema de votación con verificabilidad — referencia académica |

---

## 🏗️ Estructura Completa del Proyecto

```
PS-P4-SecureVoting-System/
│
├── 📄 README.md
├── 📄 CONTRIBUTING.md
├── 📄 requirements.txt
├── 📄 .env.example
├── 📄 app.py                            ← Entry point Flask
│
├── 📁 .github/
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── workflows/
│       ├── ci.yml
│       └── azure-deploy.yml
│
├── 📁 app/
│   ├── __init__.py
│   ├── extensions.py
│   │
│   ├── 📁 blockchain/                   ← NÚCLEO DEL PROYECTO
│   │   ├── block.py                     ← VoteBlock con calculate_hash()
│   │   ├── chain.py                     ← VotingBlockchain: add/validate
│   │   ├── proof_of_work.py             ← PoW: encontrar nonce válido
│   │   └── validator.py                 ← Validación externa
│   │
│   ├── 📁 voting/                       ← Protocolo de votación
│   │   ├── ballot_crypto.py             ← RSA keypair + sign + verify + anonymize
│   │   ├── models.py                    ← Election, Candidate, Ballot, VoterKey
│   │   └── routes.py                    ← /register /vote /receipt
│   │
│   ├── 📁 elections/
│   │   ├── models.py
│   │   └── routes.py                    ← Crear/gestionar elecciones
│   │
│   ├── 📁 results/
│   │   ├── counter.py                   ← Conteo al cierre
│   │   └── routes.py                    ← /public/chain /admin/audit
│   │
│   └── 📁 auth/
│       └── routes.py                    ← Login via G1 OAuth (S7)
│
├── 📁 templates/
│   ├── base.html
│   ├── voting/election.html
│   ├── voting/cast_vote.html
│   ├── voting/receipt.html
│   └── voting/public_chain.html
│
├── 📁 database/
│   └── schema.sql
│
├── 📁 docs/
│   ├── semana-01/protocolo_criptografico.md
│   ├── semana-02/blockchain_design.md
│   ├── semana-07/metricas_simulacion.md
│   └── semana-08/EF_paper_draft.md
│
└── 📁 tests/
    ├── test_blockchain.py               ← PoW, integridad, doble voto
    ├── test_voting_crypto.py            ← RSA sign/verify/anonymize
    └── test_integrity.py                ← Alteración detectada
```

---

## ⚡ Inicio Rápido (Local)

```bash
git clone https://github.com/TU-USUARIO/PS-P4-SecureVoting-System.git
cd PS-P4-SecureVoting-System
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env

flask run --port 8004
# → http://localhost:8004

pytest tests/ -v
```

---

## 🔐 Propiedades Criptográficas Garantizadas

| Propiedad | Mecanismo | Verificable |
|---|---|:---:|
| **Unicidad** | UNIQUE constraint + verify_voter_participation() en blockchain | ✅ |
| **Anonimato** | vote_hash = SHA256(firma_RSA), no el candidato | ✅ |
| **Integridad** | SHA-256 encadenado + Proof of Work | ✅ |
| **Verificabilidad** | El receipt incluye block_hash verificable en cadena pública | ✅ |
| **Auditabilidad** | Cadena pública en `/public/chain` sin datos privados | ✅ |

---

## 👥 Integrantes del Grupo G4

| # | Nombre | GitHub | Rol Técnico |
|:---:|---|---|---|
| 1 | [Completar] | [@usuario](https://github.com/usuario) | Líder / Blockchain Core |
| 2 | [Completar] | [@usuario](https://github.com/usuario) | Protocolo RSA + Firma |
| 3 | [Completar] | [@usuario](https://github.com/usuario) | Módulo Votación + Rutas |
| 4 | [Completar] | [@usuario](https://github.com/usuario) | Verificación Pública + Auditoría |
| 5 | [Completar] | [@usuario](https://github.com/usuario) | Azure Deploy + Métricas |

---

## 👨‍🏫 Contacto Docente

- **Docente:** Mg. Ruben Quispe Llacctarimay — [@RubenCarty](https://github.com/RubenCarty)
- **Repo del curso:** [DD281-Programacion-Segura-2026-1](https://github.com/RubenCarty/DD281-Programacion-Segura-2026-1)
- **Demo G4:** [civicvote.uqaisolutions.com.pe](https://civicvote.uqaisolutions.com.pe)

---

*Universidad Autónoma del Perú — DD281 Programación Segura — 2026-1*
*UQ AI SOLUTION COMPANY SAC — Ciclo VIII — Ingeniería de Sistemas*
