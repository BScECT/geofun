# Airborne Laser Scanning

## Introduction

In Chapter 3, we examined how the positions of points on the Earth can be determined within a geographic coordinate reference system (CRS). We focused primarily on the capabilities of Global Navigation Satellite Systems (GNSS) and saw that these technologies can provide positions with (sub-)centimetre-level precision. Such accuracy allows us to measure topography and detect surface changes over time with great confidence.

However, despite its precision, GNSS is not a particularly efficient technology for collecting terrain elevations over large areas. Acquiring dense elevation data point by point quickly becomes time-consuming, labour-intensive, and costly. This naturally raises the question: can terrain elevations be measured more efficiently?

The answer will not come as a surprise: yes, they can. A range of remote sensing techniques exists that are capable of collecting terrain elevation data at sub-metre spatial resolution and with centimetre-level vertical accuracy, often over very large areas and in a relatively short amount of time. Some of these techniques can even be used to measure seafloor topography, known as bathymetry.

In this lecture, we will focus on one such technique: laser scanning, also referred to as lidar (Light Detection and Ranging). Because our primary interest lies in the efficient acquisition of terrain elevations over large areas, the emphasis of this lecture will be on airborne laser scanning, that is, lidar systems mounted on aircraft. This is a highly versatile technology that is widely used for mapping land topography and, under suitable conditions, for measuring bathymetry in shallow and clear waters.

The principles and techniques discussed in this lecture are not limited to airborne platforms. They also apply to laser scanning systems deployed from a wide range of other platforms, including tripods, backpacks, vehicles, trains, drones, helicopters, and satellites.


The main objective of this chapter is: to develop a
physical and technical understanding of airborne laser scanning that
enables you to reason about system design choices, data quality, and
application suitability, rather than treating LiDAR data as a black
box.

The chapter is structured as follows. We begin with an explanation of
the two main principles of laser ranging. The first is based on
measuring travel time, so-called time-of-flight (ToF) systems;
the second is based on measuring phase differences, referred to as
phase-based systems. For the application we are concerned with,
time-of-flight systems are the most relevant and will therefore receive
most attention.

Next, we follow a single laser pulse along its entire journey: from the
moment it is generated, through its emission from the instrument,
propagation through the atmosphere or water, interaction with the target
surface, its return to the detector, and finally the signal processing
steps that determine the range to the target. Along the way, we
introduce the key system-related, propagation-related, and
target-related parameters that govern system performance.

This naturally leads to the derivation of a central analytical tool in
LiDAR remote sensing: the laser range equation, which relates
the transmitted laser power to the power received by the sensor while
explicitly accounting for system characteristics, propagation losses,
and target properties.

Finally, we address how the resulting measurements are georeferenced
within a geographic CRS when acquired from an aircraft and
conclude with an overview of the processing steps required to obtain
what we ultimately aim for in many applications: a digital surface
model (DSM) and a digital terrain model (DTM).

## Principles of Lidar

Lidar (Light Detection and Ranging) is an active remote sensing
technology that uses laser radiation to measure ranges.

```{admonition} Active vs Passive remote Sensing
Active remote sensing instruments measure reflected or backscattered energy that is emitted by the instrument itself. Passive remote sensing instruments measure naturally occurring radiation, either reflected solar radiation or thermally emitted radiation from the Earth–atmosphere system.
```

The range can be measured in different ways. Time-of-Flight
(ToF), also known as pulse-based, systems emit short laser
pulses and measure the time it takes for the pulse to travel to a
target, be reflected, and return to the sensor. Because electromagnetic
radiation propagates at the speed of light c, the distance $l$ to the
target is obtained from 

$l = \frac{1}{2}c\tau$

where 𝜏 is the measured
round-trip travel time (i.e., the time-of-flight) of the pulse. The
factor $\frac{1}{2}$ accounts for the outgoing and returning path (see
Tiberius et al., 2022, Section 20.1.1). 

Phase-based lidar systems determine distance by interferometry, that
is, by measuring the phase difference $\Phi$ in radians with 

$\Phi \in [0,2\pi)$


between the transmitted laser signal, whose intensity is modulated, and
the received signal. Phase-based systems can achieve very high
precision, on the order of a few millimetres. However, because they
require comparatively more signal power than ToF systems, they are
typically used for short-range applications such as indoor scanning.
Their operational range is usually up to 80–120 m, with optimal
performance below approximately 50 m (see Tiberius et al., 2022,
Section 20.1.2 for further explanation).

