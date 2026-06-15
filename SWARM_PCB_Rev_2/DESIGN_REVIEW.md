# SWARM_PCB Rev 2 — Design Review Package

**Date:** 2026-06-15  
**Revision:** Rev 2  
**Status:** Pre-production (JLCPCB ready, EMC open items)

## 1. Overview

SWARM communications board integrating an STM32F446 + Raspberry Pi Pico 2 control stack,
MEMS sensor suite (IMU, magnetometer, pressure, 6DoF), half-bridge motor driver section,
and a set of Hirose DF40C board-to-board connectors for system integration.

| Parameter | Value |
|-----------|-------|
| Board dimensions | 81.6 mm × 156.5 mm |
| Layer count | 2 (F.Cu + B.Cu) |
| Board thickness | 1.6 mm FR4 |
| Copper weight | 1 oz (35 µm) |
| Surface finish | HASL (default) |
| Solder mask | Both sides |
| Silkscreen | Both sides |
| Via tenting | Both sides |

## 2. Schematic Summary

- **Total components:** 227 (77 unique part numbers)
- **Total nets:** 358
- **No-connects:** 131
- **Hierarchical sheets:** CONTROL · POWER · SENSOR · TX\_RX · HEADER\_PINS (×5 instances)

**Power rails:**
- `+12V_POWER`: 12.0V
- `+3.3VA_CONTROL`: 3.3V
- `+3.3V_CONTROL`: 3.3V
- `+3.3V_HEADER`: 3.3V
- `+3.3V_POWER`: 3.3V
- `+3.3V_SENSOR`: 3.3V
- `+3.3V_TXRX`: 3.3V
- `+BATT_POWER`: —
- `+VPiezo_POWER`: —
- `12V_TXRX`: 12.0V
- `GND_CONTROL`: —
- `GND_HEADER`: —
- `GND_POWER`: —
- `GND_SENSOR`: —
- `GND_TXRX`: —
- `PWR_FLAG`: —
- `VBUS_CONTROL`: —
- `VCC_12`: —
- `VCC_3.3`: —
- `VIN_POWER`: —
- `VPiezo_TXRX`: —
- `V_REF_HALF_TXRX`: —

**Estimated power budget (known ICs):**

| Rail | IC | Est. current |
|------|----|-------------|
| `+3.3VA_CONTROL` | aU2 STM32F446RET6 | 100 mA |
| `+3.3V_CONTROL` | aU2 STM32F446RET6 | 100 mA |
| `+3.3V_CONTROL` | aU1 RaspberryPi Pico 2 | 10 mA |
| `+3.3V_SENSOR` | cU3 MS583730BA01-50 | 5 mA |

## 3. Bill of Materials

**77 line items · 219 total placements**

