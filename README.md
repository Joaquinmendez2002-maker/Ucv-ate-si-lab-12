# 🧠 UCV-ATE-SI-LAB-12 — Perceptrón Simple

[![CI](https://github.com/Joaquinmendez2002-maker/Ucv-ate-si-lab-12/actions/workflows/ci.yml/badge.svg)](https://github.com/Joaquinmendez2002-maker/Ucv-ate-si-lab-12/actions/workflows/ci.yml)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=Joaquinmendez2002-maker_Ucv-ate-si-lab-12&metric=alert_status)](https://sonarcloud.io/project/overview?id=Joaquinmendez2002-maker_Ucv-ate-si-lab-12)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=Joaquinmendez2002-maker_Ucv-ate-si-lab-12&metric=coverage)](https://sonarcloud.io/project/overview?id=Joaquinmendez2002-maker_Ucv-ate-si-lab-12)

> Laboratorio de Inteligencia Artificial — Universidad César Vallejo  
> Implementación desde cero de un **Perceptrón Simple** para la aprobación automatizada de créditos bancarios.

---

## 📋 Descripción

Un banco desea automatizar la aprobación preliminar de créditos utilizando dos variables de entrada:

| Variable | Descripción |
|---|---|
| `ingreso_mensual` | Nivel de ingreso del solicitante (escala 1–10) |
| `historial_crediticio` | Historial crediticio: `1` = bueno, `0` = malo |

El perceptrón aprende a clasificar solicitudes como **aprobadas (1)** o **rechazadas (0)** a partir de datos de entrenamiento históricos.

---

## 🗂️ Estructura del Proyecto

```
UCV-ATE-SI-LAB-12/
├── .github/
│   └── workflows/
│       └── ci.yml              # Pipeline CI con GitHub Actions
├── Lab-PerceptronSimple/
│   ├── src/
│   │   ├── __init__.py
│   │   ├── dataset.py          # Datos de entrenamiento
│   │   └── perceptron.py       # Implementación del Perceptrón
│   ├── tests/
│   │   ├── __init__.py
│   │   └── test_perceptron.py  # Pruebas unitarias con pytest
│   ├── main.py                 # Punto de entrada
│   └── pytest.ini              # Configuración de pytest
├── .gitignore
└── README.md
```

---

## 🚀 Instalación y Uso

### Prerrequisitos

- Python 3.12+
- Git

### Clonar el repositorio

```bash
git clone https://github.com/Joaquinmendez2002-maker/Ucv-ate-si-lab-12.git
cd Ucv-ate-si-lab-12
```

### Ejecutar el proyecto

```bash
cd Lab-PerceptronSimple
python main.py
```

### Ejecutar las pruebas

```bash
cd Lab-PerceptronSimple
pip install pytest
pytest
```

---

## 🧪 Dataset de Entrenamiento

```python
training_data = [
    ([8, 1], 1),  # Ingreso alto + buen historial → Aprobado
    ([7, 1], 1),
    ([6, 1], 1),
    ([3, 0], 0),  # Ingreso bajo + mal historial → Rechazado
    ([2, 0], 0),
    ([1, 0], 0)
]
```

---

## 🧠 Arquitectura del Perceptrón

```
Entradas:        Pesos:           Suma ponderada:      Activación:
x1 (ingreso) ──→ w1 ──┐
                       ├──→ Σ(xi·wi) + bias ──→ f(z) ──→ salida (0 o 1)
x2 (historial)──→ w2 ──┘
```

**Función de activación:** escalón unitario — retorna `1` si `z ≥ 0`, `0` en caso contrario.

**Regla de aprendizaje (Perceptrón):**

```
w_i ← w_i + η · (esperado − predicción) · x_i
bias ← bias + η · (esperado − predicción)
```

Donde `η = 0.1` es la tasa de aprendizaje.

---

## ⚙️ CI/CD con GitHub Actions

El pipeline se ejecuta automáticamente en cada `push` y `pull_request`:

```yaml
on:
  push:
  pull_request:
```

**Pasos del pipeline:**

1. Checkout del código
2. Setup de Python 3.12
3. Instalación de `pytest`
4. Ejecución de pruebas unitarias

---

## 🔍 Análisis de Calidad con SonarCloud

Este proyecto está integrado con **SonarCloud** para análisis estático de código.

- **Connection ID:** `joaquinmendez2002-maker`
- **Project Key:** `Joaquinmendez2002-maker_Ucv-ate-si-lab-12`
- **Dashboard:** [Ver en SonarCloud](https://sonarcloud.io/project/overview?id=Joaquinmendez2002-maker_Ucv-ate-si-lab-12)

La configuración de SonarLint en VS Code (`settings.json`) permite análisis en tiempo real:

```json
{
    "sonarlint.connectedMode.project": {
        "connectionId": "joaquinmendez2002-maker",
        "projectKey": "Joaquinmendez2002-maker_Ucv-ate-si-lab-12"
    }
}
```

---

## 🌿 Flujo de Ramas

| Rama | Propósito |
|---|---|
| `main` | Código estable y en producción |
| `develop` | Desarrollo activo e integración continua |

Los cambios se desarrollan en `develop` y se integran a `main` mediante Pull Request.

---

## 📝 Preguntas de Análisis

1. **¿Qué representan los pesos?**  
   Indican la importancia relativa de cada variable de entrada (ingreso e historial) sobre la decisión final del modelo.

2. **¿Qué función cumple el bias?**  
   Desplaza el umbral de activación, permitiendo al modelo ajustarse incluso cuando todas las entradas son cero.

3. **¿Cómo aprende el perceptrón?**  
   Calcula el error entre la predicción y el valor esperado, y ajusta los pesos y el bias proporcionalmente a ese error durante varias épocas.

4. **¿Por qué el perceptrón no puede resolver XOR?**  
   El perceptrón simple solo puede separar clases **linealmente separables**. XOR no lo es: sus cuatro puntos no pueden dividirse con una única línea recta.

5. **¿Qué ventajas tiene un perceptrón multicapa?**  
   Puede aprender fronteras de decisión **no lineales** mediante capas ocultas con funciones de activación no lineales (como ReLU o sigmoide), resolviendo problemas como XOR.

---

## 🎯 Reto MIT — Problema XOR

| x1 | x2 | XOR |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Un perceptrón simple **no puede resolver XOR** porque sus salidas no son linealmente separables en el plano (ninguna línea recta puede dividir los `1` de los `0`).

Un **perceptrón multicapa (MLP)** sí puede resolverlo agregando una capa oculta con 2 neuronas que aprenden representaciones intermedias, combinadas en la capa de salida para producir la clasificación correcta.

---

## 🛠️ Herramientas

![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)
![pytest](https://img.shields.io/badge/pytest-testing-0A9EDC?logo=pytest&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI/CD-2088FF?logo=githubactions&logoColor=white)
![SonarCloud](https://img.shields.io/badge/SonarCloud-Quality-F3702A?logo=sonarcloud&logoColor=white)
![VS Code](https://img.shields.io/badge/VS_Code-Editor-007ACC?logo=visualstudiocode&logoColor=white)

---

## 👤 Autor

**Joaquin Mendez**  
[@Joaquinmendez2002-maker](https://github.com/Joaquinmendez2002-maker)  
Universidad César Vallejo — Ingeniería de Sistemas

---

*Laboratorio de Inteligencia Artificial — 2025*