There are additional ranging principles (i.e., triangulation
lidar), but these will not be discussed here. For the acquisition of
terrain elevations, ToF systems are by far the most commonly used.

## The Journey of a Laser Pulse

To understand how the technology works and which factors influence its
performance, let us follow a laser pulse in a time-of-flight (ToF)
lidar system along its entire journey: from the moment it is
generated, through its emission from the instrument, propagation through
the atmosphere or water, interaction with the target surface, return to
the detector, and finally the signal processing steps that determine the
range to the target.

### Laser Transmitter

#### The Laser

A laser is a device that generates a highly coherent, monochromatic,
and directional beam of electromagnetic radiation through the process of
stimulated emission. The term laser is an acronym for Light
Amplification by Stimulated Emission of Radiation.

At the core of a laser is a gain medium (such as a crystal, gas,
or semiconductor) whose atoms or ions can be excited to higher energy
states by an external energy source, known as the pump. When an
excited particle is stimulated by an incoming photon with the
appropriate energy, it emits a second photon that is identical in
wavelength, phase, and direction to the first. This process leads to
optical amplification.

The gain medium is placed inside an optical resonator, typically
formed by two mirrors facing each other. One mirror is highly
reflective, while the other is partially transmissive. Photons bounce
back and forth between the mirrors, stimulating further emissions and
building up a coherent light field. A fraction of this amplified light
escapes through the partially transmissive mirror as the laser beam.

#### Laser Wavelength

For the mapping of terrain elevations, typically diode-pumped
Nd:YAG lasers are used operating at a wavelength of 1,064 nm
(near-infrared). Other wavelength options are available, however.

To illustrate why the choice of the wavelength matters, consider the
absorption spectrum of electromagnetic radiation in water. As shown in
the Fig. 1, absorption is strongly wavelength dependent: absorption
is relatively low in the blue–green part of the visible electromagnetic
spectrum and much higher at longer wavelengths. As a consequence, blue
and green light can penetrate further into the water column—potentially
reaching the bottom—whereas radiation at near-infrared wavelengths is
absorbed rapidly. So, the 1,064 nm laser cannot be used to measure
bathymetry, a green laser does!

```{figure} figures/absorption_water.png
Absorption spectrum of liquid water across a wide wavelength range. Taken from [https://commons.wikimedia.org/wiki/File:Absorption_spectrum_of_liquid_water.png](https://commons.wikimedia.org/wiki/File:Absorption_spectrum_of_liquid_water.png)
```

```{admonition} Laser wavelength
<table>
<tbody>
<tr>
<td><p>The choice of wavelength
depends on application-specific requirements such as range, accuracy,
surface type, and atmospheric conditions. The options include
(PhoenixLiDAR.com, 2024):</p>
<ul>
<li>532 nm (green): Primarily used for bathymetric lidar applications,
where water depth is measured. These systems typically have a relatively
short range but can penetrate the water surface and provide accurate
depth measurements. Green light is more strongly absorbed by atmospheric
particles, which limits its performance under certain atmospheric
conditions.</li>
<li>905 nm (near-infrared): Commonly used in drone-based lidar systems.
Lidar systems operating at 905 nm tend to perform better in humid or
foggy conditions and are therefore suitable for mapping low vegetation
and relatively flat terrain.</li>
<li>1,064 nm (near-infrared): This longer near-infrared wavelength is
less affected by atmospheric scattering, making it well suited for
long-range applications such as high-altitude airborne mapping and
surveying.</li>
<li>1,550 nm (near-infrared): Typically used in high-power lidar systems
that can operate from both drones and crewed aircraft. These systems
often exhibit lower data noise and are widely used for high-resolution
and high-accuracy mapping, albeit with ranges generally shorter than
those achieved at 1,064 nm.</li>
</ul></td>
</tr>
</tbody>
</table>
```

#### Other Important Laser Parameters