| Qty | References | Value | Package | MPN | Manufacturer |
|-----|-----------|-------|---------|-----|-------------|
| 2 | dL1,dL2 |  | L_Panasonic_PCC-M0630M | — | — |
| 2 | bC15,bC5 | 0.22u | C_0603_1608Metric | — | — |
| 5 | dR10,dR15,dR16,dR21 +1 | 10 | R_0603_1608Metric | — | — |
| 6 | dR12,dR13,dR25,dR26 +2 | 100 | R_0603_1608Metric | — | — |
| 10 | bR1,bR6,bR7,bR9 +6 | 100k | R_0603_1608Metric | — | — |
| 33 | aC1,aC10,aC11,aC12 +29 | 100n | C_0603_1608Metric | — | — |
| 17 | aR13,aR14,aR15,aR16 +13 | 10k | R_0603_1608Metric | — | — |
| 4 | aC15,bC25,dC27,dC28 | 10n | C_0603_1608Metric | — | — |
| 5 | aC14,aC5,aC8,cC4 +1 | 10u | C_0603_1608Metric | — | — |
| 3 | bC14,bC21,bC4 | 10u | C_0805_2012Metric | — | — |
| 1 | dC23 | 10u | C_0805_2012Metric_Pad1.18x1.45 | — | — |
| 2 | dC7,dC8 | 10u | C_1210_3225Metric | — | — |
| 1 | aFB1 | 120R | R_0603_1608Metric | — | — |
| 1 | dR30 | 121 | R_0603_1608Metric | — | — |
| 1 | bL2 | 15u | L_Wuerth_MAPI-5030 | — | — |
| 1 | aY2 | 16MHz | Crystal_SMD_SeikoEpson_FA238-4 | — | — |
| 1 | bF1 | 1812L150/24MR | Fuse_1812_4532Metric | — | — |
| 1 | bR11 | 182k | R_0603_1608Metric | — | — |
| 1 | bR10 | 187k | R_0603_1608Metric | — | — |
| 6 | aR1,aR12,aR2,aR3 +2 | 1k | R_0603_1608Metric | — | — |
| 7 | dC1,dC16,dC2,dC29 +3 | 1n | C_0603_1608Metric | — | — |
| 8 | aC16,aC17,aC18,aC19 +4 | 1u | C_0603_1608Metric | — | — |
| 2 | dC11,dC14 | 1u | C_0805_2012Metric | — | — |
| 2 | aC3,cC1 | 2.2u | C_0603_1608Metric | — | — |
| 1 | bC1 | 2.2u | C_0805_2012Metric | — | — |
| 1 | dR17 | 20m | R_2512_6332Metric | — | — |
| 8 | bC10,bC16,bC17,bC18 +4 | 22u | C_0805_2012Metric | — | — |
| 5 | bC11,bC2,bC22,bC23 +1 | 22u | C_1210_3225Metric | — | — |
| 1 | bL3 | 22u | L_Panasonic_PCC-M0630M | — | — |
| 1 | dR32 | 3.83k | R_0603_1608Metric | — | — |
| 2 | dR35,dR36 | 3.92k | R_0603_1608Metric | — | — |
| 1 | aY1 | 32.768KHz | Crystal_SMD_MicroCrystal_CM9V- | — | — |
| 1 | bR3 | 36k | R_0603_1608Metric | — | — |
| 5 | aR10,aR11,bR2,cR1 +1 | 4.7k | R_0603_1608Metric | — | — |
| 1 | bR5 | 43.2k | R_0603_1608Metric | — | — |
| 4 | dR1,dR2,dR3,dR4 | 47k | R_0603_1608Metric | — | — |
| 1 | dC9 | 47u | C_0603_1608Metric | — | — |
| 3 | aR7,aR8,dR29 | 5.1k | R_0603_1608Metric | — | — |
| 1 | dR33 | 5.9k | R_0603_1608Metric | — | — |
| 1 | bL1 | 6.8u | L_Wuerth_MAPI-5030 | — | — |
| 1 | bR4 | 82k | R_0603_1608Metric | — | — |
| 1 | bR15 | 84.5k | R_0603_1608Metric | — | — |
| 1 | bR8 | 9.09k | R_0603_1608Metric | — | — |
| 1 | dR31 | 953 | R_0603_1608Metric | — | — |
| 1 | dU5 | ADG7421FBCPZ-RL7 | CP-10-16_ADI | — | — |
| 1 | cU2 | ASM330LHHXTR | XDCR_ASM330LHHXTR | — | STMicroelectronics |
| 2 | bD3,bD4 | BLUE | LED_JE2835_CRW | — | — |
| 1 | aJ1 | Conn_01x02_Pin | PinHeader_1x02_P1.00mm_Vertica | — | — |
| 1 | dJ1 | Conn_01x03_Pin | JST_XH_B3B-XH-AM_1x03_P2.50mm_ | — | — |
| 1 | aJ4 | Conn_01x06_Pin | PinHeader_1x06_P1.00mm_Vertica | — | — |
| 2 | bJ2,dJ2 | Conn_01x08_Pin | JST_PH_B8B-PH-SM4-TB_1x08-1MP_ | — | — |
| 3 | J25,J26,J27 | Conn_01x12_Pin | PinSocket_1x12_P2.54mm_Vertica | — | — |
| 1 | J28 | Conn_01x13_Pin | PinSocket_1x13_P2.54mm_Vertica | — | — |
| 15 | J10,J11,J12,J18 +11 | Conn_02x25_Odd_Even | HIROSE_DF40C-50DP-0.4V_51_ | — | — |
| 1 | bD2 | GREEN | LED_JE2835_CRW | — | — |
| 1 | dU3 | INA240A2DR | SOIC-8_3.9x4.9mm_P1.27mm | — | — |
| 1 | dU7 | INA823DR | SOIC127P599X175-8N | — | — |
| 4 | dQ1,dQ2,dQ3,dQ4 | IPD50N10S3L-16 | TO-252-2 | — | — |
| 2 | bU1,bU2 | LMR33630ADDA | Texas_HSOP-8-1EP_3.9x4.9mm_P1. | — | — |
| 1 | cU4 | LSM6DSO32TR | XDCR_LSM6DSO32TR | — | STMicroelectronics |
| 1 | cU1 | MMC5603NJ | XDCR_MMC5603NJ | — | Memsic Inc. |
| 1 | cU3 | MS583730BA01-50 | TE_MS5837-xxBA | — | — |
| 1 | aJ3 | Micro_SD_Card | AMPHENOL_1140084168 | — | — |
| 1 | dU8 | OPA2322AIDGKR | DGK8 | — | — |
| 1 | aD1 | PURPLE | LED_JE2835_CRW | — | — |
| 1 | aD2 | RGB | LED_RGB_PLCC-6 | — | — |
| 1 | aU1 | RaspberryPi Pico 2 | RaspberryPi_Pico_SMD | — | — |
| 1 | bD1 | SMBJ18A | D_SMB | — | — |
| 1 | bD5 | SS34-HF | D_SMA | — | — |
| 1 | aU2 | STM32F446RET6 | LQFP-64_10x10mm_P0.5mm | — | — |
| 1 | dU4 | TLV9101IDCKR | SC70-5_DCK_TEX | — | — |
| 1 | dU6 | TPD2E007DCKR | DCK3 | TPD2E007DCKR | — |
| 1 | bU3 | TPS55340RTER | QFN50P300X300X80-17N | — | — |
| 2 | dU1,dU2 | UCC27211D | SOIC127P599X175-8N | — | Texas Instruments |
| 1 | aU3 | USBLC6-2SC6 | SOT-23-6 | — | — |
| 1 | aJ2 | USB_C_Receptacle_USB2.0_16P | USB_C_Receptacle_GCT_USB4085 | — | — |
| 1 | bJ1 | XT30PW-M | AMASS_XT30PW-M | — | Amass |

