**Except for the Introduction, this chapter is reproduced in its
entirety from (this book is published under a CC BY-NC-SA license).
Explicit references to other chapters and sections of this book have
been added. The Introduction is adapted from Chapter 12 of , with minor
reorganization of the material and the omission of one subsection.**

# Introduction

The Global Positioning System (GPS), also known as the NAVigation
Satellite Time And Ranging (NAVSTAR) system, is one the most successful
satellite systems to date. Its success is strongly linked to the
ever-decreasing costs of GPS receivers, which primarily consist of
electronic hardware. While high-end receivers still cost in the order of
$ 1-10k, mass-market receivers, such as those used in smartphones, cost
no more than a few dollars each. Currently there are about as many GPS
devices on Earth as people, nearly 7 billion, the vast majority of which
are in smartphones. The global Global Navigation Satellite System (GNSS)
downstream market revenues, from both devices and services, were in 2020
around 150 billion Euro, according to the market report by the European
GNSS Agency (GSA), now the European Union Agency for the Space Programme
(EUSPA) .

The first GPS satellite was launched back in February 1978. GPS is a
*one-way* radio ranging system which provides real-time knowledge of
one’s Position and Velocity, and a very accurate Time reference as well
(all together referred to as PVT).

GPS provides Positioning, Navigation and Timing (PNT) functionality,
which is very valuable not only for the US military, for which it was
first developed, but also to a myriad of commercial activities, as well
as the general public at large.

The GPS system consists of three segments.

1.  The space segment, consisting of 24 or more satellites, with
    accurate atomic clocks on board, continuously transmitting ranging
    signals to Earth.

2.  The control segment, consisting of a number of ground stations,
    which monitors the satellites, computes their orbits and clock
    offsets, and uploads this information to the satellites, which in
    turn encode this information on the ranging signal (the so-called
    navigation data).

3.  The user segment, simply consisting of many GPS receivers, which
    each track four or more GPS satellites, and compute their own
    position.

This chapter provides an introduction to GPS positioning.
Section <a href="#chap:ranging" data-reference-type="ref"
data-reference="chap:ranging">2</a> presents the basic concepts of the
measurement of travel-time of a radio signal from a GPS satellite to a
receiver. With these measurements of range as input,
Section <a href="#chap:GPSpositioning" data-reference-type="ref"
data-reference="chap:GPSpositioning">3</a> describes the default mode of
GPS positioning, referred to as stand-alone or single-point positioning.
The next section introduces the concept of relative positioning, by
means of which high-accuracy, centimeter-level positioning is made
possible.
Section <a href="#chap:GNSSapplications" data-reference-type="ref"
data-reference="chap:GNSSapplications">5</a> presents, after a brief
overview of the four major Global Navigation Satellite Systems (GNSS),
an overview of the wide range of applications of GPS/GNSS in today’s
society. There is much more more of information available on this
subject, and the reader is therefore referred to, for instance, the
textbooks and .

<figure id="fig:GPSblockIIF" data-latex-placement="bht">
<div class="center">

</div>
<figcaption>GPS block IIF satellite, built by Boeing. These GPS
satellites, 12 in total, have been launched between 2010 and 2016. They
have a design lifetime of 12 years. The full GPS constellation nominally
consists of 24 satellites. Image courtesy of Boeing <span
class="citation" data-cites="boeing"></span>.</figcaption>
</figure>

# Ranging

## Radio signal

The GPS satellites transmit signals in the so-called L-band (i.e. 1 to 2
GHz range) of the electromagnetic radio frequency spectrum. GPS uses
Code Division Multiple Access (CDMA) to allow different satellites to
send signals at exactly the same center frequency without interfering
with each other. The signal consists of a carrier wave on which each
satellite modulates its own unique Pseudo Random Noise (PRN) spreading
code, see Figure <a href="#fig:gpssignal" data-reference-type="ref"
data-reference="fig:gpssignal">2</a>, and, at a low rate, the satellite
orbit and clock information. The signals arrive at the receiver with an
unknown *delay* due to travelling all the way from satellite to
receiver, and due to the relative velocity of the GPS satellites with
respect to a GPS user on or near the Earth’s surface, with an unknown
*Doppler frequency shift*.

<figure id="fig:gpssignal" data-latex-placement="bht">
<div class="center">

</div>
<figcaption>The GPS L1 CA-signal is composed of a carrier wave (a
sinusoid with a frequency of 1575.42 MHz; not to scale in the above
diagram), a spreading code (a sequence of ‘0’ and ‘1’ bits/chips, here
represented by values ‘-1’ and ‘+1’, and unique for each satellite), and
a low rate navigation data message. Both the spreading code and
navigation message are phase-modulated on the carrier wave, through a
technique called Binary Phase Shift Keying (BPSK); basically multiplying
the carrier by the ‘-1’ and ‘+1’ values of the spreading code and
navigation data, and the resulting modulated signal is shown at bottom.
For the so-called CA-code on the GPS L1-frequency signal, the spreading
codes are all publicly available, and GPS receivers have them built in.
CA refers to Coarse Acquisition, but can also be understood as Civilian
Access.</figcaption>
</figure>

## Measurement of range

GPS offers two types of range measurements: pseudorange measurements and
carrier phase measurements.

### Pseudorange measurement

A GPS receiver typically consists of tens to hundreds of so-called
channels, and will allocate each of these to a specific GPS (GNSS)
satellite. When a GPS receiver first starts up, it will begin to search
for a particular GPS satellite on each of its channels, by scanning
(trying) for the corresponding spreading codes at different Doppler
offsets and time delays. This is done by overlaying the received signal
with a local copy or replica of the same code and then (time) shifting
it until correlation shows a maximum (best fit, or match). The time
shift then directly yields the travel-time measurement.

Once the receiver has locked onto the *spreading code*, it can start
regularly taking pseudorange code and Doppler frequency measurements,
which are basically the shift in time (delay) and the shift in frequency
that are required to maintain the tracking lock (onto the received
satellite signal).

Through the pseudorange, the receiver measures the *travel-time* of the
radio signal from satellite ‘s’ to receiver ‘r’:
*τ*<sub>*r*</sub><sup>*s*</sup> = *t*<sub>*r*</sub> − *t*<sup>*s*</sup>
where *t*<sup>*s*</sup> is the time the signal was transmitted by the
satellite, and *t*<sub>*r*</sub> the time the signal was received at the
receiver, later noting that these clocks may, to some extent, deviate
from the true time. The measured travel-time is converted into the
pseudorange, expressed in unit meter, through
*p*<sub>*r*</sub><sup>*s*</sup> = *c**τ*<sub>*r*</sub><sup>*s*</sup>
by multiplying by the speed of light *c* in vacuum
(*c* ≈ 3 ⋅ 10<sup>8</sup> m/s).

The pseudorange represents the travel-time of the signal, and thereby
ideally the distance from satellite to receiver. In practice it is
affected by the satellite clock offset (known to the receiver through
the navigation message), the receiver clock offset, which is unknown,
and a number of additional delays, which we cover in the sequel
(Figure <a href="#fig:signalpath" data-reference-type="ref"
data-reference="fig:signalpath">10</a>), and all multiplied by the speed
of light. The clock error is addressed in . In particular the oscillator
in the receiver, driving the clock, will not behave perfectly, and hence
the receiver clock may run ahead of time, or lag behind. The time shown
by the receiver clock is denoted by *t*<sub>*r*</sub>(*t*), and it is a
function of true time *t*. It equals true time *t*, plus a so-called
clock offset *δ**t*<sub>*r*</sub>(*t*), hence
*t*<sub>*r*</sub>(*t*) = *t* + *δ**t*<sub>*r*</sub>(*t*)
When the receiver measures the travel-time, to eventually produce the
pseudorange measurement, it ‘reads’ the moment of signal arrival at its
own clock, and hence this measurement is off by an amount of
*δ**t*<sub>*r*</sub>(*t*). The travel-time can be conceived as being
obtained by ‘reading’ the receiver clock at signal reception, and
‘reading’ the satellite clock at signal transmission, hence the
*measured* travel-time reads
*τ*<sub>*r*</sub><sup>*s*</sup>(*t*) = *t*<sub>*r*</sub>(*t*) − *t*<sup>*s*</sup>(*t* − *τ*(*t*))
Mind that the (true) travel-time *τ*(*t*) is a function of time, as the
receiver may move, and the satellite for sure moves. Substituting here
the expression for *t*<sub>*r*</sub>(*t*), assuming that the satellite
clock is perfectly on time, hence
*t*<sup>*s*</sup>(*t* − *τ*(*t*)) = *t* − *τ*(*t*) (the satellites carry
atomic clocks), and multiplying by the speed of light now gives:
$$\begin{equation}
p\_{r}^{s}(t) = c \tau\_{r}^{s}(t) = \underbrace{c \tau(t)}\_{l\_{r}^{s}(t)} + \underbrace{c \delta t\_{r}(t)}\_{b\_{r}(t)}
\label{eq:pseudorange}
\end{equation}$$
where, in the absence of for instance atmospheric delays,
*l*<sub>*r*</sub><sup>*s*</sup> denotes the geometric distance between
satellite and receiver. This equation shows that the *pseudorange* is a
measure for the geometric distance *l*<sub>*r*</sub><sup>*s*</sup>,
apart from the receiver clock offset *b*<sub>*r*</sub>, and hence the
term *pseudo*-range.

### Carrier phase measurement

