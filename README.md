# BIPV Structural Load API

**Structural design loads for building-integrated photovoltaic (BIPV) facade and roof systems.**  
EN 1991-1-4:2005 · EN 1990:2002 · ASCE 7-22 · Research-grade. Every value cites its source standard.

[![RapidAPI](https://img.shields.io/badge/RapidAPI-Subscribe-0055DA?style=flat-square)](https://rapidapi.com/bethelnedi/api/bipv-structural-load-api)
[![Docs](https://img.shields.io/badge/API_Docs-Swagger-85EA2D?style=flat-square)](https://amfumu-bipv-structural-api.hf.space/docs)
[![Bundle](https://img.shields.io/badge/Bundle-BIPV_Suite_$79/mo-purple?style=flat-square)](https://rapidapi.com/user/bethelnedi)

---

## What It Calculates

Send building geometry, panel specification, and installation configuration. Get back a complete structural load output — every value cited to its source standard or peer-reviewed paper.

| Output | Source Standard |
|--------|----------------|
| Peak wind velocity pressure qp(z) | EN 1991-1-4:2005 Eq.(4.8) |
| External pressure coefficients Cpe | EN 1991-1-4:2005 Table 7.1 |
| Air permeability correction factor | Miller & Kopp (2024) DOI:10.3389/fbuil.2024.1398472 |
| Net wind pressure on panel (Pa, kN/m²) | EN 1991-1-4:2005 §5.2 |
| Panel + mounting dead load (kN/m²) | EN 1991-1-1:2002 Annex A |
| ULS load combinations | EN 1990:2002 Table A1.2(B) |
| Bracket shear + pull-out forces (kN) | EN 1990:2002 §6.4 |
| SLS deflection check L/200 | Yin et al. (2023) Eng. Structures 285:116021 |
| US wind loads C&C | ASCE 7-22 Chapter 30 |

---

## Quick Start

```bash
curl -X POST https://amfumu-bipv-structural-api.hf.space/calculate \
  -H "X-API-Key: YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "site": {
      "basic_wind_speed_ms": 28,
      "terrain_category": "II",
      "building_height_m": 30,
      "building_width_m": 40,
      "building_depth_m": 20,
      "standard": "EN"
    },
    "panel": {
      "panel_type": "glass_glass_standard",
      "panel_width_m": 1.0,
      "panel_height_m": 1.7,
      "panel_thickness_mm": 12.0
    },
    "installation": {
      "installation_type": "ventilated_facade_bracket",
      "facade_zone": "B",
      "tilt_deg": 90,
      "fixing_points": 4,
      "bracket_spacing_m": 0.85
    }
  }'
```

**Returns:**
```json
{
  "results": {
    "net_wind_pressure": { "w_net_pa": -861.6 },
    "uls_combinations": { "governing_uls_kn_m2": 1.591 },
    "bracket_loads": { "pullout_force_kn": 0.676 },
    "deflection_sls": { "passes_sls": true, "utilisation_ratio": 0.302 }
  }
}
```

---

## Facade Zones

Zone A (corners) always produces the highest suction loads and governs bracket design.

| Zone | Location | Cpe (10m²) |
|------|----------|-------------|
| A | Corners | -1.2 |
| B | Mid-wall | -0.8 |
| C | Large surfaces | -0.5 |
| D | Windward face | +0.8 |
| E | Leeward face | -0.6 |

Use `POST /all-zones` (Pro) to get the full zone map for a building elevation in one call.

---

## Panel Types

| Type | Weight kg/m² |
|------|-------------|
| glass_glass_standard | 22.0 |
| glass_glass_thin | 17.0 |
| glass_backsheet | 12.5 |
| glass_glass_semitrans | 20.0 |
| thin_film_glass | 15.0 |
| flexible_lightweight | 3.5 |

---

## Scope

**Covered:** Wind loads · Dead loads · ULS/SLS combinations · Bracket design forces · Air permeability correction · EN Eurocode and ASCE 7-22.

**Not covered:** Glass stress (EN 16612:2019) · Seismic loads (EN 1998-1) · Connection capacity (EN 1993-1-8). These require material certificates and site-specific hazard data.

---

## Plans

| Plan | Price | Calls |
|------|-------|-------|
| Free | $0/mo | 10/month |
| Pro | $49/mo | 2,000/hr |
| **BIPV Bundle** | **$79/mo** | Structural + Energy Yield APIs |

---

## Citation Register

- EN 1991-1-4:2005 — Eurocode 1: Wind actions
- EN 1991-1-1:2002 — Eurocode 1: Densities, self-weight, imposed loads
- EN 1990:2002 — Eurocode: Basis of structural design
- ASCE 7-22 — Minimum Design Loads for Buildings
- Miller & Kopp (2024) Front. Built Environ. DOI:10.3389/fbuil.2024.1398472
- Yin et al. (2023) Engineering Structures 285:116021

---

## Topics

`bipv` `structural-loads` `wind-loads` `eurocode` `asce-7` `facade-engineering` `building-integrated-pv` `en-1991` `uls` `sls` `bracket-design` `solar-facade` `curtain-wall` `structural-engineering` `fastapi` `python` `rapidapi` `solar-api`
