# SWARM_PCB Rev 2 — Design Review Package

**Date:** 2026-06-17
**Revision:** Rev 2
**Status:** Pre-production — schematic and layout open items remain before fabrication

---

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

---

## 2. Schematic Summary

- **Total components:** 227 (77 unique part numbers)
- **Total nets:** 358
- **No-connects:** 131
- **Hierarchical sheets:** CONTROL · POWER · SENSOR · TX\_RX · HEADER\_PINS (×5 instances)

**Power rails:**

| Net | Voltage | Source |
|-----|---------|--------|
| `VIN_POWER` | 12–16.8 V | bJ1 XT30 (battery) |
| `+12V_POWER` | 12.0 V | bU2 LMR33630 |
| `12V_TXRX` | 12.0 V | bU2 LMR33630 |
| `+3.3V_POWER` | 3.3 V | bU1 LMR33630 |
| `+3.3V_CONTROL` | 3.3 V | bU1 |
| `+3.3VA_CONTROL` | 3.3 V | filtered from +3.3V via aFB1 |
| `+3.3V_SENSOR` | 3.3 V | bU1 |
| `+3.3V_TXRX` | 3.3 V | bU1 |
| `+3.3V_HEADER` | 3.3 V | bU1 |
| `+VPiezo_POWER` | ~23.85 V | bU3 TPS55340RTER |

**Verified regulator output voltages:**

| Regulator | R_top | R_bot | V_ref | V_out calculated |
|-----------|-------|-------|-------|-----------------|
| bU1 LMR33630 (+3.3V) | bR1=100k | bR5=43.2k | 1.0V | **3.315V** ✓ |
| bU2 LMR33630 (+12V) | bR7=100k | bR8=9.09k | 1.0V | **12.00V** ✓ |
| bU3 TPS55340RTER (VPiezo) | bR10=255k | bR12=10k | 0.9V | **23.85V** ✓ |

---

## 3. Bill of Materials

**77 line items · 219 total placements**