Additionally, a GPS receiver may measure the *fractional* phase
difference between the received carrier wave from the satellite and a
locally generated copy (replica). And, it can keep track of the number
of cycles of the carrier wave since the start of tracking, together
known as the *carrier phase* (CP) measurement. This measurement includes
the accumulated number of ‘zero-crossings’ since lock-on of the signal
(for instance, when the fractional phase jumps from 1.99*π* to 0.02*π*,
the full period is accounted for and the resulting carrier phase
measurement, output by the receiver, is 2.02*π*).

The carrier wave measurement is a very precise measure of the distance
between the satellite and the receiver, but the initial number of
carrier wave cycles is unknown, and needs to be estimated before the
carrier phase measurements can be effectively used, see
Figure <a href="#fig:ambiguity" data-reference-type="ref"
data-reference="fig:ambiguity">3</a>. The much better precision of the
carrier phase measurement with respect to the pseudorange code
measurement can be understood from
Figure <a href="#fig:gpssignal" data-reference-type="ref"
data-reference="fig:gpssignal">2</a>, since the carrier period is much
smaller than the code chip duration (for the L1 CA-code signal, 1540
periods of the carrier fit in one chip of the Pseudo Random Noise (PRN)
spreading code).

<figure id="fig:ambiguity" data-latex-placement="bht">
<div class="center">

