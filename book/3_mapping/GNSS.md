# GNSS Positioning

Except for the Introduction, this chapter is reproduced in its entirety from Tiberius et al. (2022) (this book is published under a CC BY-NC-SA license). Explicit references to other chapters and sections of this book have been added. The Introduction is adapted from Chapter 12 of Tiberius et al. (2022), with minor reorganization of the material and the omission of one subsection.

## Introduction

The Global Positioning System (GPS), also known as the NAVigation Satellite Time And Ranging (NAVSTAR) system,
is one the most successful satellite systems to date. 
Its success is strongly linked to the ever-decreasing costs of GPS receivers, which primarily consist of electronic hardware.
While high-end receivers still cost in the order of \$ 1-10k,
mass-market receivers, such as those used in smartphones, cost no more than a few dollars each.
Currently there are about as many GPS devices on Earth as people, nearly 7 billion, the vast majority of which are in smartphones.
The global Global Navigation Satellite System (GNSS) downstream market revenues, from both devices and services, were in 2020 around 150 billion Euro,
according to the market report by the European GNSS Agency (GSA), now the European Union Agency for the Space Programme (EUSPA) (European GNSS Agency, 2019).

The first GPS satellite was launched back in February 1978.
GPS is a *one-way* radio ranging system which provides real-time knowledge of one's Position and Velocity,
and a very accurate Time reference as well (all together referred to as PVT).

GPS provides Positioning, Navigation and Timing (PNT) functionality, which is very valuable not only for the US military,
for which it was first developed, but also to a myriad of commercial activities, as well as the general public at large.

The GPS system consists of three segments.
1. The space segment, consisting of 24 or more satellites, with accurate atomic clocks on board, continuously transmitting ranging signals
      to Earth.
2. The control segment, consisting of a number of ground stations, which monitors the satellites, computes their orbits and clock offsets,
      and uploads this information to the satellites, which in turn encode this information on the ranging signal (the so-called navigation data).
3. The user segment, simply consisting of many GPS receivers, which each track four or more GPS satellites, and compute their own position.

This chapter provides an introduction to GPS positioning. 
Section~{ref}`chap:ranging` presents the basic concepts of the measurement of travel-time of a radio signal from a GPS satellite to a receiver.
With these measurements of range as input, Section~{ref}`chap:GPSpositioning` describes the default mode of GPS positioning, referred to as stand-alone or single-point positioning.
The next section introduces the concept of relative positioning, by means of which high-accuracy, centimeter-level positioning is made possible.
Section~{ref}`chap:GNSSapplications` presents, after a brief overview of the four major Global Navigation Satellite Systems (GNSS),
an overview of the wide range of applications of GPS/GNSS in today's society.
There is much more more of information available on this subject, and
the reader is therefore referred to, for instance, the textbooks Teunissen and Montenbruck [2017] and Morton et al. [2021].

````{figure} ../figures/GNSS/GPSsatelliteblockIIF.jpg
---
name: GPSblockIIF
width: 60%
align: center
---
GPS block IIF satellite, built by Boeing. These GPS satellites, 12 in total, have been launched between 2010 and 2016. They have a design lifetime of 12 years. The full GPS constellation nominally consists of 24 satellites. Image courtesy of Boeing.
````

## Ranging

### Radio signal

The GPS satellites transmit signals in the so-called L-band (i.e. 1 to 2 GHz range) of the electromagnetic radio frequency
spectrum. GPS uses Code Division Multiple Access (CDMA) to allow different satellites to send
signals at exactly the same center frequency without interfering with each other. The signal consists
of a carrier wave on which each satellite modulates its own unique Pseudo Random Noise (PRN)
spreading code, see Figure~{ref}`fig:gpssignal`, and, at a low rate, the satellite orbit and clock information. The signals
arrive at the receiver with an unknown *delay* due to travelling all the way from satellite to receiver, and due to the relative velocity
of the GPS satellites with respect to a GPS user on or near the Earth's surface, with an unknown *Doppler frequency shift*.