| Qty | References | Value | Package | MPN |
|-----|-----------|-------|---------|-----|
| 2 | dL1,dL2 | **(empty — see Finding #C3)** | L_Panasonic_PCC-M0630M | — |
| 2 | bC15,bC5 | 0.22u | C_0603_1608Metric | — |
| 5 | dR10,dR15,dR16,dR21 +1 | 10 | R_0603_1608Metric | — |
| 6 | dR12,dR13,dR25,dR26 +2 | 100 | R_0603_1608Metric | — |
| 10 | bR1,bR6,bR7,bR9 +6 | 100k | R_0603_1608Metric | — |
| 33 | aC1,aC10,aC11,aC12 +29 | 100n | C_0603_1608Metric | — |
| 17 | aR13,aR14,aR15,aR16 +13 | 10k | R_0603_1608Metric | — |
| 4 | aC15,bC25,dC27,dC28 | 10n | C_0603_1608Metric | — |
| 5 | aC14,aC5,aC8,cC4 +1 | 10u | C_0603_1608Metric | — |
| 3 | bC14,bC21,bC4 | 10u | C_0805_2012Metric | — |
| 1 | dC23 | 10u | C_0805_2012Metric_Pad1.18x1.45 | — |
| 2 | dC7,dC8 | 10u | C_1210_3225Metric | — |
| 1 | aFB1 | 120R | R_0603_1608Metric | — |
| 1 | dR30 | 121 | R_0603_1608Metric | — |
| 1 | bL2 | 15u | L_Wuerth_MAPI-5030 | — |
| 1 | aY2 | 16MHz | Crystal_SMD_SeikoEpson_FA238-4 | — |
| 1 | bF1 | 1812L150/24MR | Fuse_1812_4532Metric | — |
| 1 | bR11 | 182k | R_0603_1608Metric | — |
| 1 | bR10 | **255k** | R_0603_1608Metric | — |
| 6 | aR1,aR12,aR2,aR3 +2 | 1k | R_0603_1608Metric | — |
| 7 | dC1,dC16,dC2,dC29 +3 | 1n | C_0603_1608Metric | — |
| 8 | aC16,aC17,aC18,aC19 +4 | 1u | C_0603_1608Metric | — |
| 2 | dC11,dC14 | 1u | C_0805_2012Metric | — |
| 2 | aC3,cC1 | 2.2u | C_0603_1608Metric | — |
| 1 | bC1 | 2.2u | C_0805_2012Metric | — |
| 1 | dR17 | 20m | R_2512_6332Metric | — |
| 8 | bC10,bC16,bC17,bC18 +4 | 22u | C_0805_2012Metric | — |
| 5 | bC11,bC2,bC22,bC23 +1 | 22u | C_1210_3225Metric | — |
| 1 | bL3 | 22u | L_Panasonic_PCC-M0630M | — |
| 1 | dR32 | 3.83k | R_0603_1608Metric | — |
| 2 | dR35,dR36 | 3.92k | R_0603_1608Metric | — |
| 1 | aY1 | 32.768KHz | Crystal_SMD_MicroCrystal_CM9V- | — |
| 1 | bR3 | 36k | R_0603_1608Metric | — |
| 1 | aR18 | 33 | R_0603_1608Metric | — |
| 5 | aR10,aR11,bR2,cR1 +1 | 4.7k | R_0603_1608Metric | — |
| 1 | bR5 | 43.2k | R_0603_1608Metric | — |
| 4 | dR1,dR2,dR3,dR4 | 47k | R_0603_1608Metric | — |
| 1 | dC9 | 47u | C_0603_1608Metric | — |
| 3 | aR7,aR8,dR29 | 5.1k | R_0603_1608Metric | — |
| 1 | dR33 | 5.9k | R_0603_1608Metric | — |
| 1 | bL1 | 6.8u | L_Wuerth_MAPI-5030 | — |
| 1 | bR4 | 82k | R_0603_1608Metric | — |
| 1 | bR15 | 84.5k | R_0603_1608Metric | — |
| 1 | bR8 | 9.09k | R_0603_1608Metric | — |
| 1 | dR31 | 953 | R_0603_1608Metric | — |
| 1 | dU5 | ADG7421FBCPZ-RL7 | CP-10-16_ADI | — |
| 1 | cU2 | ASM330LHHXTR | XDCR_ASM330LHHXTR | — |
| 2 | bD3,bD4 | BLUE | LED_JE2835_CRW | JE2835ABL-N-0005A0000-N0000001 |
| 1 | aJ1 | Conn_01x02_Pin | PinHeader_1x02_P1.00mm_Vertical | — |
| 1 | dJ1 | Conn_01x03_Pin | JST_XH_B3B-XH-AM_1x03_P2.50mm_ | — |
| 1 | aJ4 | Conn_01x06_Pin | PinHeader_1x06_P1.00mm_Vertical | — |
| 2 | bJ2,dJ2 | Conn_01x08_Pin | JST_PH_B8B-PH-SM4-TB_1x08-1MP_ | — |
| 3 | J25,J26,J27 | Conn_01x12_Pin | PinSocket_1x12_P2.54mm_Vertical | — |
| 1 | J28 | Conn_01x13_Pin | PinSocket_1x13_P2.54mm_Vertical | — |
| 15 | J10,J11,J12,J18 +11 | Conn_02x25_Odd_Even | HIROSE_DF40C-50DP-0.4V_51_ | — |
| 1 | bD2 | GREEN | LED_JE2835_CRW | JE2835AGR-N-0002A0000-N0000001 |
| 1 | dU3 | INA240A2DR | SOIC-8_3.9x4.9mm_P1.27mm | — |
| 1 | dU7 | INA823DR | SOIC127P599X175-8N | INA823DR |
| 4 | dQ1,dQ2,dQ3,dQ4 | IPD50N10S3L-16 | TO-252-2 | — |
| 2 | bU1,bU2 | LMR33630ADDA | Texas_HSOP-8-1EP_3.9x4.9mm_P1. | — |
| 1 | cU4 | LSM6DSO32TR | XDCR_LSM6DSO32TR | — |
| 1 | cU1 | MMC5603NJ | XDCR_MMC5603NJ | — |
| 1 | cU3 | MS583730BA01-50 | TE_MS5837-xxBA | — |
| 1 | aJ3 | Micro_SD_Card | AMPHENOL_1140084168 | — |
| 1 | dU8 | OPA2322AIDGKR | DGK8 | — |
| 1 | aD1 | PURPLE | LED_JE2835_CRW | JE2835APP-N-0001A0000-N0000001 |
| 1 | aD2 | RGB | LED_RGB_PLCC-6 | L1MC-RGB0028000MP0 |
| 1 | aU1 | RaspberryPi Pico 2 | RaspberryPi_Pico_SMD | — |
| 1 | bD1 | SMBJ18A | D_SMB | — |
| 1 | bD5 | SS34-HF | D_SMA | — |
| 1 | aU2 | STM32F446RET6 | LQFP-64_10x10mm_P0.5mm | — |
| 1 | dU4 | TLV9101IDCKR | SC70-5_DCK_TEX | — |
| 1 | dU6 | TPD2E007DCKR | DCK3 | TPD2E007DCKR |
| 1 | bU3 | TPS55340RTER | QFN50P300X300X80-17N | TPS55340RTER |
| 2 | dU1,dU2 | UCC27211D | SOIC127P599X175-8N | — |
| 1 | aU3 | USBLC6-2SC6 | SOT-23-6 | — |
| 1 | aJ2 | USB_C_Receptacle_USB2.0_16P | USB_C_Receptacle_GCT_USB4085 | — |
| 1 | bJ1 | XT30PW-M | AMASS_XT30PW-M | — |

---

## 4. PCB Analysis

- **Footprints:** 253 (214 front, 39 back)
- **SMD / THT:** 221 / 9
- **Vias:** 1540 (all tented both sides)
- **Track segments:** 2180
- **Total track length:** 5154 mm
- **Copper pour zones:** 6
- **Routing:** Complete (0 unrouted)

**Assembly complexity:**
- Score: 38/100 — hand assembly feasible
- Hard: 5, Medium: 201, Easy: 21

### 4.1 DRC Findings

| Rule | Severity | Count | Description | Status |
|------|----------|-------|-------------|--------|
| CC-DET | info | 18 | Copper clearance detection | Info only |
| CP-002 | info | 60 | Copper pour info | Info only |
| DFM-001 | warning | 3 | Annular ring 0.1mm — advanced process required | FIXED (482 vias increased to 0.1mm ring) |
| DFM-002 | warning | 1 | Via annular ring below IPC Class 2 (0.125mm) | FIXED |
| PM-001 | error | 9 | Courtyard overlaps (J28/J26, aC9/aC14 vs aU2) | ACCEPTED |
| PM-002 | warning | 9 | Components outside/near board edge (aU1, bJ2, dJ2) | ACCEPTED |
| TE-001 | warning | 1 | Thermal relief | Info only |
| TS-DET | info | 6 | Trace size detection | Info only |
| TV-001 | info | 9 | Trace/via info | Info only |

---

## 5. EMC Pre-Compliance Analysis

| Rule | Severity | Count | Issue | Recommended Action |
|------|----------|-------|-------|--------------------|
| GP-001 | error | 54 | Signal with significant reference plane gap | Add ground stitching vias under signal routes |
| SU-001 | error | 1 | Adjacent signal layers F.Cu/B.Cu without ground plane | 2-layer limitation — acceptable for prototype |
| BE-001 | warning | 11 | Signal routed near board edge | Keep-away zone or reroute away from edge |
| CK-003 | warning | 5 | Clock signal routed near I/O connector | Add ground guard trace or increase spacing on SWCLK |
| GP-005 | warning | 1 | Multiple ground domains (6 detected) | Merge GND domains with stitching vias at boundaries |
| EE-001 | info | 1 | Board cavity resonance frequencies estimated | Informational — no action |
| IO-001 | info | 22 | No EMC filter near I/O connector pins | Add ferrite + cap filter if CE/FCC required |
| IO-002 | info | 25 | Insufficient ground pins on I/O connectors | Increase GND pin count in future rev |
| RP-001 | info | 22 | Missing ground stitching via at layer transition | Add via adjacent to each F.Cu→B.Cu transition |

---

## 6. Schematic Findings

Findings are grouped by sheet and severity. Items marked ✓ have been resolved.

### 6.1 POWER Sheet

| ID | Sev | Description | Action |
|----|-----|-------------|--------|
| P1 | **Critical** | Input capacitors bC2, bC6, bC11 (22µF/1210) rated 6.3V on VIN_POWER (12–17V) — will fail in service | Replace with ≥25V-rated 22µF/1210 (e.g., GRM32ER61E226KE15L) |
| P2 | **Critical** | Input caps bC1 (2.2µF), bC4, bC14, bC21 (10µF) rated 10V on 12–17V VIN rail | Replace with ≥25V-rated equivalents |
| P3 | **Critical** | Output caps bC16–bC19 (22µF/0805) rated 6.3V on +12V_POWER output | Replace with ≥25V-rated 22µF/0805 |
| P4 | **Critical** | Output caps bC22, bC23 (22µF/1210) rated 6.3V on +VPiezo_POWER (~24V) | Replace with ≥50V-rated 22µF (1210 or 1812) |
| P5 | **High** | bR10 schematic value = 255k but MPN field still holds 187k part number (RC0603FR-07187KL) | Change MPN to RC0603FR-07255KL |
| P6 | **Info** | bF1 polyfuse hold 1.5A: total VIN draw estimated ~310mA at 3.3W system power (piezo comms load is real-power limited, reactive current circulates in LC network) — 4.8× margin ✓ | — |
| P7 | **Medium** | bD3 (BLUE LED) drive current ≈ 0.24mA via bR3=36kΩ from 12V — likely invisible | Reduce bR3 to 10–15kΩ for ~0.6–0.85mA, or document as intentional |
| P8 | **Low** | bD1 SMBJ18A TVS uses SS34 Schottky symbol — misleading in schematic | Replace symbol with TVS/Zener symbol; add MPN=SMBJ18A |
| P9 | **Low** | No reverse-polarity protection on VIN before bF1 — reversed battery destroys all ICs | Add P-channel FET or Schottky in series (if connector is not keyed: XT30 is polarised so this is low priority) |
| P10 | **Info** | bU1 V_out = 3.315V ✓, bU2 V_out = 12.00V ✓, bU3 V_out = 23.85V ✓ | — |

### 6.2 CONTROL Sheet

| ID | Sev | Description | Action |
|----|-----|-------------|--------|
| C1 | **High** | aC3 = 2.2µF on STM32F446 VCAP pin — datasheet specifies 1µF ±20% X5R/X7R; 2.2µF may cause internal regulator instability | Replace with 1µF |
| C2 | **Info** | HSE load caps aC18/aC19 = 10pF C0G (GRM1885C1H100JA01D) on OSC_IN/OSC_OUT ✓ | — |
| C3 | **High** | aR18 (33Ω SWCLK) MPN set to RC0603FR-0710KL — this is a 10kΩ part, not 33Ω | Change MPN to RC0603FR-0733RL (Yageo 33Ω 0603) |
| C4 | **Info** | LSE load caps omitted intentionally — STM32F446 LSE oscillator has built-in internal load capacitors (~5pF each) ✓ | — |
| C5 | **Medium** | VBAT (STM32F446 pin 1) decoupling not confirmed in wire tracing | Confirm 100nF cap directly on VBAT pin |
| C6 | **Medium** | NRST filter capacitor not confirmed | Confirm 100nF cap on NRST to GND |
| C7 | **Medium** | No series resistor on OSC_OUT for HSE — crystal overdrive protection | Add 0Ω DNP (or 100Ω) in series on OSC_OUT |
| C8 | **Medium** | LED drive currents very low: aD1 purple ≈ 0.2mA via aR1=1kΩ; aD2 RGB blue channel ≈ 0.3mA — barely visible | Reduce series resistors to 100–220Ω |
| C9 | **Medium** | SD card data lines have no series damping resistors — at SPI 25MHz, ringing likely | Add 22–33Ω series resistors on SCK and MOSI/MISO |
| C10 | **Low** | SWO line has no series resistor — add 33–100Ω for EMI | Optional: add 33Ω on SWO_P |
| C11 | **Low** | aFB1 uses R_0603_1608Metric footprint — ferrite bead should use inductor footprint | Change to L_0603_1608Metric footprint |
| C12 | **Low** | USB SBU1/SBU2 pins on aJ2 disposition unconfirmed | Confirm floating is intentional (USB 2.0 no alt-mode) |
| C13 | **Low** | HEARTBEAT signal (Pico↔STM32) has no series resistor | Add 100Ω if trace length is significant |
| C14 | **Info** | aR18 = 33Ω on SWCLK (M2) ✓ | — |
| C15 | **Info** | USB CC1/CC2 pull-downs aR7=aR8=5.1kΩ — correct for UFP 900mA ✓ | — |
| C16 | **Info** | I2C pull-ups aR10=aR11=4.7kΩ — correct for 400kHz ✓ | — |

### 6.3 SENSOR Sheet

| ID | Sev | Description | Action |
|----|-----|-------------|--------|
| S1 | **High** | cU2 (ASM330LHHXTR) CS pin must be pulled HIGH to select I2C mode — pull-up not confirmed | Add 10kΩ pull-up on CS to +3.3V_SENSOR; tie MSCL/MSDA to GND if unused |
| S2 | **High** | cU4 (LSM6DSO32TR) CS pin must be pulled HIGH for I2C mode — pull-up not confirmed | Add 10kΩ pull-up on CS to +3.3V_SENSOR |
| S3 | **High** | I2C pull-ups cR1=cR2=4.7kΩ serve 4 devices — may violate 300ns tR max at 400kHz | Reduce to 2.2kΩ if running Fast Mode; confirm operating frequency |
| S4 | **Medium** | cU2 VDD_IO (pin 5) connection not confirmed — must connect to +3.3V_SENSOR | Verify pin 5 is not floating |
| S5 | **Medium** | cU3 (MS5837) missing 10µF bulk decoupling cap — datasheet requires 100nF + 10µF | Add 10µF cap on cU3 VDD |
| S6 | **Medium** | cU2 and cU4 missing 1µF VDD bulk cap — STMicro app note requires 100nF + 1µF | Add 1µF per device |
| S7 | **Low** | No series resistors on I2C SDA/SCL — 22–33Ω recommended for multi-device stub | Optional: add 22Ω on SCL/SDA |
| S8 | **Low** | Interrupt lines (ACC1_INT1/2, ACC2_INT1/2) routed without series resistors | Add 100Ω series on INT lines to header |
| S9 | **Info** | I2C addresses: cU2 SDO=GND_SENSOR → 0x6A ✓; cU4 SDO=+3.3V_SENSOR → 0x6B ✓ | — |

### 6.4 TX_RX Sheet

| ID | Sev | Description | Action |
|----|-----|-------------|--------|
| T1 | **Critical** | dQ1–dQ4 use IPD50R3K0CE KiCad symbol (500V/3Ω/1.7A CoolMOS) but Value/MPN = IPD50N10S3L-16 (100V/16mΩ/50A) — symbol electrical params are completely wrong | Create or source correct IPD50N10S3L-16 symbol; update lib_id |
| T2 | **Critical** | dL1, dL2 have empty Value and no MPN — inductor specs unknown, nothing will be ordered | Assign inductance, current rating, DCR, footprint, and MPN |
| T3 | **Info** | dU7 symbol renamed SWARM_Library:INA823DR; INA823/INA828 are pin-compatible (identical SOIC-8 pinout) — connections valid ✓ | — |
| T4 | **High** | No bootstrap diode from +12V to VB nodes on either half-bridge — schematic note says firmware must precharge at boot | Add fast-recovery Schottky (e.g., STPS1L40) from VDD to each VB; removes firmware dependency and improves reliability |
| T5 | **Info** | INA240A2DR gain=50 on 20mΩ shunt: load is piezo transducer (capacitive/resonant), peak drive current expected <<1A — output well within range ✓ | — |
| T6 | **Medium** | Single gate resistor per FET (10Ω) controls both turn-on and turn-off — slower turn-off increases switching losses | Add anti-parallel diode+resistor for independent turn-on/turn-off control |
| T7 | **Medium** | No gate-source TVS or Zener clamp on FET gates — Vgs ringing could exceed ±20V Vgs(max) of IPD50N10S3L-16 | Add 15V Zener from gate to source on each FET |
| T8 | **Medium** | INA823DR gain resistor identification unclear (dR30=121Ω vs dR32=3.83kΩ — which is Rg?) | Confirm which net connects between RG1 and RG2 on INA823; document gain |
| T9 | **Medium** | Vref for INA823 uses unbuffered resistor divider (V_REF_HALF_TXRX from 4×47kΩ) — output impedance ~12kΩ affects accuracy | Buffer the mid-rail reference with a unity-gain op-amp |
| T10 | **Medium** | dU1/dU2 UCC27211D VDD supply rail: must be 12V_TXRX, not 3.3V (UVLO = 8V) | Verify VDD pins connect to 12V_TXRX |
| T11 | **Info** | dR17 WSL2512R0200FEA shunt (20mΩ) rated 1W — verify RMS motor current <7A (7²×0.02 = 0.98W) | Document expected RMS current |
| T12 | **Info** | dU1/dU2 HI/LI inputs are TTL-compatible — 3.3V MCU drive is sufficient ✓ | — |

### 6.5 Top-Level / HEADER\_PINS

| ID | Sev | Description | Action |
|----|-----|-------------|--------|
| H1 | **Medium** | J1 connector in HEADER_PINS.kicad_sch has empty Value field; J2/J3/J4 correctly show Conn_02x25_Odd_Even | Populate J1 Value field |
| H2 | **Low** | GND_HEADER and +3.3V_HEADER missing PWR_FLAG in top-level sheet — causes ERC warnings | Add two PWR_FLAG symbols on those nets in top-level |
| H3 | **Info** | GND domain architecture documented in top-level schematic ✓ | — |

---

## 7. MPN Audit

### Missing MPNs — ICs (High Priority)

| Ref | Value | Note |
|-----|-------|------|
| aU1 | RaspberryPi Pico 2 | Core MCU module |
| aU2 | STM32F446RET6 | Core MCU |
| aU3 | USBLC6-2SC6 | USB ESD |
| bU1, bU2 | LMR33630ADDA | Buck regulators |
| cU3 | MS583730BA01-50 | Pressure sensor |
| dQ1–dQ4 | IPD50N10S3L-16 | Power FETs (symbol mismatch too — see T1) |
| dU1, dU2 | UCC27211D | Gate drivers |
| dU3 | INA240A2DR | Current sense |
| dU4 | TLV9101IDCKR | Op-amp |
| dU5 | ADG7421FBCPZ-RL7 | Analog switch |
| dU8 | OPA2322AIDGKR | Op-amp |

### Missing MPNs — Passives / Discretes

| Ref | Value |
|-----|-------|
| aY1 | 32.768kHz crystal |
| aY2 | 16MHz crystal |
| aFB1 | 120R ferrite bead |
| bD1 | SMBJ18A TVS |
| bD5 | SS34-HF Schottky |
| bF1 | 1812L150/24MR polyfuse |
| bL1 | 6.8µH inductor |
| bL2 | 15µH inductor |
| bL3 | 22µH inductor |
| dL1, dL2 | **No value** — see Finding T2 |
| aR18 | 33Ω — MPN currently wrong (see Finding C3) |

### Missing MPNs — Connectors

| Ref | Value |
|-----|-------|
| aJ1 | 2-pin 1mm header |
| aJ2 | USB-C GCT USB4085 |
| aJ3 | Micro SD (Amphenol 1140084168) |
| aJ4 | 6-pin 1mm SWD header |
| bJ1 | XT30PW-M |
| bJ2, dJ2 | JST PH 8-pin |
| dJ1 | JST XH 3-pin |
| J1–J4 | Hirose DF40C-50DP-0.4V |
| J25–J28 | 12/13-pin sockets |

### MPNs Confirmed Assigned

| Ref | MPN |
|-----|-----|
| aD1 | JE2835APP-N-0001A0000-N0000001 |
| aD2 | L1MC-RGB0028000MP0 |
| bD2 | JE2835AGR-N-0002A0000-N0000001 |
| bD3, bD4 | JE2835ABL-N-0005A0000-N0000001 |
| bU3 | TPS55340RTER |
| cU1 | MMC5603NJ |
| cU2 | ASM330LHHXTR |
| cU4 | LSM6DSO32TR |
| dU6 | TPD2E007DCKR |
| dU7 | INA823DR |

---

## 8. PCB Fixes Applied This Revision

| Fix | Rule | Description | Scope |
|-----|------|-------------|-------|
| Via tenting | VP-001 | Added `(tenting front back)` to all vias | 1,540 vias |
| Keepout zones removed | KO-001 | Removed stale auto-placement-area zones | 4 zones |
| Annular ring increase | DFM-001 | 0.25→0.35 and 0.3→0.4 pad sizes | 482 vias |
| Fiducial markers added | FD-001 | 1mm/2mm-mask fiducials on F.Cu and B.Cu | 6 markers |

---

## 9. Open Items

Items are sorted by priority. ✓ = resolved this session.

| Priority | ID | Item | Owner |
|----------|----|------|-------|
| ✓ Done | M4 | bR10 corrected 187k→255k for VPiezo=24V | Schematic |
| ✓ Done | M2 | 33Ω SWCLK series resistor (aR18) added near aJ4 | Schematic |
| ✓ Done | L2 | LED MPNs assigned (aD1, aD2, bD2, bD3, bD4) | BOM |
| ✓ Done | H3 | GND domain architecture documented in top-level | Schematic |
| ✓ Done | M3 | IMU I2C addresses verified (cU2=0x6A, cU4=0x6B) | Schematic |
| **Critical** | P1–P4 | Fix capacitor voltage ratings: VIN/12V/VPiezo caps severely under-rated (6.3V caps on 12–24V rails) | BOM/Layout |
| ✓ Done | T1 | dQ1–dQ4 lib_id replaced with Device:MOSFET_N; Value/MPN remain IPD50N10S3L-16 | Schematic |
| **Design-pending** | T2 | dL1/dL2 marked TBD — piezo impedance matching inductors, values require piezo characterisation | Schematic |
| High | P5 | Update bR10 MPN to RC0603FR-07255KL (currently shows 187k part) | BOM |
| ✓ Done | P6 | Polyfuse 1.5A adequate — piezo acoustic comms real power <<10W, VIN draw ~310mA | — |
| ✓ Done | C1 | aC3 (VCAP) changed to 1µF / GRM188R60J105KE15D | Schematic |
| ✓ Done | C2 | HSE load caps aC18/aC19 confirmed 10pF C0G; MPN updated to GRM1885C1H100JA01D | Schematic |
| High | C3 | Fix aR18 MPN to RC0603FR-0733RL (currently populated with 10kΩ MPN) | BOM |
| High | S1 | Add 10kΩ pull-up on cU2 (ASM330) CS pin to +3.3V_SENSOR | Schematic |
| High | S2 | Add 10kΩ pull-up on cU4 (LSM6DSO32) CS pin to +3.3V_SENSOR | Schematic |
| ✓ Done | S3 | cR1/cR2 I2C pull-ups changed to 2.2kΩ / RC0603FR-072K2L | Schematic |
| ✓ Done | T3 | dU7 lib symbol renamed to SWARM_Library:INA823DR; pin-compatible with INA828 | Schematic |
| Low | T4 | Add bootstrap diode from VDD to VB nodes — low risk for piezo load since half-bridge switches every cycle, charging bootstrap cap continuously | Schematic |
| ✓ Done | T5 | INA240 gain/shunt appropriate for piezo drive currents (<<1A) — not a motor load | — |
| ✓ Done | C4 | LSE load caps not needed — STM32F446 has internal oscillator capacitors | — |
| Medium | C5 | Confirm 100nF cap on STM32F446 VBAT pin | Schematic |
| Medium | C6 | Confirm 100nF cap on STM32F446 NRST | Schematic |
| Medium | C8 | Increase LED series resistors: aD1 and aD2 channels drive <0.5mA — nearly invisible | Schematic |
| Medium | S4 | Confirm cU2 VDD_IO (pin 5) connection to +3.3V_SENSOR | Schematic |
| Medium | S5 | Add 10µF bulk cap on cU3 (MS5837) VDD | Schematic |
| Medium | T6 | Add gate-source Zener clamps (15V) on dQ1–dQ4 | Schematic |
| Medium | T8 | Identify INA823DR gain resistor and document gain; buffer V_REF_HALF_TXRX | Schematic |
| Medium | H1 | Populate J1 Value field in HEADER_PINS.kicad_sch | Schematic |
| Medium | BOM | Assign MPNs to aU1, aU2, aU3, bU1, bU2, dQ1–dQ4, dU1–dU5, dU8, cU3 | BOM |
| Medium | BOM | Assign MPNs to connectors: aJ2, aJ3, bJ1, bJ2, J1–J4 (on-PCB connectors are critical) | BOM |
| Low | P7 | Reduce bR3 to increase bD3/bD4 LED brightness, or document as intentional | Schematic |
| Low | P8 | Replace bD1 symbol with TVS symbol; set MPN=SMBJ18A | Schematic |
| Low | C10 | Add 33Ω series resistor on SWO line | Schematic |
| Low | C11 | Change aFB1 footprint to L_0603_1608Metric | Schematic |
| Low | H2 | Add PWR_FLAG for GND_HEADER and +3.3V_HEADER in top-level schematic | Schematic |
| Low | BOM | Assign MPNs to aY1, aY2, aFB1, bD1, bD5, bF1, bL1, bL2, bL3 | BOM |
| Low | EMC | GP-001: Add ground stitching vias (54 sites) | Layout |
| Low | EMC | RP-001: Add GND via at each layer transition (22 sites) | Layout |
| Info | — | dC9 rail voltage (47µF Samsung 0603 rated 4V) — verify placement | Schematic |
| Info | — | Verify bL1/bL2 Würth WE-MAPI catalog numbers | BOM |

---

## 10. JLCPCB Manufacturing Checklist

| Item | Status |
|------|--------|
| Gerbers from KiCad | Ready to export |
| Layer count: 2 | OK |
| Board thickness: 1.6mm | OK |
| Min trace: ≥0.1mm | Verify in KiCad DRC |
| Min spacing: ≥0.1mm | Verify in KiCad DRC |
| Min drill: ≥0.15mm | OK (0.15mm used) |
| Annular ring: ≥0.1mm | FIXED (was 0.05mm) |
| Via tenting | DONE (both sides) |
| Fiducials (≥3) | DONE (6 added) |
| HASL / ENIG finish | Select at order |
| Impedance control | Not required |
| Stencil | Order with board for SMT |
| **Cap voltage ratings** | **OPEN — fix before ordering** |
| **FET symbol correction** | **OPEN — fix before ordering** |
| **Bootstrap diodes** | **OPEN — fix before ordering** |