In a ToF laser scanner, the laser does not emit its energy continuously
but in very short bursts—laser pulses—with durations ranging from
approximately one to several nanoseconds. Each pulse must contain
sufficient energy for its backscattered signal to be detected by the
receiver. Several laser parameters
(<https://www.laserax.com/blog/laser-powers#peak-power>) control this:

- (Average) Laser power: Power is defined as the rate at which energy
  is emitted and is expressed in watts (W), where 1 W corresponds to 1
  joule per second.
- Pulse repetition frequency (PRF): Because the energy is emitted in
  discrete pulses, the energy per pulse is given by the average laser
  power divided by the number of pulses emitted per second, i.e. the
  PRF.
- Pulse duration and peak power: The pulse energy is distributed over
  the pulse duration. For a given pulse energy, a shorter pulse duration
  results in a higher peak power, defined as the maximum instantaneous
  power during the pulse. Peak power is the quantity that appears in
  the laser range equation and directly influences the strength of the
  received signal.
- Laser beam divergence: Laser beam divergence describes
  the angular spread of the laser beam as it propagates through space.
  It is usually expressed in milliradians (mrad) and is determined by
  both the properties of the laser and the optical design of the
  lidar sensor. Typical values range from about 0.1 to 1.0 mrad. A
  larger divergence leads to a larger footprint on the ground; we will
  return to this point later.

These design requirements are mutually conflicting: no lidar
system can optimise pulse energy, PRF, pulse duration, divergence, eye
safety, and ranging performance simultaneously. Practical systems
therefore represent carefully engineered trade-offs. We will analyse
some of these trade-offs in more detail later. For now, let us
complete the journey of the laser pulse.

### Start Signal Generation and Beam Steering

When the laser fires, a beam splitter directs a small fraction of the
outgoing pulse to an internal start detector. This signal triggers the
Time-to-Digital Converter (TDC) to start counting the time. You can
think of this as pressing the start button on an extremely precise
stopwatch.

A beam deflection unit then steers the laser pulse in a certain
direction. Common implementations (see Fig. 2) include rotating and
oscillating mirrors, which produce different point distributions on the
ground.

```{figure} figures/laser_beam.png
Laser beam deflection with rotating and oscillating mirrors. Reproduced with permission from  Mandlburger (2024)
```

The most important specifications that describe the performance of a
scanner are:

- Horizontal Field of View (HFOV): The angular range,
  typically expressed in degrees, covered by the sensor in the
  horizontal plane. A larger HFOV results in a wider ground swath,
  allowing the sensor to cover a larger area per flight line.
- Vertical Field of View (VFOV): The angular range,
  typically expressed in degrees, covered by the sensor in the vertical
  plane. A larger VFOV enables the detection of objects over a wider
  range of vertical angles, which is particularly beneficial for mapping
  complex vertical structures such as buildings, cliffs, or vegetation.
- Scan rate: The speed at which the scanning mirror moves,
  often expressed as the number of scan lines per second. A higher scan
  rate increases the point density in the flight direction
  (along-track), assuming other parameters remain constant.
- Angular step width: The angular increment between successive
  laser pulses in the across-track direction, typically
  expressed in degrees. The minimum achievable angular step width is
  constrained by the selected laser pulse repetition frequency (PRF),
  while the maximum step width is limited by the maximum scan rate of
  the scanner. Smaller angular step widths result in higher point
  densities in the across-track direction.

### Propagation and Backscattering

After emission, the laser pulse propagates through the
atmosphere toward the ground, where it interacts with objects such
as vegetation, buildings, or the soil surface.

#### Atmospheric Propagation

The Earth’s atmosphere consists of various gases and suspended aerosol
particles. As the laser pulse travels through the atmosphere, it
interacts with these components through scattering, absorption,
refraction, and reflection. These processes (mainly scattering @
1,064nm) reduce the amount of laser energy that reaches the target and,
consequently, the strength of the returned signal.

Aerosols and water vapour selectively absorb electromagnetic radiation
at different wavelengths. The combined effect of these processes is
described by the atmospheric transmittance T, which ranges from 0 to
1, where T=1 represents a perfectly transparent atmosphere. The value
of T depends on meteorological conditions such as visibility, air
temperature, humidity, and aerosol concentration, as well as on the
flight altitude.

Atmospheric transmittance typically increases with altitude,
resulting in lower average attenuation coefficients for vertical paths
compared to horizontal paths (see Fig. 3). For flying heights of
1,000 m, 2,000 m, and 3,000 m above ground (and above sea level),
average vertical attenuations are approximately 0.22, 0.17, and 0.14
dB/km, respectively.

```{figure} figures/atmospheric_transmission.png
Atmospheric transmission at different altitudes. Taken from Zhang et al. (2024)
```

#### Interaction with the Surface

At the ground, incident laser energy can be absorbed or reflected. The
reflected portion is redistributed in different directions through
scattering, which can occur in several different ways, as illustrated in
Fig. 4.

Specular scattering occurs when the incident energy is reflected
predominantly in a single direction, such that the angle of reflection
equals the angle of incidence. This situation is rare for natural
surfaces but may occur approximately (quasi-specular reflection) on
relatively smooth surfaces such as calm water, wet soil, or smooth
roofs. In contrast, Lambertian scattering describes a situation in
which the incident energy is redistributed uniformly in all directions,
including back toward the sensor. Most natural surfaces exhibit
scattering behaviour that lies somewhere between these two idealised
cases.

```{figure} figures/scattering.png
Various forms of scattering at the surface. Taken from: Philpot & Philipson: Remote Sensing Fundamentals.
```

The scattering behaviour depends on several factors, most
importantly the type of material, the surface roughness at the scale of
the wavelength, and the wavelength of the incident laser radiation.

#### Target Cross Section

The quantity describing how effectively a target intercepts and
redirects the incoming laser energy back toward the sensor is the
target cross section (σ). It can be interpreted as the
effective area (units is $m^2$) of a target “as seen”
by a lidar sensor. It is defined as:
                                              
 ${\sigma = \frac{4\pi}{\Omega}}\rho A_{t}$

where ρ is the reflectance (or reflectivity), defined as the
fraction of incident laser energy reflected by the surface (averaged
over the illuminated target area); A<sub>t</sub> is the effective
area illuminated by the laser beam, i.e. the area of the target
projected orthogonally to the laser beam; Ω is the scattering
solid angle into which the target reflects energy toward the
receiver. A smaller Ω indicates that the reflected energy is more
concentrated (as for a specular reflector), making the target appear
“brighter” to the sensor.

```{note}

A solid angle $\Omega$ is the
three-dimensional analogue of a planar angle. It quantifies how much of
the sphere surrounding a point is subtended by an object
and is measured in steradians (sr):

1. A full sphere subtends 4$\pi$ sr.
2. Half a sphere (e.g. all directions above a flat surface) subtends 2$\pi$ sr.
```

Reflectance is a material property that is
wavelength-dependent. The curve describing reflectance as a
function of wavelength is called a reflectance spectrum. Fig. 5
shows reflectance spectra for various surface materials.

```{figure} figures/reflectance_spectra.png
Reflectance spectra for various surface materials. Taken from Rieger et al. (2025)
```

Regarding the effective illuminated target area, three cases can
be distinguished:

- Extended targets (target area \> than the laser footprint):
  In this case, $A_t$ (for a nadir footprint)
  equals:

  ${A_{t} = \pi}{{({\frac{1}{2}R\beta})}^{2} = \frac{\pi R^{2}\beta^{2}}{4}}.$

- Linear targets (e.g. power lines or wires): The target cross section
  depends linearly on range.
- Point targets (e.g. individual leaves) with an area smaller than the
  footprint: In this case, the target cross section is independent of
  range.

At first glance, the definition of σ shows no explicit
dependence on the incidence angle. However, the incidence
angle is implicitly accounted for:

- through $A_t$, since the projected area depends on
  surface orientation;
- through Ω, because changes in illumination geometry can alter the
  angular distribution of the reflected energy and thus the apparent
  scattering behaviour of the target.

For an extended target with Lambertian scattering characteristics, i.e.
a surface that reflects light in all directions according to Lambert’s
Cosine Law, the general expression for σ can be simplified to:

$\sigma = \pi\rho R^2\beta^2cos(a)$                                              

In this case, the effective scattering solid angle is $\Omega = \pi$ sr.
(Note, while a hemisphere subtends $2\pi$ sr, the
cosine-weighted angular distribution of Lambertian reflection
concentrates the effective reflected energy into $\pi
$ sr). Besides,
${A_{t} = \frac{\pi R^{2}\beta^{2}}{4}}\cos\alpha.$

### Optical-to-Electrical Conversion

The backscattered laser energy is collected by the receiver aperture and
detected by a photodiode—typically an avalanche photodiode (APD)
in traditional linear-mode lidar systems, which usually employ a single
detector. The APD converts the incoming optical signal into an
electrical current and amplifies it. The output is an analogue voltage
signal that represents an electrical “echo” of the returned laser pulse.

Three parameters are particularly important at this stage: the area
of the receiver aperture, the throughput efficiency of the
receiver, and the sensitivity of the detector. The detector
sensitivity is largely governed by the noise generated by the detector
and its associated electronics.

```{admonition} The maximum unambiguous range
Modern lidars
may operate at PRFs larger than 2,000 kHz. This raises an important
question: what is the maximum distance to a target if we
require that a laser pulse must return to the sensor before the next
pulse is emitted?

This distance is known as the maximum unambiguous
range, denoted $l_{max}$. It is given
by $l_{max} = \frac{1}{2}c(1/PRF)$

For a PRF of 2,000 kHz, this results in a
maximum unambiguous range of 75 m. In other words, if a laser scanner were
required to wait for the return of each pulse before emitting the next
one, the PRF would have to be drastically reduced to allow for larger
flying heights.

To overcome this limitation, modern lidar systems use solutions
collectively referred to as multiple-time-around
(MTA) techniques. These approaches allow multiple
pulses to be in the atmosphere simultaneously and resolve range
ambiguities using, for example, a preliminary digital terrain model or
by varying the PRF.

With the extremely high PRFs achieved by today’s lidar systems, even
these strategies are sometimes insufficient. This has motivated the
development of systems employing large numbers of parallel detectors,
such as single-photon and
Geiger-mode lidar, which can handle
very high pulse rates and return densities. For further discussion, see
Mandlburger (2019).
```

### Detection of Pulse Arrival

The system must now determine when the pulse arrived. Two main system
concepts exist.

a) Discrete-return systems - In discrete-return systems, the
analog voltage signal is fed to a discriminator that compares the signal
against a predefined threshold. When the signal exceeds this threshold,
a stop signal is sent to the TDC. The TDC then converts the measured
time interval into a digital value, which is finally converted into a
range. Again, multiple reflections may be detected per pulse (see figure
below).

