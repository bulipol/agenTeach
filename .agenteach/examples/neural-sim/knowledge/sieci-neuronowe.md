# Sieci Neuronowe

> Status: ✅ omówione — pojedynczy neuron, warstwy, funkcje aktywacji, dwuwarstwowy MLP, dobór rozmiarów architektury

---

## Czym jest sieć neuronowa

Sieć neuronowa to **funkcja** `f(x) → y`. Zamienia liczby wejściowe na liczby wyjściowe zgodnie ze swoimi wagami.

W symulacji: `x = co agent widzi` (hunger, dist, dx, dy...), `y = co agent robi` (vx, vy).

---

## Pojedynczy neuron

```
wynik = tanh( w1*x1 + w2*x2 + ... + bias )
```

**Przykład liczbowy:**
```
x1 = hunger = 0.8,  x2 = dist = 0.3
w1 = 2.0,  w2 = -1.0,  bias = -0.5

w1 * x1 =  2.0 * 0.8 =  1.6
w2 * x2 = -1.0 * 0.3 = -0.3
bias    =              -0.5
                       ----
suma ważona =           0.8  → tanh(0.8) ≈ 0.664
```

---

## Warstwa = kilka neuronów równolegle

```
Wejście: [hunger=0.8, dist=0.3]

Neuron A:  0.73*0.8 - 1.28*0.3 + 0.44 = 0.64
Neuron B: -0.20*0.8 + 0.90*0.3 - 0.10 = 0.01
Neuron C:  1.50*0.8 + 0.10*0.3 + 0.00 = 1.23

Wyjście: [tanh(0.64), tanh(0.01), tanh(1.23)] ≈ [0.57, 0.01, 0.84]
```

---

## Dlaczego 2 warstwy?

Jeden neuron = linia prosta. Nie potrafi nauczyć się logiki AND ("głodny I blisko").

Dwie warstwy: warstwa 1 sprawdza warunki osobno, warstwa 2 łączy wyniki.

---

## Architektura sieci agenta (Etap 1)

```
Wejścia: 4  [dx_food, dy_food, dist_food, energia]
Ukryta:  8 neuronów  (2 × n_wejść)
Wyjście: 2  [vx, vy]
```

---

## Dziennik nauki

Chronologiczny zapis procesu nauki. Agent używa tych wpisów do planowania przyszłych pytań i wyjaśnień.

(Brak wpisów — śledzenie rozpoczęte od 2026-02-26)
