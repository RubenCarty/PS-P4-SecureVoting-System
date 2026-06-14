# Guía de Contribución — PS-P4 SecureVoting System

## Regla fundamental

> **TODOS los integrantes del grupo DEBEN abrir su propio Pull Request cada semana.**
> Si no hay PR tuyo → no tienes entrega → no tienes nota esa semana.

---

## Estructura de tu entrega semanal

```
semana-XX/
└── TU_APELLIDO_NOMBRE/
    ├── avance_sXX.md        ← Descripción de tu aporte
    ├── codigo/              ← Tu módulo implementado
    └── evidencia/           ← Tests y capturas
```

---

## Flujo para hacer tu PR semanal

```bash
git clone https://github.com/TU_USUARIO/PS-P4-SecureVoting-System.git
cd PS-P4-SecureVoting-System
git remote add upstream https://github.com/[LIDER]/PS-P4-SecureVoting-System.git

git fetch upstream && git merge upstream/main && git push origin main

git add semana-XX/APELLIDO_NOMBRE/
git commit -m "feat(sXX): [aporte] - APELLIDO NOMBRE"
git push origin main
# Abre PR en GitHub
```

---

## Convención de commits

```
feat(s05): implementa firma digital de papeleta con RSA - GARCIA JUAN
fix(s03): previene doble voto verificando token usado - LOPEZ MARIA
test(s06): verifica que código de recibo es único y verificable - QUISPE CARLOS
```

---

## Lo que NO se permite

- Claves privadas RSA en el repositorio
- Datos reales de votantes
- Push directo a `main`
- Algoritmos criptográficos de fabricación propia (solo usar bibliotecas auditadas)

---

*DD281 Programación Segura — Universidad Autónoma del Perú — 2026-1*