b) Full-waveform systems - Full-waveform systems record
the complete backscattered signal as a function of time (see figure
below). In doing so, an Analog-to-Digital Converter (ADC) samples
the analog voltage signal at a high rate, producing a waveform.
Various algorithms can be applied (both online and in post-processing
mode) to this waveform to estimate the travel time and thus the range.
Conceptually, this often corresponds to locating one or more peaks in
the recorded waveform.

```{figure} figures/lidar_return.png
Example of a real-world incoming lidar return. Potential discrete-return peaks are marked in red. Image taken from [https://pdal.io/en/2.8.4/workshop/lidar-introduction.html#id3](https://pdal.io/en/2.8.4/workshop/lidar-introduction.html#id3)
```

```{admonition} Lidar Systems

<table>
<tbody>
<tr>
<td><p><strong>Photon-counting lidars</strong> (<em>taken and summarized
from Mandlburger (2024)</em>) – Traditional ToF lidar systems typically
require several hundred detected photons to reliably register a single
target. A Geiger-mode lidar (GmLiDAR), however, emits a divergent laser
pulse that produces a relatively large footprint on the ground. The
return signal is detected by an array of Geiger-mode avalanche
photodiodes containing thousands of single-photon-sensitive detector
elements. These detectors are biased above their breakdown voltage, so
that the arrival of a single photon triggers an avalanche, resulting in
a sharp voltage rise that stops the TDC. As a consequence, only one echo
can be detected per laser pulse and per detector cell.</p>
<p>Single-photon lidar (SPL) systems follow a different strategy. A
short laser pulse is split into a grid of beamlets (e.g. 10 × 10) using
a diffractive optical element. These beamlets are highly collimated,
producing non-overlapping footprints on the ground. Each beamlet is
received by a dedicated detector, typically composed of many
single-photon-sensitive cells operating in Geiger mode. Within a limited
dynamic range, this configuration allows the detection of multiple
targets per beamlet.</p>
<p>For both GmLiDAR and SPL, single-photon sensitivity enables operation
from higher flying altitudes and thus much higher area coverage rates.
As a result, these technologies are particularly well suited for
large-scale and nationwide topographic mapping. A schematic comparison
of linear-mode lidar, Geiger-mode lidar, and single-photon lidar is
shown in the following figure.</p>


</p></td>
</tr>
</tbody>
</table>

```{figure} figures/lidar_comparison.png
A schematic comparison of linear-mode lidar, Geiger-mode lidar, and single-photon lidar. Reproduced with permission from  Mandlburger (2024)
```

## The Laser Range Equation

After introducing the fundamental principles of lidar, we have followed
a laser pulse along its complete signal path: from emission at the
transmitter, through propagation and interaction with the target, to
detection at the receiver.

Along this path, we identified a range of system-related,
propagation-related, and target-related parameters that determine how
much of the transmitted energy is ultimately recorded by the sensor and,
consequently, the quality and reliability of the measured data.

These considerations naturally lead to one of the most important
analytical tools in lidar system design and performance analysis: the
laser range equation. This equation quantitatively relates the
transmitted laser power to the power received by the sensor, while
explicitly accounting for system characteristics, propagation losses,
and target properties.

Because of its central role in instrument selection and performance
assessment, we now derive the laser range equation step by step.

Consider a laser that transmits a pulse with power P<sub>t</sub> and
beam divergence β. The distance from the sensor to the target is R.
The target is characterised by a target cross section σ. The
receiver has a circular aperture with diameter D<sub>r\ </sub>and
collects a power P<sub>r</sub>. Let’s assume, our target is at
nadir.

At range R, the laser beam illuminates a circular footprint with
diameter Rβ and area

${A_{f} = \pi}{{({\frac{1}{2}R\beta})}^{2} = \frac{\pi R^{2}\beta^{2}}{4}}$

The irradiance at the target (power per unit area) is therefore

${E_{t} = \frac{P_{t}}{A_{f}} = P_{t}}\frac{4}{\pi R^{2}\beta^{2}}$

The target cross section σ represents the effective area that
intercepts the incident irradiance and redirects energy back toward the
sensor. Assuming Lambertian scattering and using the standard lidar
definition of σ, which accounts for isotropic re-radiation into 4π
steradians, the irradiance incident to the receiver is

${E_{r} = E_{t}}{\sigma = \frac{4P_{t}}{\pi R^{2}\beta^{2}}}\frac{\sigma}{4\pi R^{2}}$

The receiver aperture has an area

${A_{r} = \pi(\frac{1}{2}D_{r}}^{2}) = \frac{\pi D_{r}^{2}}{4}$

The power collected by the receiver is obtained by multiplying the
irradiance incident to the receiver by the receiver aperture area,
yielding

${P_{r} = \frac{4P_{t}}{\pi R^{2}\beta^{2}}}\frac{\sigma}{4\pi R^{2}}{\frac{\pi D_{r}^{2}}{4} = \frac{P_{t}\sigma D_{r}^{2}}{4\pi R^{4}\beta^{2}}}$

In practice, not all transmitted power reaches the target or the
receiver. Signal losses occur within the instrument and during
propagation through the atmosphere. These effects are accounted for by
introducing two transmission factors:

- η<sub>sys</sub>: the system transmission factor, representing the
  combined optical transmission of all components within the lidar
  system. This factor is assumed to be constant for a certain scanner
  but may vary with different systems (and over time);
- η<sub>atm</sub>: the atmospheric transmission factor, which accounts
  for attenuation due to scattering and absorption along the propagation
  path. Following Höfle and Pfeifer (2007), it is expressed as
  η<sub>atm</sub> = 10<sup>−2Ra/10000</sup>,
  where a is the atmospheric attenuation coefficient in dB/km (see
  values provided earlier) and R is the range in meters. The factor
  10,000 originates from a given in dB/km, whereas R is in meters as
  before.

Finally, the receiver also collects background power P<sub>b</sub>,
for example due to solar radiation reflected from the surface and
scattered by the atmosphere. The magnitude of this contribution depends
strongly on wavelength and can be estimated from the solar irradiance
spectrum (see Fig. 8).

```{figure} figures/solar_radiance.png
The solar irradiance spectrum. Taken from Rieger et al. (2025)
```

Including these terms, the laser range equation becomes

${P_{r} = \frac{P_{t}\sigma D_{r}^{2}}{4\pi R^{4}\beta^{2}}}\eta_{\mathit{sys}}{\eta_{\mathit{atm}} + P_{b}}$

This is the laser range equation in its most generic form. For an
extended surface,

$\sigma = \pi\rho R^2\beta^2cos(a)$

Hence,

${P\_{r} = \frac{P_{t}{({\pi\rho R^{2}\beta^{2}\cos\alpha})}D_{r}^{2}}{4\pi R^{4}\beta^{2}}}\eta_{\mathit{sys}}{{\eta_{\mathit{atm}} + P_{b}} = \frac{P_{t}{({\rho\cos\alpha})}D_{r}^{2}}{4R^{2}}}\eta_{\mathit{sys}}{\eta_{\mathit{atm}} + P_{b}}$

## Georeferencing

The material in this chapter draws extensively on Mandlburger (2024),
while being reorganized and rephrased for the purposes of this lecture.

### Remaining Components of an Airborne Laser Scanner

So far, we have focused primarily on the laser scanner itself.
To efficiently collect topographic data—or bathymetric data, the latter
only in shallow and clear waters—the laser scanner must be mounted on an
aircraft (see Fig. 9).

This immediately raises an important question: What else do we need
on board to ultimately obtain a point cloud in a geographic coordinate
reference system (CRS)?

In addition to the laser scanner, two other sensor systems are
essential: i) A GNSS, which measures the position of the
aircraft in a geocentric coordinate reference system; and ii) an
Inertial Navigation System (INS), which continuously measures
the orientation, or attitude, of the aircraft. These components must
be tightly synchronized in time, because each laser pulse must
be linked to the exact position and orientation of the platform at the
moment the pulse is emitted and received. The process of computing
georeferenced 3D points directly from the laser, GNSS, and INS
measurements is known as direct georeferencing. 

```{figure} figures/airborne_lidar.png
Schematic diagram of airborne laser scanning. Reproduced with permission from  Mandlburger (2024)
```

### The Workflow

The standard airborne lidar processing workflow begins with the
estimation of the aircraft’s trajectory. This is done by combining GNSS
and INS observations using Kalman filtering, resulting in a
so-called smoothed best estimate of the trajectory.

This trajectory provides:

- the 3D position of the platform (X, Y, Z) in a geocentric,
  Earth-centered Earth-fixed (ECEF) CRS, and
- the attitude of the platform with respect to the local
  horizon, expressed by the navigation angles roll, pitch, and
  yaw.

In the next step, the trajectory information is combined with the
time-stamped laser scanner measurements. Here, manufacturers
typically apply corrections for small systematic instrument effects of
the ranging and scanning unit (obtained based on laboratory
calibration). The step provides the corrected 3D coordinates of the
detected objects (i.e. laser echoes) in the scanner CRS. These points
form the basis for computing fully georeferenced 3D object coordinates
in a geocentric CRS, as illustrated in Fig. 10.

```{figure} figures/lidar_sensor.png
Schematic diagram of the geometric airborne lidar sensor model. Reproduced with permission from  Mandlburger (2024)
```

The transformation from scanner coordinates to geocentric coordinates
involves a chain of CRSs, each indicated by a specific index and colour
in the figure:

- s/blue: scanner CRS
- i/red: INS CRS
- n/no color: platform (or navigation) CRS (i.e. local horizon CRS:
  north/east/down)
- e/magenta: geocentric CRS

The transformation is given by Eq. 1.10.

$X^e(t) = X^{GNSS}(t) + R_n^e(t)R_i^p(t)(a^i+R_s^i(t)X^s(t))$

Reading the transformation equation from right to left, the process is
as follows:

The 3D point $X_s = (X^s, Y^s, Z^s)$ defined in the local scanner CRS, is first rotated into the INS CRS
using the boresight angles. These angles represent small
rotational offsets $(\Delta_{roll}, \Delta_{pitch}, \Delta_{yaw})$ between the scanner and the INS
reference planes (cf. green elements in the Figure). The point is then
translated using the lever arm $(a^i)$, which is the offset vector between the GNSS antenna phase
centre and the origin of the scanner CRS.

Next, the point is rotated from the INS CRS into the platform CRS using
the roll, pitch, and yaw angles measured by the INS ($R_i^n(t)$). A further rotation 
$(R_p^e(t))$ transforms the point from the platform CRS into the geocentric CRS.
This final rotation depends on the geographic position (latitude and
longitude) of the INS origin.

Finally, the geocentric coordinates of the GNSS antenna are added
(
$X^{GNSS}(t)$
), yielding the fully georeferenced 3D coordinates of the laser
point
$X^e(t)$.

## Accuracy Considerations

The overall horizontal and vertical uncertainty of the resulting 3D
laser points is determined by the accuracy of the laser scanner and the
platform trajectory, as well as by the quality of synchronization among
all sensor components (GNSS, INS, and scanner). Modern laser scanners
typically achieve ranging accuracies of 1–3 cm. Post-processed
integration of GNSS observations from both the base station and the
lidar sensor system yields positional accuracies of approximately
3–5 cm. Inertial navigation systems used in airborne lidar commonly
provide angular accuracies of about 0.0025° for roll and pitch and
0.005° for heading (yaw). Taken together, state-of-the-art airborne
lidar systems achieve sub-decimetre 3D coordinate accuracy.

# From Point Cloud to DSM / DTM

Once we have a georeferenced LiDAR point cloud—that is, a set of 3D
points expressed in a geographic CRS—the next step is to derive surface
models such as a Digital Surface Model (DSM) and/or a Digital Terrain
Model (DTM).

- Digital Surface Model (DSM) – A DSM represents the elevation
  of the highest surface within each unit of area. In practice,
  this means it includes both natural and artificial features such as
  building roofs, trees, bridges, and other objects above the ground.
  The DSM can be interpreted as a representation of what the laser sees
  first.
- Digital Terrain Model (DTM) – A DTM, by contrast, represents
  the bare-earth surface, that is, the elevation of the ground
  itself without vegetation, buildings, or other above-ground
  structures. A DTM therefore describes the shape of the terrain in the
  absence of these overlying features.

Strictly speaking, a Digital Elevation Model (DEM) is a more
generic term that refers to a raster or grid of elevation values.
Depending on how it is derived, a DEM may represent either a DSM or a
DTM.

The generation of DSMs and DTMs from LiDAR data typically involves three
main steps (Mandly, 2025):

1.  Point cloud cleaning – Raw LiDAR point clouds inevitably
    contain anomalies and inconsistencies due to sensor limitations,
    atmospheric effects, or interactions with transient objects. Point
    cloud cleaning is therefore an essential first step. This process
    may include:

    - removal of outliers, that is, points with implausible elevation
      values (for example caused by reflections from birds);
    - elimination of isolated points that have no neighbouring points
      within a specified distance;
    - filtering by return type: for DTM generation, last returns are
      often preferred, whereas for DSM generation first returns or
      highest returns are typically used.

2.  Point cloud classification – In the second step, the LiDAR
    points are classified into categories such as ground, vegetation,
    buildings, and other objects. This is usually achieved using
    filtering and classification algorithms that exploit differences in
    elevation, local surface roughness, and spatial relationships
    between neighbouring points.

3.  Interpolation to a regular grid – After classification, the
    elevation values of the selected points are used to create a
    continuous surface. For a DSM, all points (or the highest points per
    cell) are considered; for a DTM, only points classified as ground
    are used. The selected points are interpolated onto a regular grid
    (for example, 0.5 m × 0.5 m cells), with each grid cell representing
    a single elevation value.

## References

PhoenixLiDAR.com (2024), LIDAR Selection Guide - Considerations,
Comparisons, Current Scanners.
[https://phoenixlidar.com/wp-content/uploads/2023/06/2023-03-15_lidar_selection_guide.pdf](https://phoenixlidar.com/wp-content/uploads/2023/06/2023-03-15_lidar_selection_guide.pdf)

Rieger, P., Pfennigbauer, M., & Ullric, A.
(2025). Multispectral airborne laserscanning: Three wavelengths in
theory and practice. EuroSDR – Workshop on Multispectral LiDAR, June
23.
[https://www.eurosdr.net/sites/default/files/images/inline/04_riegl_eurosdr_multispectral_laserscanning_workshop2025.pdf](https://www.eurosdr.net/sites/default/files/images/inline/04_riegl_eurosdr_multispectral_laserscanning_workshop2025.pdf)


Höfle, B., & Pfeifer, N. (2007). Correction of laser scanning
intensity data: Data and model-driven approaches. ISPRS journal of
photogrammetry and remote sensing, 62(6), 415-433.

Mandlburger, G. (2019). Recent Developments in Airborne Lidar. GIM
International Magazine.
<https://www.gim-international.com/content/article/recent-developments-in-airborne-lidar-2>

Mandlburger, G. (2024). Airborne Lidar: A Tutorial for 2025 – Part I:
Lidar basics. Lidar Magazine. Volume 14, Issue 4. Nov/Dec 2024.
<https://lidarmag.com/2024/12/30/airborne-lidar-a-tutorial-for-2025/>

Mandly, F. N. (2025). How to Generate a Digital Terrain Model from a
LiDAR Point Cloud: Complete Workflow. lidarnews.com.
<https://lidarnews.com/articles/how-to-generate-a-digital-terrain-model-from-a-lidar-point-cloud-complete-workflow/>

Zhang, M., Wen, G., Fan, C., Guan, B., Song, Q., Liu, C., & Wang, S.
(2024). Analysis of the Ranging Capability of a Space Debris Laser
Ranging System Based on the Maximum Detection Distance Model. Remote
Sensing, 16(4), 727.
[https://doi.org/10.3390/rs16040727](https://doi.org/10.3390/rs16040727)

