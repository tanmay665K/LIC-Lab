**Current Mirror**

**Part 1: Current Mirror as an Active Load**

The current mirror circuit is one of the widely used designs in IC
design to provide a stable biasing current for multiple transistors at
once. Ideally, we would bias each transistor using a current source, to
ensure stability, but since this is not feasible, we use the current
mirror design and set the corresponding (W/L) ratio of each transistor
according to how much I<sub>D</sub> we need to flow in that transistor.

<img src="./media/image1.png"
style="width:5.66667in;height:5.03697in" />

As we can see, using a single I<sub>Ref</sub>, we can bias the
transistor M<sub>Ref</sub>, using which we can set the current flowing
through M<sub>1</sub>, making it act as an active load, and use it to as
our I<sub>D</sub> value in further transistors.

**Design Question:**

<img src="./media/image2.png"
style="width:5.49048in;height:5.70521in" />

**Design: -**

From the question, we can see I<sub>total</sub> = P/V<sub>DD</sub> = 1
mW /1.8 V = **0.555 mA**

Next, we know that Itotal = I<sub>ref</sub> + I<sub>X</sub>, where
I<sub>X</sub> = I<sub>D</sub>. Since the (W/L) ratio specified to us is
1:1, I<sub>X</sub> + I<sub>ref</sub> = (I<sub>total</sub>/2) = 0.2777
mA. In the next question, where (W/L) ratio is 1:2, the value of
I<sub>X</sub> = (I<sub>total</sub>/3).

Next, we need to calculate how much input voltage we will need to give
the N-channel MOSFET, for it to work as an amplifier (with gain ≥ 10
V/V).

We know that A<sub>V</sub> = -g<sub>m</sub>R<sub>out</sub> =
-gm(r<sub>o1</sub>\|\|r<sub>o2</sub>), where r<sub>o1</sub>,
r<sub>o2</sub> are the dynamic output resistances of the NMOS, PMOS
respectively, due to channel length modulation.

Since we know that r<sub>o1</sub> = 1/λ<sub>1</sub>I<sub>D1</sub>,
r<sub>o2</sub> = 1/λ<sub>2</sub>I<sub>D2</sub>, where I<sub>D1</sub> =
I<sub>D2</sub> = I<sub>D</sub>.

r<sub>o1</sub> \|\| r<sub>o2</sub> = 1/I<sub>D</sub> (λ<sub>1</sub> +
λ<sub>2</sub>) = 1/ (0.277 x 10<sup>-3</sup> x (1.382 + 1.329)) =
1331.65 Ω = **1.331 kΩ**

Note that values for λ<sub>1</sub>, λ<sub>2</sub> have been obtained
from the TSMC 180 nm process technology .lib file, where the parameter
for these values is **PCLM (Channel Length Modulation Parameter).**

We can also write g<sub>m</sub> as 2I<sub>D</sub>/V<sub>OV</sub>.
Finally, substituting all of this back into our original equation, we
get,

A<sub>V</sub> = (2I<sub>D</sub>/V<sub>OV</sub>). R<sub>out</sub>, from
which we can calculate **V<sub>OV</sub> as 0.0737V.**

V<sub>GS</sub> = V<sub>OV</sub> + V<sub>t</sub> = 0.0737 + 0.496 =
**0.569V**

Therefore, our input voltage for the NMOS is 0.569 V.

**Circuit Diagram: -**

<img src="./media/image3.png"
style="width:6.26806in;height:3.95208in" />

**For the P-channel MOSFETs, M1, M2: -** **W = 10 µm, L = 180 nm**

**For the N-channel MOSFETs, M3: -** **W = 31.23 µm, L = 180 nm**

**i. Using L = 180 nm**

1.  **DC Analysis**

<img src="./media/image4.png"
style="width:6.26806in;height:4.58681in" />

From here, we can see that the simulation is closely matching with our
calculated values, since the current flowing through the NMOS (M3), PMOS
(M1, M2) are nearly identical. From this, we can verify whether the
circuit is following our power requirements, which is a key part in the
design of any IC or chip.

P = I<sub>total</sub> \* V<sub>DD</sub> = 0.55401 mA \* 1.8 V = **0.9972
mW**, which is within our power budget.

Next, we move on to transient analysis, where we can verify whether our
V/V gain requirement is satisfied or not. To do this, we will configure
our input voltage, V<sub>in</sub> and convert it into a sinusoidal input
with DC offset of 0.569V.

2.  **Transient Analysis**

<img src="./media/image5.png" style="width:5.45592in;height:3.8692in" />

<img src="./media/image6.png"
style="width:6.07042in;height:4.23436in" />

<img src="./media/image7.png"
style="width:7.50278in;height:4.24167in" />From here, we can see that
the peak output voltage is 1.2381 V, for an input peak voltage of 10 mV.
Now, we can calculate our gain, and verify our whether our gain
requirement is satisfied or not.

