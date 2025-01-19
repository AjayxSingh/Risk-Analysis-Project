# Expected Loss Modeling

This repository provides an overview and calculation methodology for estimating **Expected Loss (EL)** using the formula:

\[ \text{Expected Loss (EL)} = \text{EAD} \times \text{PD} \times \text{LGD} \]

### Key Components

#### 1. **EAD (Exposure at Default)**
The **Exposure at Default** represents the total exposure the lender has when a borrower defaults.

- **UGD (Usage Given Default):**
  - The percentage of the committed yet undrawn balance assumed to be drawn in case of default.
  - Formula:
    \[
    \text{EAD} = \text{Outstanding Bonds} + \text{Unused Commitment} \times \text{UGD}
    \]
- **Example Calculation:**
  - Outstanding Bond Notional: **500M**
  - Unused Commitment: **500M**
  - UGD: **65%**
  - \[
    \text{EAD} = 500M + 500M \times 0.65 = 825M
    \]

#### 2. **PD (Probability of Default)**
The **Probability of Default** is calculated using the **Merton Model**. The required parameters are:

- **Firm Value (Total Assets):** 19.57
- **Expected Return:** 6% (historical average return)
- **Time Horizon:** 1 year
- **Volatility:** 44.7% (historical asset level)
- **Short-Term Liabilities:** 8.38M
- **Long-Term Liabilities:** 20.38M
- **Default Point:** Sum of liabilities exceeding **12.5M**

**Distance to Default Formula:**
\[
\text{Distance to Default} = \frac{\ln\left(\frac{\text{Firm Value}}{\text{Default Point}}\right) + (\text{Expected Return} - \frac{\text{Volatility}^2}{2}) \times \text{Time}}{\text{Volatility} \times \sqrt{\text{Time}}}
\]

**Example:**
- \[
  \text{Distance to Default} = \frac{\ln(19.57 / 12.5) + (0.06 - (0.447^2)/2) \times 1}{0.447 \times \sqrt{1}} = \text{Calculated Value}
  \]
- \[
  \text{PD} = \text{Normal Distribution}(-\text{Distance to Default}) = 13.85\%
  \]

#### 3. **LGD (Loss Given Default)**
The **Loss Given Default** represents the percentage of exposure that will not be recovered in case of default. It is modeled using a **Beta Distribution**.

**Key Variables:**
- **avg_LGD_on_bonds:** Average LGD on bonds.
- **std:** Standard deviation of the LGD values.
- **max_for_bonds:** Maximum allowable value for LGD in calculations.

**Calculation:**
- **alpha** and **beta** are derived from average LGD, standard deviation, and maximum value.
- **Mean Recovery Rate:** Represents the recovery percentage.
- \[
  \text{LGD} = \text{Calculated as } 48.75\%
  \]

#### 4. **Expected Loss (EL)**
Finally, the Expected Loss is calculated using:
\[
\text{EL} = \frac{\text{EAD} \times \text{PD} \times \text{LGD}}{100 \times 100}
\]

**Example Calculation:**
- **EAD:** 825M
- **PD:** 13.85%
- **LGD:** 48.75%
- \[
  \text{EL} = \frac{825M \times 13.85 \times 48.75}{100 \times 100} = \$55,710,091.76
  \]

---

### Repository Structure
- **README.md**: Documentation and explanation of the EL calculation methodology.
- **Scripts/**: Python/R scripts for automating the calculations.
- **Examples/**: Sample data and worked-out examples.

### Prerequisites
- Basic understanding of financial terms such as EAD, PD, and LGD.
- Familiarity with statistical distributions (e.g., Beta Distribution).
- Software tools such as Python, R, or Excel for implementing the formulas.

---

### Use Cases
- **Credit Risk Assessment:** Estimating potential losses for financial institutions.
- **Regulatory Compliance:** Meeting Basel III or other regulatory requirements.
- **Portfolio Management:** Managing risk and optimizing returns.

### References
- Moody’s Model for Loss Given Default.
- Merton Model for Probability of Default.
- Historical Financial Data for Volatility and Expected Returns.


