# BESS-using-Solar-PV-Array
A Battery Energy Storage system using Solar PV array with the help of Boost converter

This system is a 2-STAGE DC-DC power conversion architecture designed for renewable energy microgrids.
1. Stage 1 (Boost Converter): Steps up the variable, low voltage from the Solar PV array (150V) to a stable, elevated intermediate DC-bus voltage (270V to 300V) close to 300 V
2. Stage 2 (Half-Bridge Converter): Operates bidirectionally. When solar generation is high, it operates in Buck mode to step down the DC-bus voltage to smoothly charge the battery (160V). When solar generation drops, it seamlessly switches to Boost mode to extract power from the battery and support the central DC-bus load.

## 2. Design Formulas

### 2.1 Stage 1: PV Boost Converter Sizing

#### 2.1.1 Duty Cycle of the Boost Converter

D_boost = 1 - (V_in / V_out)

**Where:**

- V_in = Solar input voltage (V)
- V_out = Required boost converter output voltage (V)

---

#### 2.1.2 Boost Inductor Selection

L_boost = (V_in × D_boost) / (ΔI_L × f_s)

**Where:**

- V_in = Solar input voltage (V)
- D_boost = Boost converter duty cycle
- ΔI_L = Peak-to-peak inductor current ripple (A)
- f_s = Switching frequency (Hz)

---

#### 2.1.3 PV Input Capacitor Selection

C_in_pv = (I_out × D_boost) / (ΔV_in × f_s)

**Where:**

- I_out = Boost converter output current (A)
- D_boost = Boost converter duty cycle
- ΔV_in = Allowed PV input voltage ripple (V)
- f_s = Switching frequency (Hz)

---

### 2.2 Intermediate DC-Link Design

#### 2.2.1 DC-Link Capacitor Selection

C_dc_link = (I_load × D_max) / (ΔV_out × f_s)

**Where:**

- I_load = Load current (A)
- D_max = Maximum converter duty cycle
- ΔV_out = Allowed DC-link voltage ripple (V)
- f_s = Switching frequency (Hz)

---

#### 2.2.2 Load Resistance Calculation

R_load = (V_dc²) / P_load

**Where:**

- V_dc = DC-link voltage (V)
- P_load = Total load power (W)

---

### 2.3 Stage 2: Synchronous Half-Bridge Converter Sizing

#### 2.3.1 Charging Duty Cycle

D_hb = V_batt / V_out

**Where:**

- V_batt = Battery bank voltage (V)
- V_out = DC-link voltage (V)

---

#### 2.3.2 Battery Filter Inductor Selection

L_batt = ((V_out - V_batt) × D_hb) / (ΔI_batt × f_s)

**Where:**

- V_out = DC-link voltage (V)
- V_batt = Battery bank voltage (V)
- D_hb = Half-bridge duty cycle
- ΔI_batt = Battery charging current ripple (A)
- f_s = Switching frequency (Hz)

---

### 2.4 Closed-Loop PI Controller

#### 2.4.1 PI Controller Transfer Function

G_c(s) = K_p + (K_i / s)

**Where:**

- K_p = Proportional gain
- K_i = Integral gain
- s = Laplace complex frequency variable

# 3. Primary Commercial Applications

## 3.1 Solar PV Energy Storage Systems (ESS)

In standard grid-tied or off-grid solar power systems, solar panels cannot directly charge a battery bank efficiently or safely.

### The Problem

- Solar panel output voltage varies continuously with solar irradiance and temperature.
- Batteries require a regulated charging voltage and current to prevent overcharging, overheating, and reduced battery life.

### Proposed Solution

- **Stage 1 (Boost Converter):** Converts the variable PV voltage (approximately **150 V**) into a stable high-voltage DC bus (**270–300 V**).
- **Stage 2 (Synchronous Half-Bridge Converter):** Steps the DC bus voltage down to the required battery charging voltage (**160 V**) while providing controlled charging current.

This two-stage architecture ensures efficient power extraction from the PV array and safe battery charging.

---

## 3.2 Electric Vehicle (EV) Regenerative Fast-Charging Stations

The proposed converter topology is well suited for modern EV charging infrastructure.

### Forward Power Flow

PV Array → Boost Converter → DC Bus → Half-Bridge Converter → EV Battery

### Bidirectional Operation

Because the half-bridge converter is bidirectional, power can also flow in the reverse direction.

Battery → Half-Bridge Converter → DC Bus → External Load / Grid

This enables:

- Vehicle-to-Grid (V2G) operation
- Peak load management
- Renewable energy integration
- Backup power support

---

## 3.3 Uninterruptible Power Supplies (UPS) and Data Centers

Modern data centers rely on uninterrupted DC power for continuous operation.

### Proposed System Operation

- During normal operation, the boost converter harvests renewable energy and maintains the DC bus.
- The half-bridge converter continuously charges the battery bank.
- During a power outage, the converter instantly reverses power flow and supplies stored battery energy to the DC bus.
- The transition occurs rapidly, allowing uninterrupted power delivery to critical loads.

This makes the converter suitable for online UPS and energy backup applications.

---

# 4. Academic and Engineering Contributions

The proposed model demonstrates several important concepts in modern power electronics.

## 4.1 Decoupled Two-Stage Converter Architecture

- Separates the PV generation stage from the battery charging stage.
- Improves stability by isolating the switching dynamics of both converters.
- Enables independent control of the PV source and battery load.

---

## 4.2 Synchronous Rectification

- Uses complementary MOSFET switching instead of conventional diode rectification.
- Reduces conduction losses.
- Improves converter efficiency.
- Minimizes thermal stress in practical hardware implementations.

---

## 4.3 Closed-Loop PI Control

- Employs a PI controller for automatic regulation of the converter output.
- Reduces startup transients and overshoot.
- Maintains stable battery charging conditions.
- Provides steady-state operation under varying load and input conditions.

The closed-loop control system ensures reliable converter performance and improved dynamic response.