A<sub>V</sub> = V<sub>out</sub>/V<sub>in</sub> = (0.96 – 1.2381)/(10 mV)
= **-27.81 V/V = 28.884 dB**

This definitely satisfies our gain requirement, since we needed a V/V
gain of ≥ 10 V/V.

3.  **AC Analysis**

<img src="./media/image8.png"
style="width:7.45833in;height:3.56667in" />Finally, we move on to AC
analysis, where we can calculate the 3 dB bandwidth and verify our
calculated dB gain.

> From here, we can see our 3 dB BW = 629.997 MHz – 0 = **629.997 MHz**
>
> The midband gain we are obtaining from our frequency response, i.e.,
> **29.298 dB** is also similar to the value we calculated, **28.884
> dB**.

**Circuit 2: Ratio of 1:2 using L = 180 nm**

For ratio of 1:2, then I<sub>ref</sub> = I<sub>total</sub>/3 = **0.183
mA**.

<img src="./media/image9.png"
style="width:6.26806in;height:3.88958in" />**Circuit Diagram –**

**DC Analysis –**

<img src="./media/image10.png"
style="width:5.64599in;height:4.18539in" />

**Transient Analysis –** <img src="./media/image11.png"
style="width:5.91094in;height:5.16176in" />

Gain (V/V) = (1.26006-0.96)/ (-10 mV) = **30.006 V/V = 29.544 dB** for
an input voltage of 10 mV peak voltage, frequency of 1 kHz, sine wave.
Let us perform the frequency response to verify this.

**AC Analysis –**

<img src="./media/image12.png" style="width:6.26806in;height:5.425in" />

From here, we can see that our midband gain is around **29.325 dB**,
which is a close match with our calculated value of 29.544 dB, which
gives a V/V gain of around **29.25 V/V**, not that far off from our
calculated gain of 30.006 V/V.

**ii. Analysis using L = 500 nm**

1)  **1:1 using L = 500 nm**

<img src="./media/image13.png" style="width:5.475in;height:3.48333in" />

For CMOSN (M3), **W = 65.19 µm, L = 500 nm**

For CMOSP (M1, M2), **W = 10 µm, L = 500 nm**

**DC Analysis:**

<img src="./media/image14.png"
style="width:5.16417in;height:3.77901in" />

**Transient Analysis:**

<img src="./media/image15.png"
style="width:6.26806in;height:5.40347in" />

**AC Analysis –**

<img src="./media/image16.png"
style="width:6.26806in;height:5.47569in" />

**Gain = 37.87023 dB, 3 dB BW = 122.329 MHz**

**ii. Circuit 2: Ratio of 1:2 using L = 500 nm**

For CMOSN (M3), **W = 85.243 µm, L = 500 nm**

For CMOSP (M1), **W = 10 µm, L = 500 nm**

For CMOSP (M2), **W = 20 µm, L = 500 nm**

**DC Analysis –**

<img src="./media/image17.png"
style="width:5.90643in;height:4.34442in" />

**Transient Analysis –**

<img src="./media/image18.png"
style="width:6.26806in;height:5.53125in" />

Gain (V/V) = **-62.063 V/V = 35.855 dB**

**AC Analysis –**

<img src="./media/image19.png"
style="width:6.26806in;height:5.52153in" />

**3 dB BW = 93.0732 MHz, Gain (dB) = 38.015 dB**

**ii. Analysis using L = 1 µm**

1.  **Ratio of 1:1**

For CMOSN (M3), **W = 93.35 µm, L = 1 µm**

For CMOSP (M1), **W = 10 µm, L = 1 µm**

For CMOSP (M2), **W = 10 µm, L = 1 µm**

<img src="./media/image20.png"
style="width:5.56343in;height:3.68594in" />

**DC Analysis –**

<img src="./media/image17.png"
style="width:5.05471in;height:3.71795in" />

**Transient Analysis –**

<img src="./media/image21.png"
style="width:5.86667in;height:4.94957in" />

Gain (V/V) = **-60 V/V = 35.563 dB**

**AC Analysis –**

<img src="./media/image22.png"
style="width:5.04167in;height:4.4021in" />

**3 dB BW = 98.90171 MHz, Gain (dB) = 35.481 dB**

**ii. Analysis using L = 1 µm**

1.  **Ratio of 1:1**

For CMOSN (M3), **W = 121.51 µm, L = 1 µm**

For CMOSP (M1), **W = 20 µm, L = 1 µm**

For CMOSP (M2), **W = 10 µm, L = 1 µm**

<img src="./media/image23.png"
style="width:6.26806in;height:3.61528in" />

**DC Analysis –**

<img src="./media/image24.png"
style="width:5.1285in;height:3.74268in" />

**Transient Analysis –**

<img src="./media/image25.png"
style="width:6.26806in;height:5.58056in" />

