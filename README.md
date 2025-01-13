# How does it work? | Как это работает?

## 1. Function `calculate_rtp_optimized`

This function calculates the RTP (Return to Player) for a given distribution of symbols on the reels. The calculation is based on the probability of symbols appearing and their respective payouts.

### Main Formula
```
RTP = Σ (P(s)^3 * Payout(s)), where s ∈ S
```

Where:
- **s** — a symbol from the set of all symbols **S**.
- **P(s)** — the probability of symbol **s** appearing on a single reel:
  ```
  P(s) = Number of symbol s / Total number of reel slots
  ```
- **P(s)^3** — the probability of symbol **s** appearing simultaneously on all three reels.
- **Payout(s)** — the payout for three matching symbols of **s**.

### Summary
The function sums the contribution of each symbol, multiplying the probability of the combination by the corresponding payout, and returns the RTP as a percentage.

---

## 2. Function `probability_weighted_adjustment`

This function distributes symbols on the reels based on their payouts so that higher-paying symbols appear less frequently. It uses the principle of inversely proportional probability to payouts.

### Key Idea
If a symbol **s** has a high payout, its quantity on the reels is reduced so that its probability (**P(s)**) is lower. This reduces the overall RTP, helping to balance the system.

### Steps

#### 1. Proportional Distribution
```
Number of symbol s = floor((Payout(s) / Σ Payout(s)) * Reel size)
```

#### 2. Weight Adjustment
The weight of a symbol is considered so that less frequently paid symbols appear more often:
```
Number of symbol s * (1 - Weight)
```

Where weight:
```
Weight = Payout(s) / Σ Payout(s)
```

#### 3. Reel Size Adjustment
The total number of symbols must match the reel size. Adjustments are made to eliminate any differences.

---

## 3. Function `refine_rtp_to_target`

This function fine-tunes the distribution of symbols on the reels to achieve a target RTP.

### Key Idea
The RTP is increased or decreased by adjusting the number of symbols:
- If the current RTP is higher than the target, the count of high-payout symbols is reduced.
- If the current RTP is lower than the target, the count of low-payout symbols is increased.

### Algorithm

1. Calculate the current RTP using `calculate_rtp_optimized`.
2. If `RTP_current > RTP_target`:
   - Reduce the count of symbols with high payouts.
3. If `RTP_current < RTP_target`:
   - Increase the count of symbols with low payouts.
4. The adjustments continue until the difference between the current and target RTP is within a defined tolerance.

---

# Conclusion

These functions rely on fundamental probability principles:
- Calculating the probabilities of symbols on reels.
- Optimizing the symbol distribution to achieve a target RTP.
- Iteratively refining values to minimize error.



------
### rus


## 1. Функция `calculate_rtp_optimized`

Эта функция рассчитывает RTP (Return to Player) для заданного распределения символов на барабанах. Основой является вероятность выпадения символов и их выплаты.

### Основная формула
```
RTP = Σ (P(s)^3 * Payout(s)), где s ∈ S
```

Где:
- **s** — символ из множества всех символов **S**.
- **P(s)** — вероятность появления символа **s** на одном барабане:
  ```
  P(s) = Количество символов s / Общее количество ячеек на барабане
  ```
- **P(s)^3** — вероятность того, что символ **s** выпадет одновременно на всех трёх барабанах.
- **Payout(s)** — выплата за три совпадающих символа **s**.

### Итог
Функция суммирует вклад каждого символа, умножая вероятность выпадения комбинации на соответствующую выплату, и возвращает RTP в процентах.

---

## 2. Функция `probability_weighted_adjustment`

Эта функция распределяет символы на барабанах на основе их выплат так, чтобы более дорогие символы выпадали реже. Используется принцип обратной пропорциональности вероятности к выплате.

### Основная идея
Если символ **s** имеет высокую выплату, его количество на барабанах уменьшается, чтобы вероятность его выпадения (**P(s)**) была меньше. Это снижает общий RTP, помогая сбалансировать систему.

### Шаги

#### 1. Пропорциональное распределение
```
Количество символов s = floor((Payout(s) / Σ Payout(s)) * Размер барабана)
```

#### 2. Коррекция веса
Учитывается вес символа, чтобы реже выплачиваемые символы выпадали чаще:
```
Количество символов s * (1 - Вес)
```

Где вес:
```
Вес = Payout(s) / Σ Payout(s)
```

#### 3. Согласование с размером барабана
Общая сумма всех символов должна совпадать с размером барабана. Вносятся корректировки, чтобы устранить разницу.

---

## 3. Функция `refine_rtp_to_target`

Эта функция уточняет распределение символов на барабанах, чтобы достигнуть целевого RTP.

### Основная идея
RTP увеличивается или уменьшается путём регулирования количества символов:
- Если текущий RTP выше целевого, уменьшаются символы с высокими выплатами.
- Если текущий RTP ниже целевого, увеличиваются символы с низкими выплатами.

### Алгоритм

1. Вычисляется текущий RTP с помощью `calculate_rtp_optimized`.
2. Если `RTP_текущий > RTP_целевой`:
   - Уменьшается количество символов с высокими выплатами.
3. Если `RTP_текущий < RTP_целевой`:
   - Увеличивается количество символов с низкими выплатами.
4. Проверка продолжается, пока разница между текущим и целевым RTP не станет меньше заданного допуска (`tolerance`).

---

# Вывод

Функции опираются на базовые принципы теории вероятностей:
- Вычисление вероятностей для символов на барабанах.
- Оптимизация распределения символов для достижения целевого RTP.
- Итеративная корректировка значений для минимизации ошибки.