## 4. PCB Analysis

- **Footprints:** 253 (214 front, 39 back)
- **SMD / THT:** 221 / 9
- **Vias:** 1540 (all tented both sides)
- **Track segments:** 2180
- **Total track length:** 5154 mm
- **Copper pour zones:** 6
- **Routing:** Complete (0 unrouted)

**Assembly complexity:**
- Score: 38/100 (Low assembly complexity (score 38/100) — hand assembly feasible)
- Hard: 5, Medium: 201, Easy: 21

**Package breakdown:**
- 0603: 132
- other_SMD: 53
- 0805: 15
- 1210: 7
- SON: 4
- SOIC: 4
- TO-252: 4
- SOP: 2
- LQFP: 1
- SOT-23: 1
- 2512: 1
- SC70: 1
- QFN: 1
- 1812: 1

### 4.1 DRC Findings

| Rule | Severity | Count | Description | Status |
|------|----------|-------|-------------|--------|
| CC-DET | info | 18 | Copper clearance detection | Info only |
| CP-002 | info | 60 | Copper pour info | Info only |
| DFM-001 | warning | 3 | Annular ring 0.1mm — advanced process required | FIXED (482 vias increased to 0.1mm ring) |
| DFM-002 | warning | 1 | Via annular ring below IPC Class 2 (0.125mm) | FIXED |
| PM-001 | error | 9 | Courtyard overlaps (J28/J26, aC9/aC14 vs aU2) | ACCEPTED (courtyard overlaps) |
| PM-002 | warning | 9 | Components outside/near board edge (aU1, bJ2, dJ2) | ACCEPTED (edge clearance) |
| TE-001 | warning | 1 | Thermal relief | Info only |
| TS-DET | info | 6 | Trace size detection | Info only |
| TV-001 | info | 9 | Trace/via info | Info only |

## 5. EMC Pre-Compliance Analysis

> Analysis performed by kicad-happy EMC analyzer.