**AC Analysis –**

<img src="./media/image26.png"
style="width:6.26806in;height:5.53889in" />

**3 dB BW = 57.2524 MHz, Gain (dB) = 38.69341 dB**

**Table of Comparisons**

| **Parameter** | **L = 180 nm (1:1)** | **L = 180 nm (1:2)** | **L = 500 nm (1:1)** | **L = 500 nm (1:2)** | **L = 1 μm (1:1)** | **L = 1 μm (1:2)** |
|----|----|----|----|----|----|----|
| **NMOS Width** | 31.23 μm | Not specified | 65.19 μm | 85.243 μm | 93.35 μm | 121.51 μm |
| **PMOS Width (M1)** | 10 μm | 10 μm | 10 μm | 10 μm | 10 μm | 20 μm |
| **PMOS Width (M2)** | 10 μm | 20 μm | 10 μm | 20 μm | 10 μm | 10 μm |
| **Voltage Gain (V/V)** | 27.81 | 30.006 | Not directly specified | 62.063 | 60 | Not directly specified |
| **Gain (dB)** | 29.298 | 29.325 | 37.87 | 38.015 | 35.481 | 38.693 |
| **3dB Bandwidth (MHz)** | 629.997 | Not clearly specified | 122.329 | 93.073 | 98.902 | 57.252 |

**Part 2: Differential Amplifier**

Now that we have understood the basics of the current mirror, we will
move onto using it to design our differential amplifier, using the same
parameters that we designed for the differential amplifier simulation.
<img src="./media/image27.png"
style="width:6.21486in;height:4.09729in" />

For the N-channel MOSFETs (CMOSN), the W/L ratios are as follows: -

**M1, W = 108.5 µm, L = 180 nm**

**M2, W = 108.5 µm, L = 180 nm**

**M3, W = 22.42 µm, L = 180 nm**

**M6, W = 10 µm, L = 180 nm**

The reason for the (W/L) ratio of M3 being more than double that of M6
is because the current flowing through M3 should be double than the
current of M6, i.e., I<sub>M3</sub> = 1.222 mA, while I<sub>M6</sub> =
0.611 mA.

This is also the same reason why M4, M5 have the same (W/L) ratios, so
that equal amounts of current flows through both transistors.

For the P-channel MOSFETs (CMOSP), the W/L ratios are as follows: -

**M4, W = 52 µm, L = 180 nm**

**M5, W = 52 µm, L = 180 nm**

**M6, W = 10 µm, L = 180 nm**

**DC Analysis**

<img src="./media/image28.png"
style="width:7.0965in;height:4.74017in" />

As we can see, for our (W/L) ratios, the values we obtain from the DC
analysis closely match the ones we require.

**Transient Analysis**

<img src="./media/image29.png"
style="width:6.94756in;height:6.07777in" />

We have supplied a differential input of 10 mV peak voltage, 1 kHz
frequency, sine wave. The input is differential, i.e., only to the gate
of M1, since the output of a differential amplifier is the difference in
drain voltages of M1, M2. Since the output is a difference, if we supply
common input, the amplifier will reject the signal and provides very
little to no gain (ideally).

A<sub>v</sub> = (1.092 – 0.95)/ (-10 mV) = **-14.2 V/V = 23.045 dB**

**Results and Inferences**

The experiment demonstrates several important characteristics of current
mirror circuits with varying channel lengths and W/L ratios:

1.  **Gain-Bandwidth Trade-off**

There is a clear inverse relationship between gain and bandwidth across
the different channel lengths. The 180 nm designs show modest gain (~29
dB) but exceptional bandwidth (\>600 MHz), while the 1 μm designs
provide much higher gain (~35-39 dB) at the expense of reduced bandwidth
(\<100 MHz).

2.  **Channel Length Effects**

Increasing the channel length from 180 nm to 500 nm and then to 1 μm
results in:

1.  Increased gain: Due to reduced channel length modulation effects (λ)
    in longer channel devices, resulting in higher output resistance.

2.  Decreased bandwidth: Due to increased parasitic capacitances
    associated with larger transistor dimensions.

3.  Larger transistor widths required: NMOS widths had to be
    significantly increased (31 μm → 121 μm) to maintain the same
    current levels.

<!-- -->

3.  **W/L Ratio Impact**

The 1:2 ratio consistently outperforms the 1:1 ratio in terms of gain
across all channel lengths:

1.  For 180 nm: Modest improvement (29.298 dB → 29.325 dB)

2.  For 500 nm: Slight improvement (37.87 dB → 38.015 dB)

3.  For 1 μm: More significant improvement (35.481 dB → 38.693 dB)

The current mirror circuit's performance can thus be tailored to
specific application needs by selecting appropriate channel lengths and
W/L ratios, with clear trade-offs between gain, bandwidth, and silicon
area (as evidenced by the increasing transistor widths required for
longer channel designs).