````{figure} ../figures/GNSS/GPSsignal.png
---
name: gpssignal
width: 60%
align: center
---
The GPS L1 CA-signal is composed of a carrier wave (a sinusoid with a frequency of 1575.42~MHz; not to scale in the above diagram), a spreading code (a sequence of `0' and `1' bits/chips, here represented by values `-1' and `+1', and unique for each satellite), and a low rate navigation data message. Both the spreading code and navigation message are phase-modulated on the carrier wave, through a technique called Binary Phase Shift Keying (BPSK); basically multiplying the carrier by the `-1' and `+1' values of the spreading code and navigation data, and the resulting modulated signal is shown at bottom. For the so-called CA-code on the GPS L1-frequency signal, the spreading codes are all publicly available, and GPS receivers have them built in. CA refers to Coarse Acquisition, but can also be understood as Civilian Access.
````

### Measurement of range

GPS offers two types of range measurements: pseudorange measurements and carrier phase measurements.

#### Pseudorange measurement

A GPS receiver typically consists of tens to hundreds of so-called channels, and will allocate each of these to a
specific GPS (GNSS) satellite. When a GPS receiver first starts up, it will begin to search for a particular
GPS satellite on each of its channels, by scanning (trying) for the corresponding spreading codes at different Doppler offsets and time delays.
This is done by overlaying the received signal with a local copy or replica of the same code and then (time) shifting it until correlation shows a maximum
(best fit, or match). The time shift then directly yields the travel-time measurement.

Once the receiver has locked onto the *spreading code*, it can start regularly taking pseudorange code and Doppler frequency measurements,
which are basically the shift in time (delay) and the shift in frequency that are required to maintain the tracking lock (onto the received satellite signal).

Through the pseudorange, the receiver measures the *travel-time* of the radio signal from satellite `s' to receiver `r':

$$
\begin{equation}
\tau_{r}^{s} = t_r - t^s
\end{equation}
$$

where $t^s$ is the time the signal was transmitted by the satellite, and $t_r$ the time the signal was received at the receiver,
later noting that these clocks may, to some extent, deviate from the true time. The measured travel-time is converted into the
pseudorange, expressed in unit meter, through

$$
\begin{equation}
p_{r}^{s} = c \tau_{r}^{s}
\end{equation}
$$

by multiplying by the speed of light $c$ in vacuum ($c \approx 3 \cdot 10^8$~m/s).

The pseudorange represents the travel-time of the signal, and thereby ideally the distance from satellite to receiver. In practice it is affected
by the satellite clock offset (known to the receiver through the navigation message), the receiver clock offset, which is unknown,
and a number of additional delays, which we cover in the sequel (Figure~{ref}`fig:signalpath`), and all multiplied by the speed of light.
The clock error is addressed in Section~21.2.1 in Tiberius et al. (2022). 
In particular the oscillator in the receiver, driving the clock, will not behave perfectly, and hence the receiver clock may run ahead of time, or lag behind.
The time shown by the receiver clock is denoted by $t_r(t)$, and it is a function of true time $t$. It equals true time~$t$, plus a so-called clock offset
$\delta t_{r}(t)$, hence

$$
\begin{equation}
t_{r}(t) = t + \delta t_{r}(t)
\end{equation}
$$

When the receiver measures the travel-time, to eventually produce the pseudorange measurement, it `reads' the moment of signal arrival at its own clock,
and hence this measurement is off by an amount of $\delta t_{r}(t)$. The travel-time can be conceived as being obtained by `reading' the receiver clock at 
signal reception, and `reading' the satellite clock at signal transmission, hence the *measured* travel-time reads

$$
\begin{equation}
\tau_{r}^{s}(t) = t_{r}(t) - t^{s}(t-\tau(t))
\end{equation}
$$

Mind that the (true) travel-time $\tau(t)$ is a function of time, as the receiver may move, and the satellite for sure moves.
Substituting here the expression for $t_{r}(t)$, assuming that the satellite clock is perfectly on time, hence $t^{s}(t-\tau(t))=t-\tau(t)$
(the satellites carry atomic clocks), and multiplying by the speed of light now gives:

$$
\begin{equation}
p_{r}^{s}(t) = c \tau_{r}^{s}(t) = \underbrace{c \tau(t)}_{l_{r}^{s}(t)} + \underbrace{c \delta t_{r}(t)}_{b_{r}(t)}
\end{equation}
$$

where, in the absence of for instance atmospheric delays, $l_{r}^{s}$ denotes the geometric distance between satellite and receiver.
This equation shows that the *pseudorange* is a measure for the geometric distance $l_{r}^{s}$, apart from the receiver clock offset~$b_r$, and hence
the term *pseudo*-range.

#### Carrier phase measurement

Additionally, a GPS receiver may measure the *fractional* phase difference between the received carrier wave from the satellite
and a locally generated copy (replica). And, it can keep track of the number of cycles of the carrier wave since the start of tracking,
together known as the *carrier phase* (CP) measurement. This measurement includes the accumulated number of `zero-crossings' since
lock-on of the signal (for instance, when the fractional phase jumps from $1.99 \pi$ to $0.02 \pi$, the full period is accounted for
and the resulting carrier phase measurement, output by the receiver, is $2.02 \pi$).

The carrier wave measurement is a very precise measure of the distance between the satellite and the receiver, but the initial number of 
carrier wave cycles is unknown, and needs to be estimated before the carrier phase measurements can be effectively used, see Figure~{ref}`fig:ambiguity`.
The much better precision of the carrier phase measurement with respect to the pseudorange code measurement can be understood from
Figure~{ref}`fig:gpssignal`, since the carrier period is much smaller than the code chip duration (for the L1 CA-code signal, 1540 periods
of the carrier fit in one chip of the Pseudo Random Noise (PRN) spreading code).

````{figure} ../figures/GNSS/ambiguity.png
---
name: ambiguity
width: 60%
align: center
---
Carrier phase measurement: only the *fractional* phase difference can be measured, shown in red in units of length [m] (with $\Phi \in [0,2\pi \rangle$ when expressed in radians; $\varphi = \lambda \frac{\Phi
````

#### Concluding remarks

Linking to the exposition on measuring distances in Chapter~20 in Tiberius et al. (2022) , the pseudorange measurement corresponds to
`pulse-based'-ranging, and the carrier phase measurement obviously to `phase-based'-ranging, see Section~20.1 in Tiberius et al. (2022) on the principles of ranging,
though one should note that GPS is about *one-way* ranging (rather than two-way ranging, as in Chapter~20 in Tiberius et al. (2022) ).

The receiver can also measure the received *signal-strength*, through the so-called carrier-to-noise-density ratio C/N0,
which gives an indication of the quality of the measurement (larger signal-strength yields more precise measurement).

And some receivers output also the measurement of the *Doppler frequency* of the carrier wave, which is a measure for the (relative) velocity of the receiver
with respect to the satellite (along the line of sight), see also Section~20.2 in Tiberius et al. (2022). The Doppler frequency, multiplied by the wavelength,
presents the range-rate $\dot{l}_{r}^{s}$, that is, the change in range $l_{r}^{s}(t)$ per unit time.

The measurements can be stored, e.g.\ for the purpose of later analysis and processing,
in receiver manufacturer proprietary format or in a generally accepted exchange format,
namely RINEX, see Appendix~F in Tiberius et al. (2022).

The pseudorange measurement precision is typically at the one or few meter level for low-cost, mass-market equipment, and can get down
to the few decimeter level for professional high-end equipment.

The carrier phase measurement precision ranges from the few centimeter to the millimeter level. The carrier phase is an ambiguous
measurement of distance, but it is more precise than the pseudorange, typically by two orders of magnitude.

````{figure} ../figures/GNSS/graphC1.png
---
name: graphsC1L1D1
width: 60%
align: center
---
Example of time series of (at left) C1 pseudorange measurements, in meter, (in the middle) L1 carrier phase measurements, in cycles, and  (at right) D1 Doppler frequency measurements, in Hertz, of a stationary, permanent receiver in Delft, cf.\ Figure~{ref}`fig:skyplot
````

Figure~\ref{fig:graphsC1L1D1` shows measurements, collected by a stationary receiver in Delft, on signals received from GPS satellite PRN20, as a function of time.
A pass-over of a GPS satellite typically takes several, up to 7 hours. With a nearly circular orbit of the GPS satellite around the Earth,
the distance from satellite to receiver is shortest when the satellite is directly overhead.
By default actually the negative of the Doppler frequency is output by the GPS receiver (as shown in the graph at right, the measured Doppler frequency is positive (in the interval from about 7-10 hours),
while the distance at the same time, as shown in the graph at left, is decreasing).

### Multi-frequency ranging

One of the major error sources in GPS is due to the ionosphere, see also Figure~{ref}`fig:signalpath` and Table~{ref}`tab:errorbudget`. The ionosphere is a ionized part of the Earth's upper atmosphere.
There ultraviolet (UV) solar radiation separates electrons from neutral gas atoms and molecules. The free electrons in the ionosphere
delay the radio signals, and thus affect the range measurements, with delays in terms of distance ranging from a few meter to hundreds of meters.

The largest delays occur round the geomagnetic equator around local noon, and during solar maxima. The ionospheric delay
may be highly variable, as a function of both time and space.

One way of dealing with the ionospheric delay is to track signals from the same satellite on two or more frequencies. The ionosphere delay scales,
to a very good approximation, with the inverse of the square of the radio frequency of the signal, and this relation can be used to create the so-called
ionosphere-free range measurements (a linear combination of measurements at two different frequencies, from which the ionospheric delay has been
removed). For this reason the GPS satellites were originally designed to transmit ranging signals on both the L1 (1575.42~MHz) and L2 (1227.60~MHz) frequency.

## Positioning

GPS positioning is based on the concept of multi-lateration (not triangulation). By measuring distances to a number of GPS satellites,
as shown in Figure~{ref}`fig:GPSpositioning`, and using the known satellite positions, a GPS receiver can compute its own position.
To estimate the three position coordinates of the receiver $x_r$, $y_r$, $z_r$, and the receiver clock offset $b_r$, a
GPS receiver needs to track at least 4 satellites.

````{figure} ../figures/GNSS/GPSpositioning.png
---
name: GPSpositioning
width: 60%
align: center
---
GPS positioning --- in three dimensions --- is based on measuring pseudoranges to at least four satellites, of which the positions are known. Visualization by Axel Smits.
````

### Geometric interpretation

Knowing ones distance to an object (satellite) at a known position, translates into being on a circle (in 2D) or a sphere (in 3D) around this object
(with the satellite in the center).
As we have seen with ({ref}`eq:pseudorange`), the GPS pseudorange measurement relates to the geometric range (distance) from satellite to receiver,
but, also to an offset caused by the receiver clock! This means, the pseudorange gives us the distance from satellite to receiver, but it may or will
be too small, or too large by a certain amount, namely the receiver clock offset~$b$. The good news is that the receiver clock offset is the *same*
for all pseudoranges measured by the receiver at a specific time. If the receiver clock is ahead of GPS-time, all pseudoranges will be measured too long,
and by the same amount. This leads us to the approach of solving for three position coordinates and the receiver clock error at the same time,
and hence, requiring pseudorange measurements to at least four satellites (rather than three).

To see the effect of the receiver clock error on the positioning problem at work, we consider a simple two-dimensional positioning example (in which we assume that there is no effect of noise present in the pseudorange measurements).
So, in two dimensions, we would need to solve for two receiver position coordinates and one receiver clock error, hence in total three unknown parameters,
so we need at least three pseudorange measurements.

````{figure} ../figures/GNSS/trilateration_green.png
---
name: trilaterationgreenblue
width: 60%
align: center
---
Two-dimensional positioning example with three satellites (at known positions, represented by the black dots). The measured pseudoranges are visualized by circles, in green at left, and in blue at right.
````

````{figure} ../figures/GNSS/trilateration.png
---
name: trilateration
width: 60%
align: center
---
The process of determining the receiver clock offset: the measured pseudoranges have to be reduced or enlarged, but all with exactly the same amount, in order to meet at one physical position. The amount to make that happen is the receiver clock offset. The different colors represent different values for the receiver clock offset.
````

In Figure~{ref}`fig:trilaterationgreenblue` at left, the measured pseudoranges are shown in green, and apparently these three green circles do not all
meet in one point. The pseudoranges are `too short', the reason obviously being the receiver clock lagging behind. When the radii of the green circles
are enlarged, all by exactly the same amount, to yield the blue circles, as shown at right, we arrive at an intersection of all three circles in one point.
We have solved for the two position coordinates, and the receiver clock offset as well\footnote{
When, in this example, the receiver clock would behave perfectly and be exactly aligned with GPS-time, we could solve the two-dimensional
positioning problem by measuring just two pseudoranges, which then directly give us two proper distances, though two circles may intersect at two points
actually. With GPS this would be no problem, as the satellites are at 20.000 km distance, and the other intersection point will generally be on the other
side of the Earth, or even way beyond.
}.
This clearly demonstrates that positioning and timing are intimately related!

### Pseudorange observation equation

With expanding the one-way geometric range $l_{r}^{s}$ between satellite `s' and receiver `r' as

$$
\begin{equation}
l_{r}^{s} = \sqrt{(x^s-x_r)^2 + (y^s-y_r)^2 + (z^s-z_r)^2}
\end{equation}
$$

using a three-dimensional Cartesian coordinate system as shown in Figure~{ref}`fig:ECEF`,
pseudorange observation Eq.~({ref}`eq:pseudorange`) turns into

$$
\begin{equation}
\underline{p}_{r}^{s} = \sqrt{(x^s-x_r)^2 + (y^s-y_r)^2 + (z^s-z_r)^2} + b_r + \underline{e}_{r}^{s}

\end{equation}
$$

where we omitted the argument of time~$t$. The satellite position coordinates at time of signal transmission are
$x^s$, $y^s$ and $z^s$, and the receiver position coordinates at time of signal reception are $x_r$, $y_r$ and $z_r$.
The satellite position, as well as the satellite clock offset, is available to the user
through the navigation data message, cf.\ Figure~{ref}`fig:gpssignal`.
Parameter $b_r$ equals the receiver clock offset $\delta t_r$ multiplied by the speed of light~$c$, cf.\ ({ref}`eq:pseudorange`).
If the receiver clock is ahead of GPS system time, $b_r$ is positive, and the measured pseudoranges are `too long'.
And finally note that we included the (unavoidable) random measurement error $\underline{e}_{r}^{s}$ on the right hand side of Eq.~({ref}`eq:pseudorangeobseqn`).

````{figure} ../figures/GNSS/ECEF.png
---
name: ECEF
width: 60%
align: center
---
Three-dimensional Cartesian Earth-Centered Earth-Fixed (ECEF) coordinate system for GPS positioning.
````

### Positioning: parameter estimation

In practice, as one typically observes more satellites than the minimum of four, GPS positioning does not actually involve drawing circles or spheres,
but employs the principle of least squares estimation. First the observation model is defined, which links the observations to the unknown
parameters.

Since the GPS observation model is non-linear, this involves a linearisation with respect to the unknown parameters, around an approximate position,
see Tiberius et al., (2022). The linearized model of observation equations reads

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

where we assume to have $m$ satellites in view. Tiberius et al. (2022) presents the linearization of a
distance observation equation in two dimensions, and extension into three dimensions is straightforward.
The coefficients in the above design-matrix for the coordinate parameters are actually the elements of the unit-direction vector $u_{r}^{s}$
from the receiver `r', pointing to the satellite `s', cf.\ (Tiberius et al. 2022).
The above model carries $m$ observations and 4 unknown parameters, and hence the redundancy equals $m-4$.

Next, a least-squares algorithm is used to solve this linearized model, presented in matrix-vector form.
When an $m \times m$ variance matrix of the pseudorange observables is involved, a Best Linear Unbiased Estimation solution can be obtained,
which minimizes the uncertainty of the solution (see Chapter~8 in Tiberius et al. (2022).
Then one can also obtain the variance matrix of the parameter estimators, through (Equation~8.7 in Tiberius et al. (2022)), and analyse the precision of the position coordinates.

Most users of GPS are interested in position coordinates $x_r$, $y_r$, and $z_r$. Through knowledge
of the receiver clock offset $b_r = c \delta t_r$ one has in fact access to GPS system time,
which is an atomic time scale, and thereby also to UTC (Coordinated Universal Time).

Similar to the position coordinates estimation based on pseudorange measurements, the three-dimensional velocity vector of the
receiver can be estimated from the measured Doppler shift measurements, cf.\ Section~{ref}`sec:concludingremarkobs`.

A well-known and widely used format for storing and exchanging GPS (GNSS) Position, Velocity and Time (PVT)
solutions is NMEA, see Appendix E in Tiberius et al. (2022).

### Reference systems

Relying, by default, on the given satellite positions in the navigation message of the GPS signal, GPS positioning yields Cartesian coordinates
$(x,y,z)$ in WGS84, the World Geodetic System 1984, which is an Earth-Fixed, Earth-Centered (ECEF) coordinate system, as presented in Figure~{ref}`fig:ECEF`.
These Cartesian coordinates can be converted into geographic, or ellipsoidal coordinates latitude $\varphi$, longitude $\lambda$,
and ellipsoidal height $h$, see Chapter~X.

In differential mode (introduced in the next section), the position coordinates for the user receiver are in the same reference system
as the position coordinates of the base, or reference station, generally provided in a local or regional reference system (e.g.\
ETRS89 in Europe, a realization of the European Terrestrial Reference System).

### GPS accuracy and error sources

The quality of the GPS position solution is largely dependent on the number of available satellites
and their geometry with respect to the user. If enough satellites are visible on all sides of the
receiver, at high and low elevation angles, a good position accuracy can be expected.
The only weakness in the geometry is the fact that there are no satellites visible beneath the receiver, as one cannot track and observe satellites
below the local horizon. As a result vertical position accuracy is generally poorer than the horizontal accuracy by about a factor of 1.5.

In many practical situations one or more satellite signals are *blocked* by surrounding buildings or other obstacles which is called shadowing.
In this case GPS performance might be significantly degraded. Furthermore, in built-up areas, GPS receivers often experience signal reflections,
i.e.\ signals arrive at the receiver after bouncing off an object. Since the reflected signal path is always longer than the direct path,
this causes a corresponding error in the range measurement. It is also possible that both the direct and reflected signals arrive at the receiver,
which is referred to as *multipath*. In this case, the receiver must deal with the superposition of these signals, generally resulting in
a biased range measurement, see Figure~{ref}`fig:multipath`.

Carefully selecting the location for a survey can help to keep the impact of multipath at a minimum, as well as the use of a good antenna.

````{figure} ../figures/GNSS/multipath.png
---
name: multipath
width: 60%
align: center
---
Multipath: the direct line of sight signal from the satellite is received, though as well as a signal which has been reflected by the building. The reception of also a reflected signal, which has made a detour, will generally cause a bias in the measurement.
````

````{figure} ../figures/GNSS/errorsources.png
---
name: signalpath
width: 60%
align: center
---
GPS error sources. The receiver clock offset (shown in faded green) is accounted for in the observation equation ({ref}`eq:pseudorangeobseqn
````

\begin{table`
\begin{center}
\begin{tabular}{|l|c|}
\hline
       error source & 95\%-value 
\hline
       satellite orbit   &   2 m 
satellite clock   &  2-5 m 
ionosphere        &  15-90 m 
troposphere       &   20 m 
multipath         &  1-10 m 
receiver noise    &  1-3 m 
\hline
       total range  &  5-10 m 
\hline
\end{tabular}
\end{center}
\caption{GPS error budget for standalone positioning, see also Figure~{ref}`fig:signalpath`. The errors are given in the range domain, using the satellite (broadcast) navigation data message, and after Klobuchar ionospheric model
correction (which in practice yields a 50\% reduction of the ionospheric delay error), as well as tropospheric delay correction based
on an a-priori (blind) model (which yields about 90\% of reduction of the tropospheric delay error). The larger values for ionospheric and
tropospheric delay may occur for slant ranges to satellites at low elevation.}

\end{table}

The accuracy of *standalone positioning* with GPS, also referred to as single-point positioning, or absolute positioning, according to model ({ref}`eq:standalonemodel`),
in the order of 5-15 meters under reasonable satellite visibility, is limited by the accuracy of the range measurements
(time can be determined correspondingly with a tens of nanoseconds accuracy).
The GPS pseudorange measurements contain errors due to inaccurate satellite orbit and clock information,
delays along the path of the radio signal, including atmospheric delays (ionosphere and troposphere), local effects including multipath,
and measurement noise, see Figure~{ref}`fig:signalpath` and Table~{ref}`tab:errorbudget`.

Finally it is mentioned that a GPS receiver, using electromagnetic signals received from the satellites,
determines the position of the antenna phase center (typically a point inside or slightly above the antenna)
as this is where the radio signals actually arrive.
Handling the so-called antenna Phase Center Offset (PCO) with respect to the bottom of the antenna, usually a cm to dm-effect,
is important in high-precision positioning discussed in the next section.

````{figure} ../figures/GNSS/CTB3310surveymarker.jpg
---
name: CTB3310surveymarker
width: 60%
align: center
---
Survey-marker at TU Delft campus with accurate ground-truth coordinates: $X$ = 3923768.0147~m, $Y$ = 300255.7048~m, $Z$ = 5002640.2228~m (ITRF2014 at epoch 2021.50).
````

````{figure} ../figures/GNSS/spp_scatter.png
---
name: spppos
width: 60%
align: center
---
Example of GNSS standalone positioning for a duration of 5000 seconds at a 5 second interval, on September 2nd, 2021, with measurements to about 25 GNSS satellites. At left: scatter of horizontal position error, at right: time series of vertical position error.
````

### Standalone positioning: example

With the equipment of Figure~{ref}`fig:ublox` a short experiment was carried out, lasting 5000 seconds.
The antenna was installed on a survey-marker on the TU Delft campus, of which accurate position
coordinates were already available, see Figure~{ref}`fig:CTB3310surveymarker`.
The receiver ran in so-called standalone positioning or single-point positioning mode,
and every 5th position solution was saved, hence the results shown
in Figure~{ref}`fig:spppos` are obtained at a 5 second interval.

The graph at left shows the horizontal position scatter, North-coordinate versus East-coordinate,
and the graph at right shows the vertical position (Up) as a function of time.
With the given coordinates of the marker, we actually present the position *error* in Figure~{ref}`fig:spppos`,
i.e.\ the difference of the measured position coordinate and the known ground-truth position coordinate.
Hence, the origin of this graph refers to the `true' position.
The position errors are expressed in a local topocentric coordinate system, in terms of local
East, North and Up, see Section~29.4 in Tiberius et al. (2022).

Table~{ref}`tab:spppos` presents the resulting empirical mean, standard deviation (std) and the root mean square
(rms), which is the square root of the MSE, see Chapter~6 in Tiberius et al. (2022) ,
of the position error in East, North and Up, showing a better than 1 meter accuracy of GNSS standalone positioning
using over 25 GNSS satellites.

\begin{table}
\begin{center}
\begin{tabular}{|l|ccc|}
\hline
               & East & North & Up 
\hline
      mean [m] & 0.51 &  0.23 & -0.47 
std [m]  & 0.15 &  0.35 &   0.41 
rms [m]  & 0.53 & 0.42 & 0.62 
\hline
\end{tabular}
\end{center}
\caption{Empirical mean, standard deviation (std) and root mean square (rms) of position error,
based on $N$=1000 GNSS standalone position solutions.}

\end{table}

## GPS positioning modes

Several techniques have been developed to improve on the GPS Standard Positioning Service (SPS) accuracy (standalone positioning, as discussed in the previous section).
Firstly, GPS satellites broadcast a second, more precise, code on the same carrier wave, to provide the Precise Positioning Service (PPS).
However, this code is encrypted and can only be used to full extent by the US military.

Fortunately, even more accurate positioning modes are available, all relying on a kind of *augmentation*. This means that,
next to the measurements collected by the user receiver, in addition measurements are used of a nearby permanent GPS receiver,
and/or that one relies in addition on data products derived from a network of permanent tracking stations. Such a network could provide
precise estimates of the satellite positions for instance (more precise than what we by default encounter in the navigation message on the GPS signal).

### Relative positioning, or DGPS

Differential GPS (DGPS) uses a data link to a nearby base or reference station, i.e.\ another GPS receiver at an accurately known position,
and the *relative position* between the two is obtained. Measurement data from this base station are used, to reduce the effects of
the atmospheric delays, satellite clock offsets and orbit errors. This can be achieved by differencing the observations from both receivers
to the same satellites, which eliminates these (common) errors, which affect both receivers almost identically if the distance between them
is small enough, typically in the order of 5 to 10~km, considering that the satellites are at 20.000~km distance, see Figure~{ref}`fig:dgps`.

From the differenced observations, the so-called baseline (vector) between the two receivers can be computed through least-squares
estimation. The position of the rover is then obtained by adding the baseline vector to the accurately known coordinates
of the reference station. Generally the term `DGPS' is used for relative positioning, though using only pseudorange measurements.

````{figure} ../figures/GNSS/relativepositioning.png
---
name: dgps
width: 60%
align: center
---
Relative GPS positioning combines measurements from a roving receiver with measurements from a reference (or base) station. The position of the rover is actually computed *relative* to the position of the base station. A number of errors, including atmospheric errors, is almost identical for two receivers in close proximity to each other. Hence, these errors cancel in relative positioning.
````

#### Real-Time Kinematic (RTK)

To obtain the highest possible accuracy from GPS, it is no longer sufficient to use only the pseudorange code measurements, but
rather the *carrier phase* measurements, introduced in Section~{ref}`chap:ranging`, are required.
As mentioned before, the measurement of fractional phase difference does pose the problem of the unknown initial number of carrier wave cycles,
also called the carrier wave *ambiguity*, which need to be estimated together with the other unknown parameters.

An ambiguity consists of a fractional part at the satellite (equal for both receivers, and already
removed by the differencing between the base station and rover), a fractional part at the receiver
(equal for all tracked satellites), and an integer number of whole cycles. This fact of unknown parameters being integers (rather than reals) is exploited in a
technique called *Real-Time Kinematic (RTK)* positioning, or Carrier-Phase (CP) based baseline processing (if performed in
post processing), by selecting a reference satellite and forming a second difference between the
measurement to a reference satellite and those to all other satellites, to eliminate the fractional part at the
side of the receiver. In this special case the double-differenced carrier phase ambiguities can be
resolved to their integer number very efficiently through integer least-squares estimation. After only
a few minutes or within tens of seconds already, centimeter-level position accuracy can be reached.

````{figure} ../figures/GNSS/06GPSnetwork.png
---
name: 06GPSnetwork
width: 60%
align: center
---
Example of network of permanent GPS tracking stations, of a commercial network RTK service provider in the Netherlands, Belgium and Luxemburg. Image obtained with permission from [06-GPS](https://www.06-gps.nl) (06-GPS)
````

The requirement for a nearby reference receiver is a disadvantage of RTK, considering effort and/or cost.
With RTK the coverage area of a reference receiver or station typically has a radius of ten, or tens of kilometers.
In many regions and countries, networks of reference stations, or Continuously Operating Reference Stations (CORS) have been deployed
in order to cover the entire area, and in this scenario sometimes the term *network-RTK* is used, see Figure~{ref}`fig:06GPSnetwork`,
where reference stations generally have a 30-40 km interdistance.
An example of an application of RTK positioning in road construction is shown in Figure~{ref}`fig:excavator`.

````{figure} ../figures/GNSS/excavator.png
---
name: excavator
width: 60%
align: center
---
Excavator in the process of constructing a motorway embankment. RTK-GPS provides accurate real-time position information to guide this machine (note the two GPS-antennas on the back of the engine). Image courtesy of [Heijmans](https://www.heijmans.nl/).
````

Many high-end GPS receivers have RTK functionality built-in, but it can also be performed with professional software,
or even with open source software such as the RTKLIB program package (Takasu).

Today the measurements of the base station are communicated, in real-time, to the rover receiver over an Internet-connection,
using NTRIP.
Networked Transport of RTCM\footnote{
Radio Technical Commission for Maritime Services - Special Committee 104 on Differential GNSS

via Internet Protocol (NTRIP) is an application protocol
that supports the streaming of (differential) GNSS data over the Internet, based on Hyper Text Transfer Protocol (HTTP).
NTRIP has been developed by the German Federal Agency for Cartography and Geodesy (Bundesamt fur Kartographie und Geodasie).
With the measurements of the base station becoming available in real-time at the rover receiver, centimeter accurate position
solutions are obtained right at the spot.

#### RTK --- carrier phase observation equation [*]

The pseudorange observation equation was presented in ({ref}`eq:pseudorangeobseqn`)
for the purpose of standalone positioning. The errors discussed in Section~{ref}`sec:errorsources`
were basically all ignored.

The carrier phase measurement, Section~{ref}`sec:carrierphasemeasurement`, is much more precise
than the pseudorange --- the contribution to the error budget in Table~{ref}`tab:errorbudget`
by carrier phase multipath and receiver noise would only be at the millimeter to a few centimeter level.
The other error sources, like atmospheric delays and satellite related errors are taken into account now,
and put together in a delay parameter $d_{r}^{s}$.
The carrier phase observation equation, for the phase $\varphi_{r}^{s} = \lambda \frac{\Phi_{r}^{s}}{2\pi}$ expressed in meters, reads

$$
\begin{equation}
\underline{\varphi}_{r}^{s} = \underbrace{ \sqrt{(x^s-x_r)^2 + (y^s-y_r)^2 + (z^s-z_r)^2} }_{l_{r}^{s}} + b_r + d_{r}^{s} + \lambda N_{r}^{s} + \underline{e}_{r}^{s}
\end{equation}
$$

Parameter $N_{r}^{s}$ denotes the carrier phase cycle ambiguity, see Figure~{ref}`fig:ambiguity`.

#### RTK --- carrier phase positioning: parameter estimation [*]

We use *relative* positioning and develop the model of observation equations for a short baseline
(i.e.\ two receivers close together, up to 10-20~km distance).
The two receivers 1 and 2 being close together implies that the delays will be very similar
$d_{1}^{s} \approx d_{2}^{s}$ (keeping in mind that the satellite is some 20.000~km away),
and in the sequel we assume them to be really equal: $d_{1}^{s} = d_{2}^{s}$ (and residual errors are assumed to go into the $\underline{e}$-error terms).
With the position coordinates of the reference or base station $(x_1,y_1,z_1)$ being known,
and taking the difference of measurements across the two receivers, $\varphi_{1,2}^{s} = \varphi_{2}^{s} - \varphi_{1}^{s}$, we obtain

$$
\begin{equation}
\left( \begin{array}{c} \Delta \underline{\varphi}_{1,2}^{1} 
\Delta \underline{\varphi}_{1,2}^{2} 
\vdots 
\Delta \underline{\varphi}_{1,2}^{m} \end{array} \right)
 =
\left( \begin{array}{cccccccc} -u_{2,x}^{1} & -u_{2,y}^{1} & -u_{2,z}^{1} & 1 & \lambda & & &  
-u_{2,x}^{2} & -u_{2,y}^{2} & -u_{2,z}^{2} & 1 & & \lambda & &  
\vdots    &   \vdots     &   \vdots     & \vdots & & & \ddots & 
-u_{2,x}^{m} & -u_{2,y}^{m} & -u_{2,z}^{m} & 1 & & & & \lambda  
\end{array} \right)
\left( \begin{array}{c} \Delta x_{2} 
\Delta y_{2} 
\Delta z_{2} 
b_{1,2} 
N_{1,2}^{1} 
N_{1,2}^{2} 
\vdots 
N_{1,2}^{m} \end{array} \right) +
\left( \begin{array}{c} \underline{e}_{1,2}^{1} 
\underline{e}_{1,2}^{2} 
\vdots 
\underline{e}_{1,2}^{m} \end{array} \right)
\end{equation}
$$

with $b_{1,2} = b_2 - b_1$, $N_{1,2}^{s} = N_{2}^{s} - N_{1}^{s}$ and $\underline{e}_{1,2}^{s} = \underline{e}_{2}^{s} - \underline{e}_{1}^{s}$.
Note that when we would leave the ambiguities $N$ out, the above model in structure very much resembles model ({ref}`eq:standalonemodel`) for standalone positioning.
The goal of RTK-positioning is to estimate the position coordinates of the rover receiver $x_2$, $y_2$, and $z_2$,
and this is done while keeping the reference station fixed to the given position coordinates.

In the above model the receiver clock offset parameter $b_{1,2}$, as it is appearing equally in all equations,
can be removed by taking differences between measurements, e.g.\ $\varphi_{1,2}^{1,2} = \varphi_{1,2}^{2} - \varphi_{1,2}^{1}$.
The resulting model of taking differences all with respect to the first measurement $\varphi_{1,2}^{1}$, reads

$$
\begin{equation}
\left( \begin{array}{c} \Delta \underline{\varphi}_{1,2}^{1,2} 
\vdots 
\Delta \underline{\varphi}_{1,2}^{1,m} \end{array} \right)
 =
\left( \begin{array}{cccccc} -(u_{2,x}^{2}-u_{2,x}^{1}) & -(u_{2,y}^{2}-u_{2,y}^{1}) & -(u_{2,z}^{2}-u_{2,z}^{1}) & \lambda & & 
\vdots    &   \vdots     &   \vdots     &  & \ddots & 
-(u_{2,x}^{m}-u_{2,x}^{1}) & -(u_{2,y}^{m}-u_{2,y}^{1}) & -(u_{2,z}^{m}-u_{2,z}^{1}) & & & \lambda  
\end{array} \right)
\left( \begin{array}{c} \Delta x_{2} 
\Delta y_{2} 
\Delta z_{2} 
N_{1,2}^{1,2} 
\vdots 
N_{1,2}^{1,m} \end{array} \right) +
\left( \begin{array}{c} \underline{e}_{1,2}^{1,2} 
\vdots 
\underline{e}_{1,2}^{1,m} \end{array} \right)
\end{equation}
$$

With carrier phase measurements to $m$ satellites, we have $(m-1)$ of these so-called double difference measurements.
The receiver clock offset parameter has been cancelled.

These two optional sections provide a very brief introduction to carrier phase based positioning.
For a more in-depth coverage, the reader is referred to~Teunissen and Montenbruck [2017].
Least-squares estimation of *integer* parameters, such as the ambiguities $N$, is simple when there is
only one. Ordinary least-squares estimation yields a real-valued estimate for this parameter, and rounding
it to the nearest integer yields the integer least-squares estimate for the ambiguity.
With more ambiguity parameters present in the problem at the same time, as in the above model, this becomes a seriously complex problem
(for which an adequate solution is provided by the LAMBDA-method~Teunissen and Montenbruck [2017]).

Figure~{ref}`fig:ambiguouspositioning` provides a simple geometric interpretation of relative positioning
with carrier phase measurements which are inherently ambiguous, as only the fractional phase can be measured.
The rover receiver has to lie on one of the blue circle arcs, and at the same time on one of the green circle arcs.
The different arcs represent different integer values for the ambiguity. The rover receiver is at one of the intersections,
but as long as the ambiguities are not known, it is not known at which one.
For this geometric interpretation it is assumed that there is no effect of noise present in the measurements,
and the receiver clocks are assumed to behave perfectly ($b_1=b_2=0$).

````{figure} ../figures/GNSS/CPbasedpositioning.png
---
name: ambiguouspositioning
width: 60%
align: center
---
Geometric interpretation of relative positioning with carrier phase measurements, which are inherently *ambiguous*. The blue circle arcs, as possible solution for the rover receiver position result from the carrier phase measurement to the blue satellite, and the green circle arcs to those to the green satellite. The arcs are spaced by one wavelength $\lambda$ of the carrier wave.
````

#### RTK --- carrier phase positioning: example

With the equipment of Figure~{ref}`fig:ublox` a short experiment was carried out, lasting 1000 seconds.
Using measurements from a permanent GNSS reference station (only 2~km away, cf.\ Figure~{ref}`fig:skyplot`),
received in real-time using NTRIP, the receiver provided so-called RTK-fixed solutions (in ETRF2000).
For every epoch, i.e.\ once every second, a new position solution was computed, and the results are shown
in Figure~{ref}`fig:rtkfix`. The graph at left shows the horizontal position scatter, North-coordinate
versus East-coordinate, and the graph at right shows the vertical position (Up) as a function of time.
These measurements were taken at a survey-marker of which accurate position coordinates were already
available cf.\ Figure~{ref}`fig:CTB3310surveymarker`, so, in the graph of Figure~{ref}`fig:rtkfix` we actually present the position *error*,
i.e.\ the difference of the measured position coordinate and the known ground-truth position coordinate.
Hence, the origin of this graph refers to the `true' position.
The position errors are expressed in a local topocentric coordinate system, in terms of local
East, North and Up, see Section~29.4 in Tiberius et al. (2022).

````{figure} ../figures/GNSS/RTKfix_scatter.png
---
name: rtkfix
width: 60%
align: center
---
Example of Carrier Phase (CP) Real-Time Kinematic (RTK) positioning for a duration of 1000 seconds, on August 27th, 2021, with measurements of about 25 GNSS satellites, and successfully fixing the carrier phase ambiguities (RTK-fixed solution). At left: scatter of horizontal position error, at right: time series of vertical position error.
````

Table~{ref}`tab:rtkfix` presents the resulting empirical mean, standard deviation (std) and the root mean square
(rms), which is the square root of the MSE, see Chapter~6 in Tiberius et al. (2022) ,
of the position error in East, North and Up, confirming centimeter-accuracy of RTK-GPS positioning.
This is an improvement by a factor of 100 compared to the standalone positioning results in Figure~{ref}`fig:spppos`.

\begin{table}
\begin{center}
\begin{tabular}{|l|ccc|}
\hline
               & East & North & Up 
\hline
      mean [m] & 0.0016 & 0.0021 & 0.0068 
std [m]  & 0.0033 & 0.0039 & 0.0072 
rms [m]  & 0.0037 & 0.0044 & 0.0099 
\hline
\end{tabular}
\end{center}
\caption{Empirical mean, standard deviation (std) and root mean square (rms) of position error,
based on $N$=1000 Carrier Phase (CP) Real-Time Kinematic (RTK) position solutions (with ambiguities fixed).}

\end{table}

#### RTK --- carrier phase positioning: Digital Terrain Model (DTM)

Another short experiment was carried out to result in a centimeter-accurate 3D Digital Terrain Model (DTM)
of an embankment on the TU Delft campus, see Figure~{ref}`fig:talud`. The RTK survey of this bank of earth took only 15 minutes
(walking with the GNSS-receiver in a grid-like pattern over this bank, and recording measurements every 1 second).

````{figure} ../figures/GNSS/taludMekelpark.jpg
---
name: talud
width: 60%
align: center
---
Example of a centimeter-accurate 3D Digital Terrain Model (DTM) resulting from Carrier Phase (CP) Real-Time Kinematic (RTK) positioning. The DTM is presented in the national RD-NAP reference system (see Chapter~35 in Tiberius et al. (2022).
````

The RTK-fixed position solutions have been interpolated, and the resulting DTM is shown at right in Figure~{ref}`fig:talud`.
With the DTM one can easily evaluate numerically the amount of earthwork needed to create or remove this bank, in this case
442~$\mathrm{m}^3$.

#### Precise Point Positioning (PPP)

In those instances where a nearby reference receiver (or network) is not available or cost-prohibitive,
Precise Point Positioning (PPP) is an attractive alternative.
PPP only relies on a *global*, very sparse network of reference receivers
(e.g.\ some 40 receivers worldwide, and the nearest reference station can be 1000~km away, or even further), which
track the GPS satellites and compute corrections to the errors in the satellite orbits and clocks.
Conventional PPP uses dual-frequency data to eliminate the ionosphere delay, while a low-cost
variant uses single frequency data with a (predicted) ionosphere model. The fractional carrier phase
ambiguities cannot be eliminated, which means that integer least-squares estimation is not
possible. Ambiguities can still be estimated as constant values though, since an ambiguity does not
change as long as the receiver keeps tracking the satellite, a fact used in the PPP data processing.

However, because the ambiguities cannot be fixed to integer values, PPP suffers from a longer
convergence period than RTK (think of tens of minutes). After a convergence period in which the accuracy of the estimated
ambiguities improves gradually, the PPP solution starts relying more and more on the phase
measurements. The eventual position accuracy for dual-frequency PPP can reach centimeter, or even millimeter
level, while single frequency PPP can reach an accuracy of a few decimeter.

### Current developments

Much research effort is spent to try and combine the best aspects of PPP and RTK, i.e. using a
sparse (global) reference network and ambiguity resolution to enable precise positioning. Wide Area RTK and PPP-RTK are
based on the principles of RTK, but try to stretch the interstation distances to several hundreds of kilometers,
while PPP-AR starts from the global PPP network, and tries to solve the problem of ambiguity resolution (AR).
The ultimate goal is to achieve high precision positioning across a (very) large area.

````{figure} ../figures/GNSS/ubloxZED_F9P_NEW.jpg
---
name: ublox
width: 60%
align: center
---
At left: dual-frequency, multi-constellation GNSS receiver with receiver board at bottom, small patch-antenna (black) on top, and smartphone with Android positioning app at right; a total equipment cost of below 500 Euro (u-blox ZED-F9P), yet capable of providing cm-accurate RTK-GNSS positioning. At right: screenshot of SW Maps app by Softwel (P) Ltd.
````

Another development is to bring high-accuracy positioning techniques, e.g.\ RTK and PPP, to low-cost devices.
An example is shown in Figure~{ref}`fig:ublox`. The smartphone retrieves GPS differential corrections (or measurements)
of a nearby reference station through an Internet-connection using NTRIP, and forwards these to the GPS receiver, which is connected
via USB to the smartphone. The firmware on the GPS receiver chip combines the corrections with the measurements of the rover receiver,
and delivers a centimeter accurate RTK-position solution, which it relays back to the app on the smartphone.
This allows for centimeter accurate navigation, in real-time, with your smartphone.

The antenna of the rover receiver, at right in Figure~{ref}`fig:dgps`, is typically mounted on a lightweight range-pole,
for convenience of the survey-job. The position of the antenna on top of the range-pole is being measured (with GPS), and the
obtained coordinates are converted into those of the object or marker point occupied by the bottom-tip of the range-pole,
using the fact that the range-pole is being held vertically straight-up, and knowing its size.

Recently range-poles with built-in tilt compensation have become available. The tilt angle $\zeta$ is being
measured, for instance by means of an inertial measurement unit, and the horizontal displacement or offset is simply
found as $l \sin \zeta$, see Figure~{ref}`fig:tiltcompensation`.

````{figure} ../figures/GNSS/tiltcompensation.png
---
name: tiltcompensation
width: 60%
align: center
---
Principle of GPS range pole with tilt compensation. Tilt angle $\zeta$ is measured to provide, with known size $l$, the horizontal displacement $l \sin \zeta$.
````

Satellite Based Augmentation Systems (SBAS), e.g. the European EGNOS system, designed to enable GPS-based
aircraft precision approaches, rely on the same principles as PPP. However, given the primary application,
the focus is on integrity rather than accuracy (integrity refers to the trust that can be placed in the resulting position solution,
the solution is largely fault-tolerant). Carrier phase measurements are only here used to `smooth' the pseudorange solution.
SBAS is a pseudorange code Differential GPS approach for large geographical areas (wide areas).
An additional advantage of using SBAS is that the corrections are transmitted on the same radio frequency as GPS signals,
so no additional data link is necessary.

### Processing strategies, dynamic model and observation period

As already hinted at, the GPS position accuracy improves when the measurement time duration increases.
One important factor here is the *dynamic model* of the receiver motion, or how the measurement epochs can be `linked' to each other.

````{figure} ../figures/GNSS/gpsaccuracy.png
---
name: gpsaccuracy
width: 60%
align: center
---
Accuracy of various GPS positioning modes for a static receiver. The integration time is the total measurement duration, along the horizontal axis, and the position coordinates accuracy is along the vertical axis. Note the logarithmic scales. CP\&RTK stands for Carrier Phase and Real-Time Kinematic positioning.
````

If the receiver is stationary, the improvement will be most notable, as we can basically estimate a single position from many measurements
(a *static* solution). The position accuracy of a static receiver is shown as a function of the measurement duration in Figure~{ref}`fig:gpsaccuracy`
for each of the previously covered GPS processing strategies.

For a moving receiver the accuracy can also improve over time, if we can exploit the fact that some of the other parameters are constants,
e.g.\ the ambiguities, or, if the movement can be constrained or predicted to some extent based on the current position
(e.g.\ a car driving along a straight line, at constant velocity). This can be implemented with a Kalman filter,
or a recursive least-squares data processing algorithm.

In a *kinematic* solution, position coordinates are computed for each measurement instant (for instance every 1 second),
to accomodate the fact that the receiver is/was actually moving during the survey.
As a result one then obtains a *list* of position estimates, e.g.\ one every second, instead of one overall position solution
as with a static survey. The list describes the *track* or *trajectory* of the moving receiver.

Two related issues are:
1. The difference between *real-time* processing, and *post-processing* (for instance after whole survey has been completed),
where post-processed results are generally more accurate, but obviously not available right on the spot, and hence not suitable for certain applications.
2. The measurement rate of the receiver: GPS receivers often take pseudorange code, carrier phase, Doppler shift and signal-to-noise (SNR) measurements
once every second, hence at 1~Hz, but depending on the application, 10-20~Hz is also common practice today, and technically up to a 100~Hz measurement
rate is possible. To reduce the computational burden, data storage, and power requirement, lower measurement rates (e.g. once per 30 seconds)
are common in applications where objects move only very slowly, like in geoscience on measuring tectonic plate motion.
The impact of the measurement rate on the position accuracy is marginal (a higher data rate can slightly improve precision),
because the measurement errors are generally correlated in time. This means that
measurements taken in quick succession are not independent, and thereby do not offer, precision-wise, a lot of new/additional information.

## GNSS and applications

In this section we present a concise overview of Global Navigation Satellite Systems (GNSS),
addressing GPS, Glonass, Galileo and BeiDou. Then we briefly touch upon the wide range of applications of GNSS.

### Global Navigation Satellite Systems (GNSS)

The Global Positioning System (GPS), developed by the US military and operated by the US Air Force (USAF), is the first Global Navigation Satellite System
of its kind. In order not to be dependent on a US military system and/or to get their share of the GNSS market, other countries have developed their own Global Navigation Satellite Systems (GNSS).
The result is that today a lot of GNSS satellites can be seen at the same time, anywhere on Earth, anytime.
Figure~{ref}`fig:skyplot` shows as an example a so-called skyplot for Delft, with up to 40 GNSS-satellites in view.

Recently we have seen a significant increase in the available Global Navigation Satellite Systems, satellites, radio-frequencies and signals.
These developments are briefly reviewed in this section.

#### GPS

GPS is in the process of modernization. This is achieved by following up older satellites by new satellites with expanded and improved capabilities.
The civil L2C signal, for improved dual frequency (civilian) performance, becomes available on more and more satellites. Even
more importantly, new GPS satellites also transmit an additional (wideband) signal on the L5-frequency (of 1176.45~MHz) primarily designed for safety-of-life
applications (higher chiprate, hence shorter chiplength, and more precise pseudorange measurements).

#### Glonass

The Russian GLObal NAvigation Satellite System (GLONASS), has been fully replenished and at present has 24 active satellites.
Planned modernizations of GLONASS include an additional signal transmitted on the L5-frequency, and a switch from Frequency Division
Multiple Access (FDMA) to CDMA, which will increase interoperability with other GNSSes.

#### Galileo

Galileo, the European GNSS, is still under development, currently with 22 satellites. The full Galileo constellation
for Full Operational Capability will consist of 30 satellites. The Galileo system transmits navigation signals on four
different carrier frequencies: L1/E1, L5/E5a, E5b and E6, two of which (E5a and E5b) can also be
tracked together as one extra wideband (AltBOC) signal with unprecedented pseudorange accuracy.

#### BeiDou

The Chinese BeiDou Navigation Satellite System (BDS), sometimes still known as Compass, was
designed to provide independent regional navigation in the first stage and global coverage later.
The BeiDou (phase III) constellation deployment has been fully completed in 2020, with 30 satellites in orbit, providing global coverage.

#### Concluding remarks

````{figure} ../figures/GNSS/skyplotTrimbleNetR9_Oct2020.png
---
name: skyplot
width: 60%
align: center
---
Skyplot with GNSS satellites for October 8th, 2020, at 12:10 UTC, in Delft. The skyplot shows the positions of the satellites of the various constellations, like GPS, GLONASS, Galileo and BeiDou, in the sky. The outer circle represents the local horizon in Delft, 360 degrees around (0 is North, 90 East, etc). The smaller circles refer to 30 degrees of elevation, above the horizon, and 60 degrees of elevation. The middle of the skyplot corresponds to the so-called local zenith, which is directly overhead. The skyplot was obtained from the Trimble NetR9 GNSS receiver at the TU Delft observatory, of which the antenna set-up is shown at right.
````

The realized and expected upgrades of and additions to the available GNSS signals can have a
range of improvements on many GNSS applications. Some of the more important ones are: the
higher pseudorange accuracy of the new signals, the availability of many more satellites at once (more
satellites available to combat urban environments, see Figure~{ref}`fig:skyplot`), and both the availability of more radio-frequencies
and satellites.

Multi-GNSS positioning also brings new challenges, as so-called InterSystem Biases (ISB) are
introduced in the model. The system time as maintained by GPS may (will) not be the same as the
system time as maintained for Galileo, for instance. Hence one has to account for the fact that
these systems may have an offset in time with respect to each other. To use multiple systems
simultaneously in an optimal manner, these biases must be studied, and if possible corrected or
eliminated.

### Applications

There are many different applications of GNSS positioning each with its own requirements and,
related to that, a preferred processing strategy.

````{figure} ../figures/GNSS/trafficandtransport.jpg
---
name: trafficandtransport
width: 60%
align: center
---
Car navigation, route guidance and fleet management in traffic and transport are popular applications of GNSS positioning, where standard positioning service suffices. In future, assisted and automated driving will call for improved accuracy.
````

- smartphones, car navigation, and personal navigation usually have the lowest requirements,
      and the GPS (GNSS) standard positioning service suffices, cf.\ Figure~{ref}`fig:trafficandtransport`.
- lane specific navigation advice for road users requires sub-meter position accuracy, which can be
      fulfilled with single frequency PPP.
- surveying for creating maps and construction works, requires cm to mm position accuracy and will use RTK if available,
      or PPP otherwise, cf.\ Figures {ref}`fig:waterscooter` and {ref}`fig:talud`.
- deformation monitoring, due to Earthquakes, volcanic activity, mining or extraction of petroleum
      or natural gas, as well as any number of scientific applications require the highest possible accuracy
      and use carrier phase based positioning.
- aircraft precision approach and landing requires high integrity positioning, and can use SBAS to obtain this.
- machine guidance, as shown in Figure~{ref}`fig:excavator` and in particular self-driving vehicles
      require high accuracy and integrity; this can be achieved by using RTK-GNSS
      though this is still subject of research, and likely fusion with additional sensors is in order.

````{figure} ../figures/GNSS/GPSsurveyZandmotor.jpg
---
name: waterscooter
width: 60%
align: center
---
Both the on- and offshore part are regularly surveyed, to monitor the development of the Zandmotor (The Sand Engine), at the Dutch North-Sea coast, near Ter Heijde. This `building with nature' project started in 2011, and at right an aerial photo of the Zandmotor is shown, looking in Southern direction. High-precision RTK-GPS is used for positioning the quad on shore, and the jet-ski in the water (note the GPS-antenna at the back of the jet-ski, in the inset). The measurements by the quad result in a Digital Terrain Model (DTM), and echo sounder depth measurements by the jet-ski result in a seafloor-map. Photo at left by Matthieu de Schipper.
````

````{figure} ../figures/GNSS/KPNmastZvbh.jpg
---
name: KPNtelecommast
width: 60%
align: center
---
A GPS receiver is commonly used to synchronize base stations for telecommunication. Requirements on time-synchronization for this application lie in the order of a $\mu$s. The photo shows a base station with a height of 37~m, providing the full range of mobile services from 2G (GSM) to 5G (NR).
````

There is also a number of GNSS applications, in which the position solution is not the (primary) goal.
Accurate time which is obtained through determining also the receiver clock offset $b_r$,
is used in timing applications. The standard positioning service allows for timing at the 10-100~ns level,
and this is used for instance in telecommunication, cf.\ Figure~{ref}`fig:KPNtelecommast`, electrical power grids,
and financial networks.

Nuisance parameters such as the atmospheric delays can also be used as observational input e.g.\ to determine, together with using models,
the state of the Earth's ionosphere, or derive troposphere delays, for instance for Numerical Weather Prediction (NWP).

GNSS radio-signals can also be used outside of their intended purpose, e.g.\ to determine sea-level height by measuring reflected GNSS signals
from orbit.

### Resources

This part provides an introduction to positioning with GPS/GNSS. For a lot more of technical and mathematical modeling information
on GPS and GNSS positioning, navigation and timing, the reader is referred to Teunissen and Montenbruck [2017] and Morton et al. [2021]. These textbooks also cover a wide
range of applications.

The first source of information on GPS, as well as the point of contact is the [Navigation Center of the US Coast Guard](http://www.navcen.uscg.gov/)(United States Coast Guard).
Official U.S. government information about GPS is available through (https://www.gps.gov/)~(US Government).

The first source of information on Galileo and point of contact is the European Union Agency for the Space Programme ([EUSPA](https://www.euspa.europa.eu/)).

The [IGS](https://igs.org/) is the International GNSS Service, a voluntary federation of universities and research institutions, operating permanent GNSS stations worldwide,
and providing GNSS data and products for high(est)-precision applications (IGS).

### Exercises and worked examples

This section presents a couple of questions and problems with (worked) answers on GPS-positioning.

\vspace{3mm}

**Question~1** What are the largest remaining error sources in short-baseline DGPS, explain your answer.

**Answer~1** The atmosphere delays as well as the satellite orbit and clock errors are eliminated in
DGPS, cf.\ Figure~{ref}`fig:dgps`, which leaves multipath and (pseudorange) measurement noise as the largest error sources,
cf.\ Figure~{ref}`fig:signalpath` and Table~{ref}`tab:errorbudget`.

\vspace{3mm}

**Question~2** If a certain application requires decimeter positioning accuracy, which GPS positioning modes can be considered?
And for how long a time would we need to collect measurements?

**Answer~2** Real-Time Kinematic (RTK) provides decimeter or even centimeter accuracy as soon as the ambiguities can be
fixed, which generally is (well) within 100 seconds of measurements, and even faster in post-processing.
PPP can also provide decimeter accuracy after several minutes. DGPS can reach decimeter accuracy as
well, but may considerable time to allow for averaging (with static positioning only), for instance one hour.
SBAS and standalone GPS often do not reach decimeter accuracy even after one or several days (averaging with static positioning),
especially in the vertical component. An overview of the attainable accuracies can be found in Figure~{ref}`fig:gpsaccuracy`.

\vspace{3mm}

**Question~3** The principle of GPS satellite positioning and navigation consists of determining the range
from satellite to receiver through measurement of the signal travel-time. The atomic clock in the satellite is perfectly on time.
When the receiver clock is ahead of time by 0.1~$\mu$s, by how much is the measured range to the satellite too long or too short?

**Answer~3** From Eq.~({ref}`eq:clockerror`) we can see that clock error $\delta t_{r}$ is positive, as the receiver clock
is ahead of time, hence $t_{r} > t$. Next, with Eq.~({ref}`eq:pseudorange`), and $c \delta t_{r} = b_r = 30$~m, we find that
the pseudorange $p_{r}^{s}$ is too long by 30~m (compared to the actual distance $l_{r}^{s}$).

````{figure} ../figures/GNSS/1D_GPSpositioning.png
---
name: 1D_GPSpositioning
width: 60%
align: center
---
One-dimensional GPS positioning (Question~4).
````

**Question~4** The GPS positioning problem has been simplified to a single dimension. There are two satellites A and B,
and the user receiver is at R, see Figure~{ref}`fig:1D_GPSpositioning`. The positions of the satellites are known, A is at $x_A=0$, and B is at $x_B=10$.
The position of the user $x_R$ is unknown. Two pseudoranges have been measured: $p_{AR} = 9$ and $p_{BR} = 7$.
Determine the position (coordinate) of the user at R.

**Answer~4** Looking at Figure~{ref}`fig:1D_GPSpositioning` we identify two geometric ranges, namely $l_{AR} = x_R - x_A$
and $l_{BR} = x_B - x_R$ (mind to define these distances to be positive). Then, with Eq.~({ref}`eq:pseudorange`),
we formulate two observation equations:

$$
\begin{equation}
\begin{array}{lll} p_{AR} & = & l_{AR} + b_R 
p_{BR} & = & l_{BR} + b_R    \end{array}
\end{equation}
$$

which gives

$$
\begin{equation}
\begin{array}{lll} p_{AR} & = & x_R - x_A + b_R 
p_{BR} & = & x_B - x_R + b_R    \end{array}
\end{equation}
$$

and with the given satellite positions, we obtain

$$
\begin{equation}
\begin{array}{lll} p_{AR} + x_A & = & x_R + b_R 
p_{BR} - x_B & = & - x_R + b_R    \end{array}
\end{equation}
$$

We have two equations with two unknown parameters, namely $x_R$ and $b_R$, which we can solve, giving $x_R = 6$ and $b_R = 3$.
The user position coordinate equals $x_R = 6$, and we are typically not interested in the receiver clock offset.
It is easily verified that correcting the measured pseudoranges for the receiver clock offset yield the actual distances
from the two satellites to the receiver: $p_{AR} - b_R = 9-3=6$ and $p_{BR} - b_R = 7-3=4$.

\vspace{3mm}

**Question~5** The GPS relative positioning problem has been simplified to a single dimension. There is one satellite `sat' (or just `s')
and it is visible at the local horizon. The receivers `1' and `2', and the satellite are all on a straight line (along the x-coordinate axis),
see Figure~{ref}`fig:singledifference`. The radio-signals from the satellite to the two receivers pass through the Earth's atmosphere (layer `atm')
and get thereby delayed; the delay, expressed in units of range, is denoted by $d^s$. This delay is unknown (but *equal* for the signals to both receivers).
The satellite position is known, $x^{s} = -20$, and the position of receiver~1 as well $x_1 = 5$. Compute the position of receiver~2, $x_2$,
based on the pseudorange measurements $p_{1}^{s} = 32$ and $p_{2}^{s} = 37$.
In this case, you can again assume that all clocks run perfectly on time – there are no clock offsets involved.

````{figure} ../figures/GNSS/singledifference.png
---
name: singledifference
width: 60%
align: center
---
Relative positioning in one dimension (Question~5).
````

**Answer~5** The pseudorange observation equation ({ref}`eq:pseudorange`) needs to be adapted. There is no clock offset involved at all,
so parameter $b_r$ cancels, but now, we face an unknown atmospheric delay~$d^s$. Hence

$$
\begin{equation}
\begin{array}{lll} p_{1}^{s} & = & l_{1}^{s} + d^s 
p_{2}^{s} & = & l_{2}^{s} + d^s    \end{array}
\end{equation}
$$

Looking at Figure~{ref}`fig:singledifference` we identify two geometric ranges, namely $l_{1}^{s} = x_1 - x^s$
and $l_{2}^{s} = x_2 - x^s$ (mind to define these distances to be positive). Then the two observation equations become:

$$
\begin{equation}
\begin{array}{lll} p_{1}^{s} & = & x_1 - x^s + d^s 
p_{2}^{s} & = & x_2 - x^s + d^s    \end{array}
\end{equation}
$$

where there are two unknown parameters, namely $x_2$ and $d^s$. With the given measurements and coordinates, this is easily solved, to
yield $x_2 = 10$ and $d^s = 7$. Alternatively one could take the difference of the two pseudorange measurements
$p_{2}^{s} - p_{1}^{s} = x_2 - x_1$, which gives an identical result for $x_2$, and one is generally not interested in parameter~$d^s$.

## References

06-GPS. Image of network of permanent GPS tracking stations in the Netherlands, Belgium and Luxemburg.
Sliedrecht, The Netherlands, 2021. URL https://www.06-gps.nl/.
24
Boeing. Image of GPS block IIF satellite. Chicago, Illinois, n.d. URL https://www.boeing.com/space/
global-positioning-system/.
Bundesamt f¨ur Kartographie und Geod¨asie (BKG). The BKG GNSS Data Center — BKG Ntrip Client
(BNC), n.d. URL https://igs.bkg.bund.de/. website of the German Federal Agency for Cartography
and Geodesy.
M. de Schipper. Photo of RTK-GPS positioning with a quad on shore, and a jet-ski in the water, at the
Zandmotor, n.d.
European GNSS Agency. Gsa gnss market report. Technical report, European Union Agency for the Space
Programme (EUSPA), 2019. URL https://www.euspa.europa.eu/.
European Union Agency for the Space Program (EUSPA). European Union Agency for the Space Programme
(EUSPA), n.d. URL https://www.euspa.europa.eu/. website.
Heijmans N.V. Photo of excavator in the process of constructing a motorway embankment, guided by RTKGPS.
Rosmalen, The Netherlands, n.d. URL https://www.heijmans.nl/.
International GNSS Service (IGS). International GNSS Service (IGS), n.d. URL https://igs.org/. website.
J. Morton, F. van Diggelen, J. Spilker, and B. Parkinson, editors. Position, Navigation, and Timing Technologies
in the 21st Century: Integrated Satellite Navigation, Sensor Systems, and Civil Applications, Volume
1 and 2. Wiley - IEEE Press, 2021. doi: http://dx.doi.org/10.1002/9781119458449.
A. Smits. Visualization of GPS positioning, n.d. Delft University of Technology.
T. Takasu. RTKLIB: An Open Source Program Package for GNSS Positioning, n.d. URL http://www.
rtklib.com/. website.
P. Teunissen and O. Montenbruck, editors. Springer handbook of Global Navigation Satellite Systems. Springer
Handbooks. Springer Verlag, 2017. doi: http://dx.doi.org/10.1007/978-3-319-42928-1.
C. Tiberius, H. van der Marel, R. Reudink, and F. van Leijen. Surveying and Mapping. TU Delft OPEN Books,
Nov. 2022. doi: 10.5074/T.2021.007. URL https://books.open.tudelft.nl/home/catalog/book/163.
United States Coast Guard. Navigation Center, n.d. URL https://www.navcen.uscg.gov/. website of the
United States Coast Guard (USCG), U.S. Department of Homeland Security, Navigation Center.
U.S. government. Official U.S. government information about the Global Positioning System (GPS) and
related topics, n.d. URL https://www.gps.gov/. GPS.gov website.
Wikimedia Commons. Wikimedia Commons, n.d. URL https://commons.wikimedia.org/. media file
repository, for public domain and freely licensed educational media content.
25