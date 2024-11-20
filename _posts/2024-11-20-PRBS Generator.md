---
layout: post
title: PRBS Generator
math: true
date: 2024-11-20 00:02 +0100
---

A PRBS (Pseudo-Random Binary Sequence) has a close-to-white PSD, thus is suitable for testing a serial link under random data inputs. Since it can create a sequence of length $$ 2^N-1 $$ using only N registers and some XOR gates, it is widely used for implementing pattern generators for link testing.

A PRBS-N generator consists of N shift registers. Certain outputs, or taps, of the registers are XORed and fed back to the input, forming a feedback. Shown below is an example of PRBS-7 generator. Since multiple primitive polynomials may exist for a given N, different PRBS sequences may exist for PRBS-N. Note that XOR should be more precisely described as GF(2) addition.

LFSR can either have an external feedback, or an internal feedback. The benefits of internal feedback is that the critical path is shorter when multiple taps are XORed to form a feedback (operates at higher frequency). But since popular PRBS have just two taps (ex. PRBS15, PRBS31), using external is not too bad (i think).

Below are some primitive polynomials that are used for BER testing (source: Anritsu MU195040A operation manual). Simulations should be made with the below sequences rather than other polynomials.

| Order | Polynomial                  | Length                      |
| ----- | --------------------------- | --------------------------- |
| 7     | $$ 1+X^6+X^7 $$             | $$ 2^7-1 = 127 $$           |
| 9     | $$ 1+X^5+X^9 $$             | $$ 2^9-1 = 511 $$           |
| 10    | $$ 1+X^7+X^{10} $$          | $$ 2^{10}-1 = 1023 $$       |
| 11    | $$ 1+X^9+X^{11} $$          | $$ 2^{11}-1 = 2047 $$       |
| 13    | $$ 1+X+X^2+X^{12}+X^{13} $$ | $$ 2^{13}-1 = 8191 $$       |
| 15    | $$ 1+X^{14}+X^{15} $$       | $$ 2^{15}-1 = 32767 $$      |
| 20    | $$ 1+X^{3}+X^{20} $$        | $$ 2^{20}-1 = 1048575 $$    |
| 23    | $$ 1+X^{18}+X^{23} $$       | $$ 2^{23}-1 = 8388607 $$    |
| 31    | $$ 1+X^{28}+X^{31} $$       | $$ 2^{31}-1 = 2147483647 $$ |

Cadence analogLib offers vprbs. Note that default taps of some prbs can be different from the above polynomials (ex. PRBS20). The behavioral model of PRBS in analogLib is shown below.

For PAM-4 signals, there are some standards that define test sequences. PRQS10 and QPRBS13 seem good enough. PRBQS10 is two parallel PRBS20 blocks that are time-shifted by 10 symbols. PRQS13 is PRBS13 shifting two registers per symbol, outputing two bits per symbol.


<!-- Block math, keep all blank lines -->

$$
a^2+b^2=c^2
$$

<!-- Equation numbering, keep all blank lines  -->

$$
\begin{equation}
  e=mc^2
  \label{eq:label_name}
\end{equation}
$$

Can be referenced as \eqref{eq:label_name}.

<!-- Inline math in lines, NO blank lines -->

"Lorem ipsum dolor sit amet, $$ a^2+b^2=c^2 $$ consectetur adipiscing elit."

<!-- Inline math in lists, escape the first `$` -->

1. \$$ a^2+b^2=c^2 $$
2. \$$ a^2+b^2=c^2 $$
3. \$$ a^2+b^2=c^2 $$