</div>
<figcaption>Carrier phase measurement: only the <em>fractional</em>
phase difference can be measured, shown in red in units of length [m]
(with <span class="math inline"><em>Φ</em> ∈ [0, 2<em>π</em>⟩</span>
when expressed in radians; <span class="math inline">$\varphi = \lambda
\frac{\Phi}{2\pi}$</span>), and the total distance from the satellite to
the receiver equals multiple wavelengths <span
class="math inline"><em>λ</em></span> plus the fractional phase
difference. The carrier wave is sent continuously, and the receiver
cannot distinguish one cycle from another. The unknown integer number of
wavelengths, <span class="math inline"><em>N</em></span>, at the start
of signal tracking, is referred to as ambiguity. In this example <span
class="math inline"><em>N</em> = 4</span>.</figcaption>
</figure>

### Concluding remarks

Linking to the exposition on measuring distances in , the pseudorange
measurement corresponds to ‘pulse-based’-ranging, and the carrier phase
measurement obviously to ‘phase-based’-ranging, see on the principles of
ranging, though one should note that GPS is about *one-way* ranging
(rather than two-way ranging, as in ).

The receiver can also measure the received *signal-strength*, through
the so-called carrier-to-noise-density ratio C/N0, which gives an
indication of the quality of the measurement (larger signal-strength
yields more precise measurement).

And some receivers output also the measurement of the *Doppler
frequency* of the carrier wave, which is a measure for the (relative)
velocity of the receiver with respect to the satellite (along the line
of sight), see also . The Doppler frequency, multiplied by the
wavelength, presents the range-rate *l̇*<sub>*r*</sub><sup>*s*</sup>,
that is, the change in range *l*<sub>*r*</sub><sup>*s*</sup>(*t*) per
unit time.

The measurements can be stored, e.g. for the purpose of later analysis
and processing, in receiver manufacturer proprietary format or in a
generally accepted exchange format, namely RINEX, see .

The pseudorange measurement precision is typically at the one or few
meter level for low-cost, mass-market equipment, and can get down to the
few decimeter level for professional high-end equipment.

The carrier phase measurement precision ranges from the few centimeter
to the millimeter level. The carrier phase is an ambiguous measurement
of distance, but it is more precise than the pseudorange, typically by
two orders of magnitude.

<figure id="fig:graphsC1L1D1" data-latex-placement="bht">
<div class="center">

</div>
<figcaption>Example of time series of (at left) C1 pseudorange
measurements, in meter, (in the middle) L1 carrier phase measurements,
in cycles, and (at right) D1 Doppler frequency measurements, in Hertz,
of a stationary, permanent receiver in Delft, cf. Figure <a
href="#fig:skyplot" data-reference-type="ref"
data-reference="fig:skyplot">22</a>, tracking GPS satellite
PRN20.</figcaption>
</figure>

Figure <a href="#fig:graphsC1L1D1" data-reference-type="ref"
data-reference="fig:graphsC1L1D1">4</a> shows measurements, collected by
a stationary receiver in Delft, on signals received from GPS satellite
PRN20, as a function of time. A pass-over of a GPS satellite typically
takes several, up to 7 hours. With a nearly circular orbit of the GPS
satellite around the Earth, the distance from satellite to receiver is
shortest when the satellite is directly overhead. By default actually
the negative of the Doppler frequency is output by the GPS receiver (as
shown in the graph at right, the measured Doppler frequency is positive
(in the interval from about 7-10 hours), while the distance at the same
time, as shown in the graph at left, is decreasing).

## Multi-frequency ranging

One of the major error sources in GPS is due to the ionosphere, see also
Figure <a href="#fig:signalpath" data-reference-type="ref"
data-reference="fig:signalpath">10</a> and
Table <a href="#tab:errorbudget" data-reference-type="ref"
data-reference="tab:errorbudget">1</a>. The ionosphere is a ionized part
of the Earth’s upper atmosphere. There ultraviolet (UV) solar radiation
separates electrons from neutral gas atoms and molecules. The free
electrons in the ionosphere delay the radio signals, and thus affect the
range measurements, with delays in terms of distance ranging from a few
meter to hundreds of meters.

The largest delays occur round the geomagnetic equator around local
noon, and during solar maxima. The ionospheric delay may be highly
variable, as a function of both time and space.

One way of dealing with the ionospheric delay is to track signals from
the same satellite on two or more frequencies. The ionosphere delay
scales, to a very good approximation, with the inverse of the square of
the radio frequency of the signal, and this relation can be used to
create the so-called ionosphere-free range measurements (a linear
combination of measurements at two different frequencies, from which the
ionospheric delay has been removed). For this reason the GPS satellites
were originally designed to transmit ranging signals on both the L1
(1575.42 MHz) and L2 (1227.60 MHz) frequency.

# Positioning

GPS positioning is based on the concept of multi-lateration (not
triangulation). By measuring distances to a number of GPS satellites, as
shown in Figure <a href="#fig:GPSpositioning" data-reference-type="ref"
data-reference="fig:GPSpositioning">5</a>, and using the known satellite
positions, a GPS receiver can compute its own position. To estimate the
three position coordinates of the receiver *x*<sub>*r*</sub>,
*y*<sub>*r*</sub>, *z*<sub>*r*</sub>, and the receiver clock offset
*b*<sub>*r*</sub>, a GPS receiver needs to track at least 4 satellites.

<figure id="fig:GPSpositioning" data-latex-placement="bht">
<div class="center">

</div>
<figcaption>GPS positioning — in three dimensions — is based on
measuring pseudoranges to at least four satellites, of which the
positions are known. Visualization by Axel Smits <span class="citation"
data-cites="smitsGPS"></span>.</figcaption>
</figure>

## Geometric interpretation

Knowing ones distance to an object (satellite) at a known position,
translates into being on a circle (in 2D) or a sphere (in 3D) around
this object (with the satellite in the center). As we have seen with
(<a href="#eq:pseudorange" data-reference-type="ref"
data-reference="eq:pseudorange">[eq:pseudorange]</a>), the GPS
pseudorange measurement relates to the geometric range (distance) from
satellite to receiver, but, also to an offset caused by the receiver
clock! This means, the pseudorange gives us the distance from satellite
to receiver, but it may or will be too small, or too large by a certain
amount, namely the receiver clock offset *b*. The good news is that the
receiver clock offset is the *same* for all pseudoranges measured by the
receiver at a specific time. If the receiver clock is ahead of GPS-time,
all pseudoranges will be measured too long, and by the same amount. This
leads us to the approach of solving for three position coordinates and
the receiver clock error at the same time, and hence, requiring
pseudorange measurements to at least four satellites (rather than
three).

To see the effect of the receiver clock error on the positioning problem
at work, we consider a simple two-dimensional positioning example (in
which we assume that there is no effect of noise present in the
pseudorange measurements). So, in two dimensions, we would need to solve
for two receiver position coordinates and one receiver clock error,
hence in total three unknown parameters, so we need at least three
pseudorange measurements.

<figure id="fig:trilaterationgreenblue" data-latex-placement="bht">
<div class="center">

</div>
<figcaption>Two-dimensional positioning example with three satellites
(at known positions, represented by the black dots). The measured
pseudoranges are visualized by circles, in green at left, and in blue at
right.</figcaption>
</figure>

<figure id="fig:trilateration" data-latex-placement="bht">
<div class="center">

</div>
<figcaption>The process of determining the receiver clock offset: the
measured pseudoranges have to be reduced or enlarged, but all with
exactly the same amount, in order to meet at one physical position. The
amount to make that happen is the receiver clock offset. The different
colors represent different values for the receiver clock
offset.</figcaption>
</figure>

In
Figure <a href="#fig:trilaterationgreenblue" data-reference-type="ref"
data-reference="fig:trilaterationgreenblue">6</a> at left, the measured
pseudoranges are shown in green, and apparently these three green
circles do not all meet in one point. The pseudoranges are ‘too short’,
the reason obviously being the receiver clock lagging behind. When the
radii of the green circles are enlarged, all by exactly the same amount,
to yield the blue circles, as shown at right, we arrive at an
intersection of all three circles in one point. We have solved for the
two position coordinates, and the receiver clock offset as well[^1].
This clearly demonstrates that positioning and timing are intimately
related!

## Pseudorange observation equation

With expanding the one-way geometric range
*l*<sub>*r*</sub><sup>*s*</sup> between satellite ‘s’ and receiver ‘r’
as
$$l\_{r}^{s} = \sqrt{(x^s-x_r)^2 + (y^s-y_r)^2 + (z^s-z_r)^2}$$
using a three-dimensional Cartesian coordinate system as shown in
Figure <a href="#fig:ECEF" data-reference-type="ref"
data-reference="fig:ECEF">8</a>, pseudorange observation
Eq. (<a href="#eq:pseudorange" data-reference-type="ref"
data-reference="eq:pseudorange">[eq:pseudorange]</a>) turns into
$$\begin{equation}
\underline{p}\_{r}^{s} = \sqrt{(x^s-x_r)^2 + (y^s-y_r)^2 + (z^s-z_r)^2} + b_r + \underline{e}\_{r}^{s}
\label{eq:pseudorangeobseqn}
\end{equation}$$
where we omitted the argument of time *t*. The satellite position
coordinates at time of signal transmission are *x*<sup>*s*</sup>,
*y*<sup>*s*</sup> and *z*<sup>*s*</sup>, and the receiver position
coordinates at time of signal reception are *x*<sub>*r*</sub>,
*y*<sub>*r*</sub> and *z*<sub>*r*</sub>. The satellite position, as well
as the satellite clock offset, is available to the user through the
navigation data message,
cf. Figure <a href="#fig:gpssignal" data-reference-type="ref"
data-reference="fig:gpssignal">2</a>. Parameter *b*<sub>*r*</sub> equals
the receiver clock offset *δ**t*<sub>*r*</sub> multiplied by the speed
of light *c*, cf. (<a href="#eq:pseudorange" data-reference-type="ref"
data-reference="eq:pseudorange">[eq:pseudorange]</a>). If the receiver
clock is ahead of GPS system time, *b*<sub>*r*</sub> is positive, and
the measured pseudoranges are ‘too long’. And finally note that we
included the (unavoidable) random measurement error
$\underline{e}\_{r}^{s}$ on the right hand side of
Eq. (<a href="#eq:pseudorangeobseqn" data-reference-type="ref"
data-reference="eq:pseudorangeobseqn">[eq:pseudorangeobseqn]</a>).

<figure id="fig:ECEF" data-latex-placement="bht">
<div class="center">

</div>
<figcaption>Three-dimensional Cartesian Earth-Centered Earth-Fixed
(ECEF) coordinate system for GPS positioning.</figcaption>
</figure>

## Positioning: parameter estimation

In practice, as one typically observes more satellites than the minimum
of four, GPS positioning does not actually involve drawing circles or
spheres, but employs the principle of least squares estimation. First
the observation model is defined, which links the observations to the
unknown parameters.

Since the GPS observation model is non-linear, this involves a
linearisation with respect to the unknown parameters, around an
approximate position, see . The linearized model of observation
equations reads
$$\begin{equation}
\underbrace{
\left( \begin{array}{c} \Delta \underline{p}\_{r}^{1} \\ \Delta \underline{p}\_{r}^{2} \\ \vdots \\ \Delta \underline{p}\_{r}^{m} \end{array} \right)
}\_{\Delta \underline{y}} =
\underbrace{
\left( \begin{array}{cccc} -u\_{r,x}^{1} & -u\_{r,y}^{1} & -u\_{r,z}^{1} & 1  \\ 
                           -u\_{r,x}^{2} & -u\_{r,y}^{2} & -u\_{r,z}^{2} & 1  \\
                              \vdots    &   \vdots     &   \vdots     & \vdots \\
                           -u\_{r,x}^{m} & -u\_{r,y}^{m} & -u\_{r,z}^{m} & 1  \\
\end{array} \right)
}\_{A}
\underbrace{
\left( \begin{array}{c} \Delta x\_{r} \\ \Delta y\_{r} \\ \Delta z\_{r} \\ b_r \end{array} \right)
}\_{\Delta x} +
\underbrace{
\left( \begin{array}{c} \underline{e}\_{r}^{1} \\ \underline{e}\_{r}^{2} \\  \vdots \\ \underline{e}\_{r}^{m} \end{array} \right)
}\_{\underline{e}}
\label{eq:standalonemodel}
\end{equation}$$
where we assume to have *m* satellites in view. presents the
linearization of a distance observation equation in two dimensions, and
extension into three dimensions is straightforward. The coefficients in
the above design-matrix for the coordinate parameters are actually the
elements of the unit-direction vector *u*<sub>*r*</sub><sup>*s*</sup>
from the receiver ‘r’, pointing to the satellite ‘s’, cf. (). The above
model carries *m* observations and 4 unknown parameters, and hence the
redundancy equals *m* − 4.

Next, a least-squares algorithm is used to solve this linearized model,
presented in matrix-vector form. When an *m* × *m* variance matrix of
the pseudorange observables is involved, a Best Linear Unbiased
Estimation solution can be obtained, which minimizes the uncertainty of
the solution (see . Then one can also obtain the variance matrix of the
parameter estimators, through (), and analyse the precision of the
position coordinates.

Most users of GPS are interested in position coordinates
*x*<sub>*r*</sub>, *y*<sub>*r*</sub>, and *z*<sub>*r*</sub>. Through
knowledge of the receiver clock offset
*b*<sub>*r*</sub> = *c**δ**t*<sub>*r*</sub> one has in fact access to
GPS system time, which is an atomic time scale, and thereby also to UTC
(Coordinated Universal Time).

Similar to the position coordinates estimation based on pseudorange
measurements, the three-dimensional velocity vector of the receiver can
be estimated from the measured Doppler shift measurements,
cf. Section <a href="#sec:concludingremarkobs" data-reference-type="ref"
data-reference="sec:concludingremarkobs">2.2.3</a>.

A well-known and widely used format for storing and exchanging GPS
(GNSS) Position, Velocity and Time (PVT) solutions is NMEA, see .

## Reference systems

Relying, by default, on the given satellite positions in the navigation
message of the GPS signal, GPS positioning yields Cartesian coordinates
(*x*, *y*, *z*) in WGS84, the World Geodetic System 1984, which is an
Earth-Fixed, Earth-Centered (ECEF) coordinate system, as presented in
Figure <a href="#fig:ECEF" data-reference-type="ref"
data-reference="fig:ECEF">8</a>. These Cartesian coordinates can be
converted into geographic, or ellipsoidal coordinates latitude *φ*,
longitude *λ*, and ellipsoidal height *h*, see Chapter X.

In differential mode (introduced in the next section), the position
coordinates for the user receiver are in the same reference system as
the position coordinates of the base, or reference station, generally
provided in a local or regional reference system (e.g. ETRS89 in Europe,
a realization of the European Terrestrial Reference System).

## GPS accuracy and error sources

The quality of the GPS position solution is largely dependent on the
number of available satellites and their geometry with respect to the
user. If enough satellites are visible on all sides of the receiver, at
high and low elevation angles, a good position accuracy can be expected.
The only weakness in the geometry is the fact that there are no
satellites visible beneath the receiver, as one cannot track and observe
satellites below the local horizon. As a result vertical position
accuracy is generally poorer than the horizontal accuracy by about a
factor of 1.5.

In many practical situations one or more satellite signals are *blocked*
by surrounding buildings or other obstacles which is called shadowing.
In this case GPS performance might be significantly degraded.
Furthermore, in built-up areas, GPS receivers often experience signal
reflections, i.e. signals arrive at the receiver after bouncing off an
object. Since the reflected signal path is always longer than the direct
path, this causes a corresponding error in the range measurement. It is
also possible that both the direct and reflected signals arrive at the
receiver, which is referred to as *multipath*. In this case, the
receiver must deal with the superposition of these signals, generally
resulting in a biased range measurement, see
Figure <a href="#fig:multipath" data-reference-type="ref"
data-reference="fig:multipath">9</a>.

Carefully selecting the location for a survey can help to keep the
impact of multipath at a minimum, as well as the use of a good antenna.

<figure id="fig:multipath" data-latex-placement="bht">
<div class="center">

</div>
<figcaption>Multipath: the direct line of sight signal from the
satellite is received, though as well as a signal which has been
reflected by the building. The reception of also a reflected signal,
which has made a detour, will generally cause a bias in the
measurement.</figcaption>
</figure>

<figure id="fig:signalpath" data-latex-placement="bht">
<div class="center">

</div>
<figcaption>GPS error sources. The receiver clock offset (shown in faded
green) is accounted for in the observation equation (<a
href="#eq:pseudorangeobseqn" data-reference-type="ref"
data-reference="eq:pseudorangeobseqn">[eq:pseudorangeobseqn]</a>), and
hence not to be considered as an error source.</figcaption>
</figure>

| error source    | 95%-value |
|:----------------|:---------:|
| satellite orbit |    2 m    |
| satellite clock |   2-5 m   |
| ionosphere      |  15-90 m  |
| troposphere     |   20 m    |
| multipath       |  1-10 m   |
| receiver noise  |   1-3 m   |
| total range     |  5-10 m   |

GPS error budget for standalone positioning, see also
Figure <a href="#fig:signalpath" data-reference-type="ref"
data-reference="fig:signalpath">10</a>. The errors are given in the
range domain, using the satellite (broadcast) navigation data message,
and after Klobuchar ionospheric model correction (which in practice
yields a 50% reduction of the ionospheric delay error), as well as
tropospheric delay correction based on an a-priori (blind) model (which
yields about 90% of reduction of the tropospheric delay error). The
larger values for ionospheric and tropospheric delay may occur for slant
ranges to satellites at low elevation.

The accuracy of *standalone positioning* with GPS, also referred to as
single-point positioning, or absolute positioning, according to model
(<a href="#eq:standalonemodel" data-reference-type="ref"
data-reference="eq:standalonemodel">[eq:standalonemodel]</a>), in the
order of 5-15 meters under reasonable satellite visibility, is limited
by the accuracy of the range measurements (time can be determined
correspondingly with a tens of nanoseconds accuracy). The GPS
pseudorange measurements contain errors due to inaccurate satellite
orbit and clock information, delays along the path of the radio signal,
including atmospheric delays (ionosphere and troposphere), local effects
including multipath, and measurement noise, see
Figure <a href="#fig:signalpath" data-reference-type="ref"
data-reference="fig:signalpath">10</a> and
Table <a href="#tab:errorbudget" data-reference-type="ref"
data-reference="tab:errorbudget">1</a>.

Finally it is mentioned that a GPS receiver, using electromagnetic
signals received from the satellites, determines the position of the
antenna phase center (typically a point inside or slightly above the
antenna) as this is where the radio signals actually arrive. Handling
the so-called antenna Phase Center Offset (PCO) with respect to the
bottom of the antenna, usually a cm to dm-effect, is important in
high-precision positioning discussed in the next section.

<figure id="fig:CTB3310surveymarker" data-latex-placement="bht">
<div class="center">

</div>
<figcaption>Survey-marker at TU Delft campus with accurate ground-truth
coordinates: <span class="math inline"><em>X</em></span> =
3923768.0147 m, <span class="math inline"><em>Y</em></span> =
300255.7048 m, <span class="math inline"><em>Z</em></span> =
5002640.2228 m (ITRF2014 at epoch 2021.50).</figcaption>
</figure>

<figure id="fig:spppos" data-latex-placement="bht">
<div class="center">

</div>
<figcaption>Example of GNSS standalone positioning for a duration of
5000 seconds at a 5 second interval, on September 2nd, 2021, with
measurements to about 25 GNSS satellites. At left: scatter of horizontal
position error, at right: time series of vertical position
error.</figcaption>
</figure>

## Standalone positioning: example

With the equipment of
Figure <a href="#fig:ublox" data-reference-type="ref"
data-reference="fig:ublox">19</a> a short experiment was carried out,
lasting 5000 seconds. The antenna was installed on a survey-marker on
the TU Delft campus, of which accurate position coordinates were already
available, see
Figure <a href="#fig:CTB3310surveymarker" data-reference-type="ref"
data-reference="fig:CTB3310surveymarker">11</a>. The receiver ran in
so-called standalone positioning or single-point positioning mode, and
every 5th position solution was saved, hence the results shown in
Figure <a href="#fig:spppos" data-reference-type="ref"
data-reference="fig:spppos">12</a> are obtained at a 5 second interval.

The graph at left shows the horizontal position scatter,
North-coordinate versus East-coordinate, and the graph at right shows
the vertical position (Up) as a function of time. With the given
coordinates of the marker, we actually present the position *error* in
Figure <a href="#fig:spppos" data-reference-type="ref"
data-reference="fig:spppos">12</a>, i.e. the difference of the measured
position coordinate and the known ground-truth position coordinate.
Hence, the origin of this graph refers to the ‘true’ position. The
position errors are expressed in a local topocentric coordinate system,
in terms of local East, North and Up, see .

Table <a href="#tab:spppos" data-reference-type="ref"
data-reference="tab:spppos">2</a> presents the resulting empirical mean,
standard deviation (std) and the root mean square (rms), which is the
square root of the MSE, see , of the position error in East, North and
Up, showing a better than 1 meter accuracy of GNSS standalone
positioning using over 25 GNSS satellites.

|            | East | North |  Up   |
|:-----------|:----:|:-----:|:-----:|
| mean \[m\] | 0.51 | 0.23  | -0.47 |
| std \[m\]  | 0.15 | 0.35  | 0.41  |
| rms \[m\]  | 0.53 | 0.42  | 0.62  |

Empirical mean, standard deviation (std) and root mean square (rms) of
position error, based on *N*=1000 GNSS standalone position solutions.

# GPS positioning modes

Several techniques have been developed to improve on the GPS Standard
Positioning Service (SPS) accuracy (standalone positioning, as discussed
in the previous section). Firstly, GPS satellites broadcast a second,
more precise, code on the same carrier wave, to provide the Precise
Positioning Service (PPS). However, this code is encrypted and can only
be used to full extent by the US military.

Fortunately, even more accurate positioning modes are available, all
relying on a kind of *augmentation*. This means that, next to the
measurements collected by the user receiver, in addition measurements
are used of a nearby permanent GPS receiver, and/or that one relies in
addition on data products derived from a network of permanent tracking
stations. Such a network could provide precise estimates of the
satellite positions for instance (more precise than what we by default
encounter in the navigation message on the GPS signal).

## Relative positioning, or DGPS

Differential GPS (DGPS) uses a data link to a nearby base or reference
station, i.e. another GPS receiver at an accurately known position, and
the *relative position* between the two is obtained. Measurement data
from this base station are used, to reduce the effects of the
atmospheric delays, satellite clock offsets and orbit errors. This can
be achieved by differencing the observations from both receivers to the
same satellites, which eliminates these (common) errors, which affect
both receivers almost identically if the distance between them is small
enough, typically in the order of 5 to 10 km, considering that the
satellites are at 20.000 km distance, see
Figure <a href="#fig:dgps" data-reference-type="ref"
data-reference="fig:dgps">13</a>.

From the differenced observations, the so-called baseline (vector)
between the two receivers can be computed through least-squares
estimation. The position of the rover is then obtained by adding the
baseline vector to the accurately known coordinates of the reference
station. Generally the term ‘DGPS’ is used for relative positioning,
though using only pseudorange measurements.

<figure id="fig:dgps" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>Relative GPS positioning combines measurements from a roving
receiver with measurements from a reference (or base) station. The
position of the rover is actually computed <em>relative</em> to the
position of the base station. A number of errors, including atmospheric
errors, is almost identical for two receivers in close proximity to each
other. Hence, these errors cancel in relative positioning.</figcaption>
</figure>

### Real-Time Kinematic (RTK)

To obtain the highest possible accuracy from GPS, it is no longer
sufficient to use only the pseudorange code measurements, but rather the
*carrier phase* measurements, introduced in
Section <a href="#chap:ranging" data-reference-type="ref"
data-reference="chap:ranging">2</a>, are required. As mentioned before,
the measurement of fractional phase difference does pose the problem of
the unknown initial number of carrier wave cycles, also called the
carrier wave *ambiguity*, which need to be estimated together with the
other unknown parameters.

An ambiguity consists of a fractional part at the satellite (equal for
both receivers, and already removed by the differencing between the base
station and rover), a fractional part at the receiver (equal for all
tracked satellites), and an integer number of whole cycles. This fact of
unknown parameters being integers (rather than reals) is exploited in a
technique called *Real-Time Kinematic (RTK)* positioning, or
Carrier-Phase (CP) based baseline processing (if performed in post
processing), by selecting a reference satellite and forming a second
difference between the measurement to a reference satellite and those to
all other satellites, to eliminate the fractional part at the side of
the receiver. In this special case the double-differenced carrier phase
ambiguities can be resolved to their integer number very efficiently
through integer least-squares estimation. After only a few minutes or
within tens of seconds already, centimeter-level position accuracy can
be reached.

<figure id="fig:06GPSnetwork" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>Example of network of permanent GPS tracking stations, of a
commercial network RTK service provider in the Netherlands, Belgium and
Luxemburg. Image obtained with permission from <a
href="https://www.06-gps.nl">06-GPS</a> <span class="citation"
data-cites="Henry"></span>.</figcaption>
</figure>

The requirement for a nearby reference receiver is a disadvantage of
RTK, considering effort and/or cost. With RTK the coverage area of a
reference receiver or station typically has a radius of ten, or tens of
kilometers. In many regions and countries, networks of reference
stations, or Continuously Operating Reference Stations (CORS) have been
deployed in order to cover the entire area, and in this scenario
sometimes the term *network-RTK* is used, see
Figure <a href="#fig:06GPSnetwork" data-reference-type="ref"
data-reference="fig:06GPSnetwork">14</a>, where reference stations
generally have a 30-40 km interdistance. An example of an application of
RTK positioning in road construction is shown in
Figure <a href="#fig:excavator" data-reference-type="ref"
data-reference="fig:excavator">15</a>.

<figure id="fig:excavator" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>Excavator in the process of constructing a motorway
embankment. RTK-GPS provides accurate real-time position information to
guide this machine (note the two GPS-antennas on the back of the
engine). Image courtesy of <a
href="https://www.heijmans.nl/">Heijmans</a> <span class="citation"
data-cites="Heijmans"></span>.</figcaption>
</figure>

Many high-end GPS receivers have RTK functionality built-in, but it can
also be performed with professional software, or even with open source
software such as the RTKLIB program package .

Today the measurements of the base station are communicated, in
real-time, to the rover receiver over an Internet-connection, using
NTRIP. Networked Transport of RTCM[^2] via Internet Protocol (NTRIP) is
an application protocol that supports the streaming of (differential)
GNSS data over the Internet, based on Hyper Text Transfer Protocol
(HTTP). NTRIP has been developed by the German Federal Agency for
Cartography and Geodesy (BKG) . With the measurements of the base
station becoming available in real-time at the rover receiver,
centimeter accurate position solutions are obtained right at the spot.

### RTK — carrier phase observation equation \[\*\]

The pseudorange observation equation was presented in
(<a href="#eq:pseudorangeobseqn" data-reference-type="ref"
data-reference="eq:pseudorangeobseqn">[eq:pseudorangeobseqn]</a>) for
the purpose of standalone positioning. The errors discussed in
Section <a href="#sec:errorsources" data-reference-type="ref"
data-reference="sec:errorsources">3.5</a> were basically all ignored.

The carrier phase measurement,
Section <a href="#sec:carrierphasemeasurement" data-reference-type="ref"
data-reference="sec:carrierphasemeasurement">2.2.2</a>, is much more
precise than the pseudorange — the contribution to the error budget in
Table <a href="#tab:errorbudget" data-reference-type="ref"
data-reference="tab:errorbudget">1</a> by carrier phase multipath and
receiver noise would only be at the millimeter to a few centimeter
level. The other error sources, like atmospheric delays and satellite
related errors are taken into account now, and put together in a delay
parameter *d*<sub>*r*</sub><sup>*s*</sup>. The carrier phase observation
equation, for the phase
$\varphi\_{r}^{s} = \lambda \frac{\Phi\_{r}^{s}}{2\pi}$ expressed in
meters, reads
$$\underline{\varphi}\_{r}^{s} = \underbrace{ \sqrt{(x^s-x_r)^2 + (y^s-y_r)^2 + (z^s-z_r)^2} }\_{l\_{r}^{s}} + b_r + d\_{r}^{s} + \lambda N\_{r}^{s} + \underline{e}\_{r}^{s}$$
Parameter *N*<sub>*r*</sub><sup>*s*</sup> denotes the carrier phase
cycle ambiguity, see
Figure <a href="#fig:ambiguity" data-reference-type="ref"
data-reference="fig:ambiguity">3</a>.

### RTK — carrier phase positioning: parameter estimation \[\*\]

We use *relative* positioning and develop the model of observation
equations for a short baseline (i.e. two receivers close together, up to
10-20 km distance). The two receivers 1 and 2 being close together
implies that the delays will be very similar
*d*<sub>1</sub><sup>*s*</sup> ≈ *d*<sub>2</sub><sup>*s*</sup> (keeping
in mind that the satellite is some 20.000 km away), and in the sequel we
assume them to be really equal:
*d*<sub>1</sub><sup>*s*</sup> = *d*<sub>2</sub><sup>*s*</sup> (and
residual errors are assumed to go into the $\underline{e}$-error terms).
With the position coordinates of the reference or base station
(*x*<sub>1</sub>, *y*<sub>1</sub>, *z*<sub>1</sub>) being known, and
taking the difference of measurements across the two receivers,
*φ*<sub>1, 2</sub><sup>*s*</sup> = *φ*<sub>2</sub><sup>*s*</sup> − *φ*<sub>1</sub><sup>*s*</sup>,
we obtain
$$\begin{equation}
\left( \begin{array}{c} \Delta \underline{\varphi}\_{1,2}^{1} \\ \Delta \underline{\varphi}\_{1,2}^{2} \\ \vdots \\ \Delta \underline{\varphi}\_{1,2}^{m} \end{array} \right)
 =
\left( \begin{array}{cccccccc} -u\_{2,x}^{1} & -u\_{2,y}^{1} & -u\_{2,z}^{1} & 1 & \lambda & & &  \\ 
                               -u\_{2,x}^{2} & -u\_{2,y}^{2} & -u\_{2,z}^{2} & 1 & & \lambda & &  \\
                                  \vdots    &   \vdots     &   \vdots     & \vdots & & & \ddots & \\
                               -u\_{2,x}^{m} & -u\_{2,y}^{m} & -u\_{2,z}^{m} & 1 & & & & \lambda  \\
\end{array} \right)
\left( \begin{array}{c} \Delta x\_{2} \\ \Delta y\_{2} \\ \Delta z\_{2} \\ b\_{1,2} \\ N\_{1,2}^{1} \\ N\_{1,2}^{2} \\ \vdots \\ N\_{1,2}^{m} \end{array} \right) +
\left( \begin{array}{c} \underline{e}\_{1,2}^{1} \\ \underline{e}\_{1,2}^{2} \\  \vdots \\ \underline{e}\_{1,2}^{m} \end{array} \right)
\end{equation}$$
with *b*<sub>1, 2</sub> = *b*<sub>2</sub> − *b*<sub>1</sub>,
*N*<sub>1, 2</sub><sup>*s*</sup> = *N*<sub>2</sub><sup>*s*</sup> − *N*<sub>1</sub><sup>*s*</sup>
and
$\underline{e}\_{1,2}^{s} = \underline{e}\_{2}^{s} - \underline{e}\_{1}^{s}$.
Note that when we would leave the ambiguities *N* out, the above model
in structure very much resembles model
(<a href="#eq:standalonemodel" data-reference-type="ref"
data-reference="eq:standalonemodel">[eq:standalonemodel]</a>) for
standalone positioning. The goal of RTK-positioning is to estimate the
position coordinates of the rover receiver *x*<sub>2</sub>,
*y*<sub>2</sub>, and *z*<sub>2</sub>, and this is done while keeping the
reference station fixed to the given position coordinates.

In the above model the receiver clock offset parameter
*b*<sub>1, 2</sub>, as it is appearing equally in all equations, can be
removed by taking differences between measurements,
e.g. *φ*<sub>1, 2</sub><sup>1, 2</sup> = *φ*<sub>1, 2</sub><sup>2</sup> − *φ*<sub>1, 2</sub><sup>1</sup>.
The resulting model of taking differences all with respect to the first
measurement *φ*<sub>1, 2</sub><sup>1</sup>, reads
$$\begin{equation}
\left( \begin{array}{c} \Delta \underline{\varphi}\_{1,2}^{1,2} \\ \vdots \\ \Delta \underline{\varphi}\_{1,2}^{1,m} \end{array} \right)
 =
\left( \begin{array}{cccccc} -(u\_{2,x}^{2}-u\_{2,x}^{1}) & -(u\_{2,y}^{2}-u\_{2,y}^{1}) & -(u\_{2,z}^{2}-u\_{2,z}^{1}) & \lambda & & \\ 
                                  \vdots    &   \vdots     &   \vdots     &  & \ddots & \\
                             -(u\_{2,x}^{m}-u\_{2,x}^{1}) & -(u\_{2,y}^{m}-u\_{2,y}^{1}) & -(u\_{2,z}^{m}-u\_{2,z}^{1}) & & & \lambda  \\
\end{array} \right)
\left( \begin{array}{c} \Delta x\_{2} \\ \Delta y\_{2} \\ \Delta z\_{2} \\ N\_{1,2}^{1,2} \\ \vdots \\ N\_{1,2}^{1,m} \end{array} \right) +
\left( \begin{array}{c} \underline{e}\_{1,2}^{1,2} \\ \vdots \\ \underline{e}\_{1,2}^{1,m} \end{array} \right)
\end{equation}$$
With carrier phase measurements to *m* satellites, we have (*m* − 1) of
these so-called double difference measurements. The receiver clock
offset parameter has been cancelled.

These two optional sections provide a very brief introduction to carrier
phase based positioning. For a more in-depth coverage, the reader is
referred to . Least-squares estimation of *integer* parameters, such as
the ambiguities *N*, is simple when there is only one. Ordinary
least-squares estimation yields a real-valued estimate for this
parameter, and rounding it to the nearest integer yields the integer
least-squares estimate for the ambiguity. With more ambiguity parameters
present in the problem at the same time, as in the above model, this
becomes a seriously complex problem (for which an adequate solution is
provided by the LAMBDA-method ).

Figure <a href="#fig:ambiguouspositioning" data-reference-type="ref"
data-reference="fig:ambiguouspositioning">16</a> provides a simple
geometric interpretation of relative positioning with carrier phase
measurements which are inherently ambiguous, as only the fractional
phase can be measured. The rover receiver has to lie on one of the blue
circle arcs, and at the same time on one of the green circle arcs. The
different arcs represent different integer values for the ambiguity. The
rover receiver is at one of the intersections, but as long as the
ambiguities are not known, it is not known at which one. For this
geometric interpretation it is assumed that there is no effect of noise
present in the measurements, and the receiver clocks are assumed to
behave perfectly (*b*<sub>1</sub> = *b*<sub>2</sub> = 0).

<figure id="fig:ambiguouspositioning" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>Geometric interpretation of relative positioning with
carrier phase measurements, which are inherently <em>ambiguous</em>. The
blue circle arcs, as possible solution for the rover receiver position
result from the carrier phase measurement to the blue satellite, and the
green circle arcs to those to the green satellite. The arcs are spaced
by one wavelength <span class="math inline"><em>λ</em></span> of the
carrier wave.</figcaption>
</figure>

### RTK — carrier phase positioning: example

With the equipment of
Figure <a href="#fig:ublox" data-reference-type="ref"
data-reference="fig:ublox">19</a> a short experiment was carried out,
lasting 1000 seconds. Using measurements from a permanent GNSS reference
station (only 2 km away,
cf. Figure <a href="#fig:skyplot" data-reference-type="ref"
data-reference="fig:skyplot">22</a>), received in real-time using NTRIP,
the receiver provided so-called RTK-fixed solutions (in ETRF2000). For
every epoch, i.e. once every second, a new position solution was
computed, and the results are shown in
Figure <a href="#fig:rtkfix" data-reference-type="ref"
data-reference="fig:rtkfix">17</a>. The graph at left shows the
horizontal position scatter, North-coordinate versus East-coordinate,
and the graph at right shows the vertical position (Up) as a function of
time. These measurements were taken at a survey-marker of which accurate
position coordinates were already available
cf. Figure <a href="#fig:CTB3310surveymarker" data-reference-type="ref"
data-reference="fig:CTB3310surveymarker">11</a>, so, in the graph of
Figure <a href="#fig:rtkfix" data-reference-type="ref"
data-reference="fig:rtkfix">17</a> we actually present the position
*error*, i.e. the difference of the measured position coordinate and the
known ground-truth position coordinate. Hence, the origin of this graph
refers to the ‘true’ position. The position errors are expressed in a
local topocentric coordinate system, in terms of local East, North and
Up, see .

<figure id="fig:rtkfix" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>Example of Carrier Phase (CP) Real-Time Kinematic (RTK)
positioning for a duration of 1000 seconds, on August 27th, 2021, with
measurements of about 25 GNSS satellites, and successfully fixing the
carrier phase ambiguities (RTK-fixed solution). At left: scatter of
horizontal position error, at right: time series of vertical position
error.</figcaption>
</figure>

Table <a href="#tab:rtkfix" data-reference-type="ref"
data-reference="tab:rtkfix">3</a> presents the resulting empirical mean,
standard deviation (std) and the root mean square (rms), which is the
square root of the MSE, see , of the position error in East, North and
Up, confirming centimeter-accuracy of RTK-GPS positioning. This is an
improvement by a factor of 100 compared to the standalone positioning
results in Figure <a href="#fig:spppos" data-reference-type="ref"
data-reference="fig:spppos">12</a>.

|            |  East  | North  |   Up   |
|:-----------|:------:|:------:|:------:|
| mean \[m\] | 0.0016 | 0.0021 | 0.0068 |
| std \[m\]  | 0.0033 | 0.0039 | 0.0072 |
| rms \[m\]  | 0.0037 | 0.0044 | 0.0099 |

Empirical mean, standard deviation (std) and root mean square (rms) of
position error, based on *N*=1000 Carrier Phase (CP) Real-Time Kinematic
(RTK) position solutions (with ambiguities fixed).

### RTK — carrier phase positioning: Digital Terrain Model (DTM)

Another short experiment was carried out to result in a
centimeter-accurate 3D Digital Terrain Model (DTM) of an embankment on
the TU Delft campus, see
Figure <a href="#fig:talud" data-reference-type="ref"
data-reference="fig:talud">18</a>. The RTK survey of this bank of earth
took only 15 minutes (walking with the GNSS-receiver in a grid-like
pattern over this bank, and recording measurements every 1 second).

<figure id="fig:talud" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>Example of a centimeter-accurate 3D Digital Terrain Model
(DTM) resulting from Carrier Phase (CP) Real-Time Kinematic (RTK)
positioning. The DTM is presented in the national RD-NAP reference
system (see <span class="citation" data-cites="Tiberius_2022"></span>),
actually with x-85600 m, and y-445900 m. The DTM is viewed from the
South-East, like the photo on the left.</figcaption>
</figure>

The RTK-fixed position solutions have been interpolated, and the
resulting DTM is shown at right in
Figure <a href="#fig:talud" data-reference-type="ref"
data-reference="fig:talud">18</a>. With the DTM one can easily evaluate
numerically the amount of earthwork needed to create or remove this
bank, in this case 442 m<sup>3</sup>.

### Precise Point Positioning (PPP)

In those instances where a nearby reference receiver (or network) is not
available or cost-prohibitive, Precise Point Positioning (PPP) is an
attractive alternative. PPP only relies on a *global*, very sparse
network of reference receivers (e.g. some 40 receivers worldwide, and
the nearest reference station can be 1000 km away, or even further),
which track the GPS satellites and compute corrections to the errors in
the satellite orbits and clocks. Conventional PPP uses dual-frequency
data to eliminate the ionosphere delay, while a low-cost variant uses
single frequency data with a (predicted) ionosphere model. The
fractional carrier phase ambiguities cannot be eliminated, which means
that integer least-squares estimation is not possible. Ambiguities can
still be estimated as constant values though, since an ambiguity does
not change as long as the receiver keeps tracking the satellite, a fact
used in the PPP data processing.

However, because the ambiguities cannot be fixed to integer values, PPP
suffers from a longer convergence period than RTK (think of tens of
minutes). After a convergence period in which the accuracy of the
estimated ambiguities improves gradually, the PPP solution starts
relying more and more on the phase measurements. The eventual position
accuracy for dual-frequency PPP can reach centimeter, or even millimeter
level, while single frequency PPP can reach an accuracy of a few
decimeter.

## Current developments

Much research effort is spent to try and combine the best aspects of PPP
and RTK, i.e. using a sparse (global) reference network and ambiguity
resolution to enable precise positioning. Wide Area RTK and PPP-RTK are
based on the principles of RTK, but try to stretch the interstation
distances to several hundreds of kilometers, while PPP-AR starts from
the global PPP network, and tries to solve the problem of ambiguity
resolution (AR). The ultimate goal is to achieve high precision
positioning across a (very) large area.

<figure id="fig:ublox" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>At left: dual-frequency, multi-constellation GNSS receiver
with receiver board at bottom, small patch-antenna (black) on top, and
smartphone with Android positioning app at right; a total equipment cost
of below 500 Euro (u-blox ZED-F9P), yet capable of providing cm-accurate
RTK-GNSS positioning. At right: screenshot of SW Maps app by Softwel (P)
Ltd.</figcaption>
</figure>

Another development is to bring high-accuracy positioning techniques,
e.g. RTK and PPP, to low-cost devices. An example is shown in
Figure <a href="#fig:ublox" data-reference-type="ref"
data-reference="fig:ublox">19</a>. The smartphone retrieves GPS
differential corrections (or measurements) of a nearby reference station
through an Internet-connection using NTRIP, and forwards these to the
GPS receiver, which is connected via USB to the smartphone. The firmware
on the GPS receiver chip combines the corrections with the measurements
of the rover receiver, and delivers a centimeter accurate RTK-position
solution, which it relays back to the app on the smartphone. This allows
for centimeter accurate navigation, in real-time, with your smartphone.

The antenna of the rover receiver, at right in
Figure <a href="#fig:dgps" data-reference-type="ref"
data-reference="fig:dgps">13</a>, is typically mounted on a lightweight
range-pole, for convenience of the survey-job. The position of the
antenna on top of the range-pole is being measured (with GPS), and the
obtained coordinates are converted into those of the object or marker
point occupied by the bottom-tip of the range-pole, using the fact that
the range-pole is being held vertically straight-up, and knowing its
size.

Recently range-poles with built-in tilt compensation have become
available. The tilt angle *ζ* is being measured, for instance by means
of an inertial measurement unit, and the horizontal displacement or
offset is simply found as *l*sin *ζ*, see
Figure <a href="#fig:tiltcompensation" data-reference-type="ref"
data-reference="fig:tiltcompensation">20</a>.

<figure id="fig:tiltcompensation" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>Principle of GPS range pole with tilt compensation. Tilt
angle <span class="math inline"><em>ζ</em></span> is measured to
provide, with known size <span class="math inline"><em>l</em></span>,
the horizontal displacement <span
class="math inline"><em>l</em>sin <em>ζ</em></span>.</figcaption>
</figure>

Satellite Based Augmentation Systems (SBAS), e.g. the European EGNOS
system, designed to enable GPS-based aircraft precision approaches, rely
on the same principles as PPP. However, given the primary application,
the focus is on integrity rather than accuracy (integrity refers to the
trust that can be placed in the resulting position solution, the
solution is largely fault-tolerant). Carrier phase measurements are only
here used to ‘smooth’ the pseudorange solution. SBAS is a pseudorange
code Differential GPS approach for large geographical areas (wide
areas). An additional advantage of using SBAS is that the corrections
are transmitted on the same radio frequency as GPS signals, so no
additional data link is necessary.

## Processing strategies, dynamic model and observation period

As already hinted at, the GPS position accuracy improves when the
measurement time duration increases. One important factor here is the
*dynamic model* of the receiver motion, or how the measurement epochs
can be ‘linked’ to each other.

<figure id="fig:gpsaccuracy" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>Accuracy of various GPS positioning modes for a static
receiver. The integration time is the total measurement duration, along
the horizontal axis, and the position coordinates accuracy is along the
vertical axis. Note the logarithmic scales. CP&amp;RTK stands for
Carrier Phase and Real-Time Kinematic positioning.</figcaption>
</figure>

If the receiver is stationary, the improvement will be most notable, as
we can basically estimate a single position from many measurements (a
*static* solution). The position accuracy of a static receiver is shown
as a function of the measurement duration in
Figure <a href="#fig:gpsaccuracy" data-reference-type="ref"
data-reference="fig:gpsaccuracy">21</a> for each of the previously
covered GPS processing strategies.

For a moving receiver the accuracy can also improve over time, if we can
exploit the fact that some of the other parameters are constants,
e.g. the ambiguities, or, if the movement can be constrained or
predicted to some extent based on the current position (e.g. a car
driving along a straight line, at constant velocity). This can be
implemented with a Kalman filter, or a recursive least-squares data
processing algorithm.

In a *kinematic* solution, position coordinates are computed for each
measurement instant (for instance every 1 second), to accomodate the
fact that the receiver is/was actually moving during the survey. As a
result one then obtains a *list* of position estimates, e.g. one every
second, instead of one overall position solution as with a static
survey. The list describes the *track* or *trajectory* of the moving
receiver.

Two related issues are:

1.  The difference between *real-time* processing, and *post-processing*
    (for instance after whole survey has been completed), where
    post-processed results are generally more accurate, but obviously
    not available right on the spot, and hence not suitable for certain
    applications.

2.  The measurement rate of the receiver: GPS receivers often take
    pseudorange code, carrier phase, Doppler shift and signal-to-noise
    (SNR) measurements once every second, hence at 1 Hz, but depending
    on the application, 10-20 Hz is also common practice today, and
    technically up to a 100 Hz measurement rate is possible. To reduce
    the computational burden, data storage, and power requirement, lower
    measurement rates (e.g. once per 30 seconds) are common in
    applications where objects move only very slowly, like in geoscience
    on measuring tectonic plate motion. The impact of the measurement
    rate on the position accuracy is marginal (a higher data rate can
    slightly improve precision), because the measurement errors are
    generally correlated in time. This means that measurements taken in
    quick succession are not independent, and thereby do not offer,
    precision-wise, a lot of new/additional information.

# GNSS and applications

In this section we present a concise overview of Global Navigation
Satellite Systems (GNSS), addressing GPS, Glonass, Galileo and BeiDou.
Then we briefly touch upon the wide range of applications of GNSS.

## Global Navigation Satellite Systems (GNSS)

The Global Positioning System (GPS), developed by the US military and
operated by the US Air Force (USAF), is the first Global Navigation
Satellite System of its kind. In order not to be dependent on a US
military system and/or to get their share of the GNSS market, other
countries have developed their own Global Navigation Satellite Systems
(GNSS). The result is that today a lot of GNSS satellites can be seen at
the same time, anywhere on Earth, anytime.
Figure <a href="#fig:skyplot" data-reference-type="ref"
data-reference="fig:skyplot">22</a> shows as an example a so-called
skyplot for Delft, with up to 40 GNSS-satellites in view.

Recently we have seen a significant increase in the available Global
Navigation Satellite Systems, satellites, radio-frequencies and signals.
These developments are briefly reviewed in this section.

### GPS

GPS is in the process of modernization. This is achieved by following up
older satellites by new satellites with expanded and improved
capabilities. The civil L2C signal, for improved dual frequency
(civilian) performance, becomes available on more and more satellites.
Even more importantly, new GPS satellites also transmit an additional
(wideband) signal on the L5-frequency (of 1176.45 MHz) primarily
designed for safety-of-life applications (higher chiprate, hence shorter
chiplength, and more precise pseudorange measurements).

### Glonass

The Russian GLObal NAvigation Satellite System (GLONASS), has been fully
replenished and at present has 24 active satellites. Planned
modernizations of GLONASS include an additional signal transmitted on
the L5-frequency, and a switch from Frequency Division Multiple Access
(FDMA) to CDMA, which will increase interoperability with other GNSSes.

### Galileo

Galileo, the European GNSS, is still under development, currently with
22 satellites. The full Galileo constellation for Full Operational
Capability will consist of 30 satellites. The Galileo system transmits
navigation signals on four different carrier frequencies: L1/E1, L5/E5a,
E5b and E6, two of which (E5a and E5b) can also be tracked together as
one extra wideband (AltBOC) signal with unprecedented pseudorange
accuracy.

### BeiDou

The Chinese BeiDou Navigation Satellite System (BDS), sometimes still
known as Compass, was designed to provide independent regional
navigation in the first stage and global coverage later. The BeiDou
(phase III) constellation deployment has been fully completed in 2020,
with 30 satellites in orbit, providing global coverage.

### Concluding remarks

<figure id="fig:skyplot" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>Skyplot with GNSS satellites for October 8th, 2020, at 12:10
UTC, in Delft. The skyplot shows the positions of the satellites of the
various constellations, like GPS, GLONASS, Galileo and BeiDou, in the
sky. The outer circle represents the local horizon in Delft, 360 degrees
around (0 is North, 90 East, etc). The smaller circles refer to 30
degrees of elevation, above the horizon, and 60 degrees of elevation.
The middle of the skyplot corresponds to the so-called local zenith,
which is directly overhead. The skyplot was obtained from the Trimble
NetR9 GNSS receiver at the TU Delft observatory, of which the antenna
set-up is shown at right.</figcaption>
</figure>

The realized and expected upgrades of and additions to the available
GNSS signals can have a range of improvements on many GNSS applications.
Some of the more important ones are: the higher pseudorange accuracy of
the new signals, the availability of many more satellites at once (more
satellites available to combat urban environments, see
Figure <a href="#fig:skyplot" data-reference-type="ref"
data-reference="fig:skyplot">22</a>), and both the availability of more
radio-frequencies and satellites.

Multi-GNSS positioning also brings new challenges, as so-called
InterSystem Biases (ISB) are introduced in the model. The system time as
maintained by GPS may (will) not be the same as the system time as
maintained for Galileo, for instance. Hence one has to account for the
fact that these systems may have an offset in time with respect to each
other. To use multiple systems simultaneously in an optimal manner,
these biases must be studied, and if possible corrected or eliminated.

## Applications

There are many different applications of GNSS positioning each with its
own requirements and, related to that, a preferred processing strategy.

<figure id="fig:trafficandtransport" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>Car navigation, route guidance and fleet management in
traffic and transport are popular applications of GNSS positioning,
where standard positioning service suffices. In future, assisted and
automated driving will call for improved accuracy.</figcaption>
</figure>

- smartphones, car navigation, and personal navigation usually have the
  lowest requirements, and the GPS (GNSS) standard positioning service
  suffices,
  cf. Figure <a href="#fig:trafficandtransport" data-reference-type="ref"
  data-reference="fig:trafficandtransport">23</a>.

- lane specific navigation advice for road users requires sub-meter
  position accuracy, which can be fulfilled with single frequency PPP.

- surveying for creating maps and construction works, requires cm to mm
  position accuracy and will use RTK if available, or PPP otherwise,
  cf. Figures <a href="#fig:waterscooter" data-reference-type="ref"
  data-reference="fig:waterscooter">24</a> and
  <a href="#fig:talud" data-reference-type="ref"
  data-reference="fig:talud">18</a>.

- deformation monitoring, due to Earthquakes, volcanic activity, mining
  or extraction of petroleum or natural gas, as well as any number of
  scientific applications require the highest possible accuracy and use
  carrier phase based positioning.

- aircraft precision approach and landing requires high integrity
  positioning, and can use SBAS to obtain this.

- machine guidance, as shown in
  Figure <a href="#fig:excavator" data-reference-type="ref"
  data-reference="fig:excavator">15</a> and in particular self-driving
  vehicles require high accuracy and integrity; this can be achieved by
  using RTK-GNSS though this is still subject of research, and likely
  fusion with additional sensors is in order.

<figure id="fig:waterscooter" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>Both the on- and offshore part are regularly surveyed, to
monitor the development of the Zandmotor (The Sand Engine), at the Dutch
North-Sea coast, near Ter Heijde. This ‘building with nature’ project
started in 2011, and at right an aerial photo of the Zandmotor is shown,
looking in Southern direction. High-precision RTK-GPS is used for
positioning the quad on shore, and the jet-ski in the water (note the
GPS-antenna at the back of the jet-ski, in the inset). The measurements
by the quad result in a Digital Terrain Model (DTM), and echo sounder
depth measurements by the jet-ski result in a seafloor-map. Photo at
left by Matthieu de Schipper <span class="citation"
data-cites="deSchipper"></span>. Photo at right by Pmblom - own work,
May 2016, taken from <a
href="https://commons.wikimedia.org/wiki/File:Zandmotor_luchtfoto_(airplane_cropped).jpg">Wikimedia
Commons</a> <span class="citation" data-cites="wikicommons"></span>
under CC BY-SA 4.0 license.</figcaption>
</figure>

<figure id="fig:KPNtelecommast" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>A GPS receiver is commonly used to synchronize base stations
for telecommunication. Requirements on time-synchronization for this
application lie in the order of a <span
class="math inline"><em>μ</em></span>s. The photo shows a base station
with a height of 37 m, providing the full range of mobile services from
2G (GSM) to 5G (NR).</figcaption>
</figure>

There is also a number of GNSS applications, in which the position
solution is not the (primary) goal. Accurate time which is obtained
through determining also the receiver clock offset *b*<sub>*r*</sub>, is
used in timing applications. The standard positioning service allows for
timing at the 10-100 ns level, and this is used for instance in
telecommunication,
cf. Figure <a href="#fig:KPNtelecommast" data-reference-type="ref"
data-reference="fig:KPNtelecommast">25</a>, electrical power grids, and
financial networks.

Nuisance parameters such as the atmospheric delays can also be used as
observational input e.g. to determine, together with using models, the
state of the Earth’s ionosphere, or derive troposphere delays, for
instance for Numerical Weather Prediction (NWP).

GNSS radio-signals can also be used outside of their intended purpose,
e.g. to determine sea-level height by measuring reflected GNSS signals
from orbit.

## Resources

This part provides an introduction to positioning with GPS/GNSS. For a
lot more of technical and mathematical modeling information on GPS and
GNSS positioning, navigation and timing, the reader is referred to and .
These textbooks also cover a wide range of applications.

The first source of information on GPS, as well as the point of contact
is the [Navigation Center of the US Coast
Guard](http://www.navcen.uscg.gov/) . Official U.S. government
information about GPS is available through
[GPS.gov](https://www.gps.gov/) .

The first source of information on Galileo and point of contact is the
European Union Agency for the Space Programme
([EUSPA](https://www.euspa.europa.eu/)) .

The [IGS](https://igs.org/) is the International GNSS Service, a
voluntary federation of universities and research institutions,
operating permanent GNSS stations worldwide, and providing GNSS data and
products for high(est)-precision applications .

## Exercises and worked examples

This section presents a couple of questions and problems with (worked)
answers on GPS-positioning.

**Question 1** What are the largest remaining error sources in
short-baseline DGPS, explain your answer.

**Answer 1** The atmosphere delays as well as the satellite orbit and
clock errors are eliminated in DGPS,
cf. Figure <a href="#fig:dgps" data-reference-type="ref"
data-reference="fig:dgps">13</a>, which leaves multipath and
(pseudorange) measurement noise as the largest error sources,
cf. Figure <a href="#fig:signalpath" data-reference-type="ref"
data-reference="fig:signalpath">10</a> and
Table <a href="#tab:errorbudget" data-reference-type="ref"
data-reference="tab:errorbudget">1</a>.

**Question 2** If a certain application requires decimeter positioning
accuracy, which GPS positioning modes can be considered? And for how
long a time would we need to collect measurements?

**Answer 2** Real-Time Kinematic (RTK) provides decimeter or even
centimeter accuracy as soon as the ambiguities can be fixed, which
generally is (well) within 100 seconds of measurements, and even faster
in post-processing. PPP can also provide decimeter accuracy after
several minutes. DGPS can reach decimeter accuracy as well, but may
considerable time to allow for averaging (with static positioning only),
for instance one hour. SBAS and standalone GPS often do not reach
decimeter accuracy even after one or several days (averaging with static
positioning), especially in the vertical component. An overview of the
attainable accuracies can be found in
Figure <a href="#fig:gpsaccuracy" data-reference-type="ref"
data-reference="fig:gpsaccuracy">21</a>.

**Question 3** The principle of GPS satellite positioning and navigation
consists of determining the range from satellite to receiver through
measurement of the signal travel-time. The atomic clock in the satellite
is perfectly on time. When the receiver clock is ahead of time by
0.1 *μ*s, by how much is the measured range to the satellite too long or
too short?

**Answer 3** From
Eq. (<a href="#eq:clockerror" data-reference-type="ref"
data-reference="eq:clockerror">[eq:clockerror]</a>) we can see that
clock error *δ**t*<sub>*r*</sub> is positive, as the receiver clock is
ahead of time, hence *t*<sub>*r*</sub> \> *t*. Next, with
Eq. (<a href="#eq:pseudorange" data-reference-type="ref"
data-reference="eq:pseudorange">[eq:pseudorange]</a>), and
*c**δ**t*<sub>*r*</sub> = *b*<sub>*r*</sub> = 30 m, we find that the
pseudorange *p*<sub>*r*</sub><sup>*s*</sup> is too long by 30 m
(compared to the actual distance *l*<sub>*r*</sub><sup>*s*</sup>).

<figure id="fig:1D_GPSpositioning" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>One-dimensional GPS positioning (Question 4).</figcaption>
</figure>

**Question 4** The GPS positioning problem has been simplified to a
single dimension. There are two satellites A and B, and the user
receiver is at R, see
Figure <a href="#fig:1D_GPSpositioning" data-reference-type="ref"
data-reference="fig:1D_GPSpositioning">26</a>. The positions of the
satellites are known, A is at *x*<sub>*A*</sub> = 0, and B is at
*x*<sub>*B*</sub> = 10. The position of the user *x*<sub>*R*</sub> is
unknown. Two pseudoranges have been measured: *p*<sub>*A**R*</sub> = 9
and *p*<sub>*B**R*</sub> = 7. Determine the position (coordinate) of the
user at R.

**Answer 4** Looking at
Figure <a href="#fig:1D_GPSpositioning" data-reference-type="ref"
data-reference="fig:1D_GPSpositioning">26</a> we identify two geometric
ranges, namely
*l*<sub>*A**R*</sub> = *x*<sub>*R*</sub> − *x*<sub>*A*</sub> and
*l*<sub>*B**R*</sub> = *x*<sub>*B*</sub> − *x*<sub>*R*</sub> (mind to
define these distances to be positive). Then, with
Eq. (<a href="#eq:pseudorange" data-reference-type="ref"
data-reference="eq:pseudorange">[eq:pseudorange]</a>), we formulate two
observation equations:
$$\begin{array}{lll} p\_{AR} & = & l\_{AR} + b_R \\
                   p\_{BR} & = & l\_{BR} + b_R    \end{array}$$
which gives
$$\begin{array}{lll} p\_{AR} & = & x_R - x_A + b_R \\
                   p\_{BR} & = & x_B - x_R + b_R    \end{array}$$
and with the given satellite positions, we obtain
$$\begin{array}{lll} p\_{AR} + x_A & = & x_R + b_R \\
                   p\_{BR} - x_B & = & - x_R + b_R    \end{array}$$
We have two equations with two unknown parameters, namely
*x*<sub>*R*</sub> and *b*<sub>*R*</sub>, which we can solve, giving
*x*<sub>*R*</sub> = 6 and *b*<sub>*R*</sub> = 3. The user position
coordinate equals *x*<sub>*R*</sub> = 6, and we are typically not
interested in the receiver clock offset. It is easily verified that
correcting the measured pseudoranges for the receiver clock offset yield
the actual distances from the two satellites to the receiver:
*p*<sub>*A**R*</sub> − *b*<sub>*R*</sub> = 9 − 3 = 6 and
*p*<sub>*B**R*</sub> − *b*<sub>*R*</sub> = 7 − 3 = 4.

**Question 5** The GPS relative positioning problem has been simplified
to a single dimension. There is one satellite ‘sat’ (or just ‘s’) and it
is visible at the local horizon. The receivers ‘1’ and ‘2’, and the
satellite are all on a straight line (along the x-coordinate axis), see
Figure <a href="#fig:singledifference" data-reference-type="ref"
data-reference="fig:singledifference">27</a>. The radio-signals from the
satellite to the two receivers pass through the Earth’s atmosphere
(layer ‘atm’) and get thereby delayed; the delay, expressed in units of
range, is denoted by *d*<sup>*s*</sup>. This delay is unknown (but
*equal* for the signals to both receivers). The satellite position is
known, *x*<sup>*s*</sup> = −20, and the position of receiver 1 as well
*x*<sub>1</sub> = 5. Compute the position of receiver 2,
*x*<sub>2</sub>, based on the pseudorange measurements
*p*<sub>1</sub><sup>*s*</sup> = 32 and
*p*<sub>2</sub><sup>*s*</sup> = 37. In this case, you can again assume
that all clocks run perfectly on time – there are no clock offsets
involved.

<figure id="fig:singledifference" data-latex-placement="hbt">
<div class="center">

</div>
<figcaption>Relative positioning in one dimension
(Question 5).</figcaption>
</figure>

**Answer 5** The pseudorange observation equation
(<a href="#eq:pseudorange" data-reference-type="ref"
data-reference="eq:pseudorange">[eq:pseudorange]</a>) needs to be
adapted. There is no clock offset involved at all, so parameter
*b*<sub>*r*</sub> cancels, but now, we face an unknown atmospheric
delay *d*<sup>*s*</sup>. Hence
$$\begin{array}{lll} p\_{1}^{s} & = & l\_{1}^{s} + d^s \\
                   p\_{2}^{s} & = & l\_{2}^{s} + d^s    \end{array}$$
Looking at
Figure <a href="#fig:singledifference" data-reference-type="ref"
data-reference="fig:singledifference">27</a> we identify two geometric
ranges, namely
*l*<sub>1</sub><sup>*s*</sup> = *x*<sub>1</sub> − *x*<sup>*s*</sup> and
*l*<sub>2</sub><sup>*s*</sup> = *x*<sub>2</sub> − *x*<sup>*s*</sup>
(mind to define these distances to be positive). Then the two
observation equations become:
$$\begin{array}{lll} p\_{1}^{s} & = & x_1 - x^s + d^s \\
                   p\_{2}^{s} & = & x_2 - x^s + d^s    \end{array}$$
where there are two unknown parameters, namely *x*<sub>2</sub> and
*d*<sup>*s*</sup>. With the given measurements and coordinates, this is
easily solved, to yield *x*<sub>2</sub> = 10 and *d*<sup>*s*</sup> = 7.
Alternatively one could take the difference of the two pseudorange
measurements
*p*<sub>2</sub><sup>*s*</sup> − *p*<sub>1</sub><sup>*s*</sup> = *x*<sub>2</sub> − *x*<sub>1</sub>,
which gives an identical result for *x*<sub>2</sub>, and one is
generally not interested in parameter *d*<sup>*s*</sup>.

[^1]: When, in this example, the receiver clock would behave perfectly
    and be exactly aligned with GPS-time, we could solve the
    two-dimensional positioning problem by measuring just two
    pseudoranges, which then directly give us two proper distances,
    though two circles may intersect at two points actually. With GPS
    this would be no problem, as the satellites are at 20.000 km
    distance, and the other intersection point will generally be on the
    other side of the Earth, or even way beyond.

[^2]: Radio Technical Commission for Maritime Services - Special
    Committee 104 on Differential GNSS
