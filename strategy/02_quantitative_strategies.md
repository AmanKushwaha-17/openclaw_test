# Intraday Gold Trading: Quantitative Strategies

This document outlines strategies that are more data-driven and systematic, often forming the basis for algorithmic trading models.

---

## 1. Statistical Arbitrage: Gold-Silver Ratio Mean Reversion

**Archetype:** Mean Reversion / Relative Value

**Core Concept:** Gold (XAUUSD) and Silver (XAGUSD) are highly correlated assets. However, their price relationship, known as the Gold-Silver Ratio (GSR), fluctuates. This strategy assumes that the GSR has a long-term historical mean and that significant deviations from this mean will eventually revert back. Traders do not bet on the direction of gold or silver, but on the direction of the ratio itself.

**Key Elements:**
- **Gold-Silver Ratio (GSR):** Calculated by dividing the price of one ounce of gold by the price of one ounce of silver. `GSR = Price(XAUUSD) / Price(XAGUSD)`.
- **Historical Mean & Standard Deviation:** A lookback period (e.g., 200-period moving average of the GSR) is used to establish a "normal" or mean value for the ratio. The standard deviation of the ratio over this period is calculated to identify what constitutes a significant deviation.
- **Z-Score:** A Z-score can be calculated to standardize the deviation: `Z-score = (Current GSR - Mean GSR) / Standard Deviation`. This tells us how many standard deviations away from the mean the current ratio is.

**Execution:**
The strategy is executed by simultaneously taking opposing positions in gold and silver, with position sizes adjusted for their different dollar values (dollar-neutral).

- **Entry (Short the Ratio):**
    - **Signal:** The GSR moves significantly *above* its historical mean (e.g., a Z-score > 2.0). This implies gold is overvalued relative to silver.
    - **Action:** Simultaneously **SELL** Gold (XAUUSD) and **BUY** Silver (XAGUSD).

- **Entry (Long the Ratio):**
    - **Signal:** The GSR moves significantly *below* its historical mean (e.g., a Z-score < -2.0). This implies gold is undervalued relative to silver.
    - **Action:** Simultaneously **BUY** Gold (XAUUSD) and **SELL** Silver (XAGUSD).

- **Exit (Take-Profit):**
    - The position is closed when the GSR reverts back to its historical mean (e.g., the Z-score returns to 0).

- **Stop-Loss:**
    - A stop-loss can be placed if the ratio moves further away to an extreme level (e.g., a Z-score of 3.0 or -3.0). This protects against a fundamental shift in the relationship between the metals.

**Important Note:** This is a market-neutral strategy. A successful trade makes a profit regardless of whether the overall precious metals market went up or down, as long as the ratio reverts to its mean.