| Rule | Severity | Count | Issue | Recommended Action |
|------|----------|-------|-------|--------------------|
| GP-001 | error | 54 | Signal with significant reference plane gap (return current discontinuity) | Add ground stitching vias under signal routes (KiCad rework) |
| SU-001 | error | 1 | Adjacent signal layers F.Cu / B.Cu without ground plane between | 2-layer board limitation — acceptable for prototype |
| BE-001 | warning | 11 | Signal routed near board edge (potential radiation) | Keep-away zone or reroute signals away from board edge |
| CK-003 | warning | 5 | Clock signal routed near I/O connector | Add ground guard trace or increase spacing on SWCLK |
| GP-005 | warning | 1 | Multiple ground domains (6 detected) — potential ground loops | Merge GND domains with stitching vias at board boundaries |
| EE-001 | info | 1 | Board cavity resonance frequencies estimated | Informational — no action |
| IO-001 | info | 22 | No EMC filter near I/O connector pins | Add ferrite + cap filter at each connector (if CE/FCC required) |
| IO-002 | info | 25 | Insufficient ground pins on I/O connectors | Increase GND pin count in connector pinout (future rev) |
| RP-001 | info | 22 | Missing ground stitching via at layer transition | Add via adjacent to each F.Cu→B.Cu transition |

## 6. Schematic Findings

| Rule | Severity | Count | Description |
|------|----------|-------|-------------|
| SS-001 | error | 1 | PWR_FLAG / power symbol issue |
| DS-002 | warning | 1 | Datasheet URL missing or invalid |
| PU-001 | warning | 4 | Pull-up resistor warning |
| RS-001 | warning | 13 | Resistor value / series check |
| BR-DET | info | 1 | Bus / rail detection info |
| CG-AUD | info | 24 | Component group audit info |
| DI-DET | info | 1 | Diode detection info |
| DO-DET | info | 6 | DNP/optional component info |
| EP-AUD | info | 29 | ERC pin audit info |
| PD-DET | info | 2 | Power domain detection info |
| PR-DET | info | 1 | Passive reference detection |
| SJ-DET | info | 3 | SJ (solder jumper) detection |

## 7. PCB Fixes Applied This Revision

| Fix | Rule | Description | Scope |
|-----|------|-------------|-------|
| Via tenting | VP-001 | Added `(tenting front back)` to all vias | 1,540 vias |
| Keepout zones removed | KO-001 | Removed stale auto-placement-area zones | 4 zones |
| Annular ring increase | DFM-001 | 0.25→0.35 and 0.3→0.4 pad sizes | 482 vias |
| Fiducial markers added | FD-001 | 1mm/2mm-mask fiducials on F.Cu and B.Cu | 6 markers |

## 8. Open Items

| Priority | Item | Owner |
|----------|------|-------|
| High | EMC GP-001: Add ground stitching vias (54 sites) | Layout |
| High | EMC RP-001: Add GND via at each layer transition (22 sites) | Layout |
| Medium | EMC CK-003: Route SWCLK away from aJ4 or add guard trace | Layout |
| Medium | EMC GP-005: Stitch 6 ground domains at board boundaries | Layout |
| Low | Assign MPNs for LEDs (aD1, aD2, bD2, bD3, bD4) | BOM |
| Low | Assign MPNs for generic headers (J25–J28, aJ1, aJ4) | BOM |
| Low | Verify dC9 rail voltage (47µF Samsung 0603 rated 4V) | Schematic |
| Low | Verify bL1/bL2 Würth WE-MAPI catalog numbers | BOM |
| Info | dU7 confirmed INA823DR (description corrected) | — |
| Info | PM-001/PM-002 courtyard + edge violations accepted | — |

## 9. JLCPCB Manufacturing Checklist

| Item | Status |
|------|--------|
| Gerbers from KiCad 7 | Ready to export |
| Layer count: 2 | OK |
| Board thickness: 1.6mm | OK |
| Min trace: ≥0.1mm | Verify in KiCad DRC |
| Min spacing: ≥0.1mm | Verify in KiCad DRC |
| Min drill: ≥0.15mm | OK (0.15mm used) |
| Annular ring: ≥0.1mm | FIXED (was 0.05mm) |
| Via tenting | DONE (both sides) |
| Fiducials (≥3) | DONE (6 added) |
| HASL / ENIG finish | Select at order |
| Impedance control | Not required (2-layer, no controlled impedance traces) |
| Stencil | Order with board for SMT |
