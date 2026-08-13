# GNSS Positioning

This chapter is based on Tiberius et al. (2022) (this book is published under a CC BY-NC-SA license).

## Introduction on GNSS and applications

Global Navigation Satellite Systems (GNSS) are used for a wide variety of applications -- not only in our daily life to find our way with a smartphone or car navigation system -- but also in many Earth, Climate & Technology applications. Being able to accurately determine the 3D position of points and objects on Earth allows for instance to maintain [reference frames](CRS) and create maps. It also allows to observe changes in the (relative) positions of those points and objects. This is very important for monitoring applications such as:

* Ground subsidence due to natural processes (eg peat compaction, ice melt) or human activities (groundwater injection/ extraction)
* Land motion due to tectonics, volcanic activity and landslides.
* Deformation of infrastructure such as dikes and buildings.

Navigation and positioning are also (indirectly) used for Earth, Climate & Technology applications: for instance if we take ground-based or remote sensing measurements we need to know where the sensor was at the time of measurement. A more extensive list of applications can be found in Section *GNSS Applications*.

The Global Positioning System (GPS), developed by the US military and operated by the US Air Force (USAF), is the first Global Navigation Satellite System, and most well-known system, of its kind. In order not to be dependent on a US military system and/or to get their share of the GNSS market, other countries have developed their own GNSS.
The result is that today a lot of GNSS satellites can be seen at the same time, anywhere on Earth, anytime. {numref}`Figure {number} <skyplot>` shows as an example of a so-called skyplot for Delft, with up to 40 visible GNSS-satellites in view.

````{figure} ../../figures/GNSS/skyplotTrimbleNetR9_Oct2020.PNG
---
name: skyplot
width: 60%
align: center
---
Skyplot with GNSS satellites for October 8th, 2020, at 12:10 UTC, in Delft. The skyplot shows the positions of the satellites of the various constellations, GPS, GLONASS, Galileo and BeiDou, in the sky. The outer circle represents the local horizon in Delft, 360 degrees around (0 is North, 90 East, etc). The smaller circles refer to 30 degrees of elevation, above the horizon, and 60 degrees of elevation. The middle of the skyplot corresponds to the so-called local zenith, which is directly overhead. The skyplot was obtained from the Trimble NetR9 GNSS receiver at the TU Delft observatory, of which the antenna set-up is shown at right.
````

### GPS

The Global Positioning System (GPS), also known as the NAVigation Satellite Time And Ranging (NAVSTAR) system, is one the most successful satellite systems to date. Its success is strongly linked to the ever-decreasing costs of GPS receivers, which primarily consist of electronic hardware. While high-end receivers still cost in the order of 1-10kEuro, mass-market receivers, such as those used in smartphones, cost no more than a few euros each.

Currently there are about as many GNSS devices on Earth as people, more than 7 billion, the vast majority of which are in smartphones. The global GNSS downstream market revenues, from both devices and services, were in 2020 around 150 billion Euro, according to the market report by the European GNSS Agency (GSA), now the European Union Agency for the Space Programme (EUSPA) (European GNSS Agency, 2019).

The first GPS satellite was launched back in February 1978. GPS is a *one-way* radio ranging system which provides real-time knowledge of one's Position and Velocity, and a very accurate Time reference as well (all together referred to as PVT).

GPS was designed to provide Positioning, Navigation and Timing (PNT) functionality, which is very valuable not only for the US military, for which it was first developed, but also to a myriad of commercial activities, as well as the general public at large.

The GPS system consists of three segments.
1. The space segment, consisting of 24 or more satellites, with accurate atomic clocks on board, continuously transmitting ranging signals to Earth.
2. The control segment, consisting of a number of ground stations, which monitors the satellites, computes their orbits and clock offsets, and uploads this information to the satellites, which in turn encode this information on the ranging signal (the so-called navigation data).
3. The user segment, simply consisting of many GPS receivers, which each track four or more GNSS satellites, and compute their own position.

The other three GNSSs have a very similar design and functionality.

### Glonass

The Russian GLObal NAvigation Satellite System (GLONASS) was developed from the 1970's onward. It is similar to GPS, but with its own signal and constellation design. Currently, GLONASS has about 24 operational satellites in orbit.

### Galileo

Galileo, the European GNSS, has been under design and development since the late 1990's. Again, it has its own design in terms of signals and constellation, but based on *interoperability* with GPS. That is why your smartphone, and the vast majority of GNSS receivers, use GPS and Galileo (and even other GNSSs) at the same time.

### BeiDou

The Chinese BeiDou Navigation Satellite System (BDS), sometimes still known as Compass, was designed to provide independent regional navigation in the first stage and global coverage later. The BeiDou (phase III) constellation deployment has been fully completed in 2020, with 40+ satellites in orbit, providing global coverage.

### Outline

This chapter provides an introduction to GNSS positioning. 
Section *Ranging* presents the basic concepts of the measurement of travel time of a radio signal from a GNSS satellite to a receiver.
With these measurements of range as input, Section *GNSS Positioning* describes the default mode of GNSS positioning, referred to as stand-alone or single-point positioning. The next section introduces the concept of relative positioning, by means of which high-accuracy, centimeter-level positioning is made possible.
Section *GNSS applications* presents an overview of the wide range of applications of GNSS in today's society.

There is much more more of information available on this subject, and
the reader is therefore referred to, for instance, the textbooks Teunissen and Montenbruck [2017] and Morton et al. [2021].

````{figure} ../../figures/GNSS/GPSsatelliteblockIIF.jpg
---
name: GNSSblockIIF
width: 50%
align: center
---
GNSS block IIF satellite, built by Boeing. These GNSS satellites, 12 in total, have been launched between 2010 and 2016. They have a design lifetime of 12 years. The full GNSS constellation nominally consists of 24 satellites. Image courtesy of Boeing.
````

## Ranging

### Radio signal

The GNSS satellites transmit signals in the so-called L-band of the electromagnetic radio frequency spectrum, which corresponds to the 1 to 2 GHz range. The signal consists of a carrier wave, and each satellite adds its own unique *Pseudo Random Noise (PRN)* code on it, see {numref}`figure {number} <GNSSsignal>`, as well as information about the satellites' orbits and clocks. The PRN code allows a receiver to identify from which satellite a signal originates, and also *when* it was transmitted. And with that, it is thus possible to determine the travel time of the signal.

````{figure} ../../figures/GNSS/gpssignal.png
---
name: GNSSsignal
width: 80%
align: center
---
The GPS L1 signal is composed of a carrier wave (a sinusoid with a frequency of 1575.42 MHz; not to scale in the above diagram), a PRN code (a sequence of '0' and '1' bits, here represented by values '-1' and '+1', and unique for each satellite), and a low rate navigation data message. The figure illustrates how the PRN code and data message are *modulated* on the carrier wave: basically by multiplying the carrier by the '-1' and '+1' values of the spreading code and navigation data, and the resulting modulated signal is shown at bottom.
````

### Measurement of range

GNSS offers two types of range measurements: pseudorange measurements and carrier phase measurements.

#### Pseudorange measurement

A GNSS receiver typically consists of tens to hundreds of so-called channels, and will allocate each of these to a specific GNSS satellite. When a GNSS receiver first starts up, it will begin to search for a particular GNSS satellite on each of its channels. Once the receiver has locked onto a signal of a particular satellite, it can start regularly taking code measurements. These are also referred to as *pseudorange* measurements, since the *travel time* $\tau_r^s$ of the radio signal from satellite $s$ to receiver $r$ is a measure for the *range* (or: distance) from satellite to receiver, as shown below:

$$
\begin{equation}
\tau_{r}^{s} = t_r - t^s
\end{equation}
$$

where $t^s$ is the time the signal was transmitted by the satellite, and $t_r$ the time the signal was received at the receiver, later noting that these clocks will both deviate from the true time. The measured travel time is converted into the pseudorange $p_{r}^{s}$, expressed in unit meter by multiplying with the speed of light $c$ in vacuum ($c \approx 3 \cdot 10^8$ m/s):

$$
\begin{equation}
p_{r}^{s} = c \tau_{r}^{s}
\end{equation}
$$

The pseudorange represents the travel time of the signal, and thereby ideally the distance from satellite to receiver. In practice it is affected
by the satellite clock offfset from the true time (to some extent known to the receiver through the navigation message), the receiver clock offset, which is unknown, and a number of additional delays, which we cover in the sequel, see {numref}`figure {number} <signalpath>`.

The receiver clock error is caused by the oscillator in the receiver, driving the clock, which will not behave perfectly. Therefore the receiver clock may run ahead of time or lag behind, and the clock error will also be changing over time. 

The time shown by the receiver clock is denoted by $t_r(t)$, it equals true time $t$ of signal reception, plus a so-called clock offset $\delta t_{r}(t)$ at time $t$, hence

$$
\begin{equation}
t_{r}(t) = t + \delta t_{r}(t)
\end{equation}
$$

When the receiver measures the travel time, to eventually produce the pseudorange measurement, it 'reads' the moment of signal arrival at its own clock, and hence this measurement is off by an amount of $\delta t_{r}(t)$. The *measured* travel time is then

$$
\begin{equation}
\tau_{r}^{s}(t) = t_{r}(t) - (t-\tau(t))
\end{equation}
$$

where $t-\tau(t)$ is the time at which the signal was transmitted (true reception time $t$ minus travel time $\tau(t)$). For simplicity we ignore any remaining satellite clock errors, since the satellites carry very precise atomic clocks which are monitored by the ground segment (corrections are sent with the navigation message).

Substituting here the expression for $t_{r}(t)$ and multiplying by the speed of light now gives:

$$
\begin{equation}
p_{r}^{s}(t) = c \tau_{r}^{s}(t) = \underbrace{c \tau(t)}_{l_{r}^{s}(t)} + \underbrace{c \delta t_{r}(t)}_{b_{r}(t)}
\end{equation}
$$

where, in the absence of for instance atmospheric delays, $l_{r}^{s}$ denotes the geometric distance between satellite and receiver.

This equation shows that the *pseudorange* is a measure for the geometric distance $l_{r}^{s}$, apart from the receiver clock offset $b_r$, and hence
the term *pseudo*range.

#### Carrier phase measurement

Additionally, a GNSS receiver may measure the *fractional* phase difference between the received carrier wave from the satellite
and a locally generated copy (replica). And, it can keep track of the number of cycles of the carrier wave since the start of tracking,
together known as the *carrier phase* measurement. This measurement includes the accumulated number of 'zero-crossings' since
lock-on of the signal (for instance, when the fractional phase jumps from $1.99 \pi$ to $0.02 \pi$, the full period is accounted for
and the resulting carrier phase measurement, output by the receiver, is $2.02 \pi$).

The carrier wave measurement is a very precise measure of the distance between the satellite and the receiver, but the initial number of carrier wave cycles is unknown, and needs to be estimated before the carrier phase measurements can be effectively used, see {numref}`figure {number} <ambiguity>`.

````{figure} ../../figures/GNSS/ambiguity.png
---
name: ambiguity
width: 60%
align: center
---
Carrier phase measurement: only the *fractional* phase difference can be measured, shown in red in units of length [m] (fractional phase $\Phi \in \left[0,2\pi \right \rangle $ expressed in radians, converted to distance: $\varphi = \lambda \frac{\Phi}{2\pi}$). The total distance from the satellite to the receiver equals the observed fractional phase difference plus multiple wavelengths $N\cdot \lambda$. The unknown integer number ofwavelengths $N$ at the start of signal tracking, is referred to as ambiguity. In this illustrative example $N = 4$.
````

#### Concluding remarks on range measurements

GNSS receivers can also provide additional measurements, such as the signal strength and Dopplier frequency (a measure for the relative velocity of receiver with respect to satellite). This is beyond the scope of this course. More details can be found in Tiberius et al. (2022).

The pseudorange measurement precision is typically at the  decimeter level. The carrier phase measurement precision ranges from the few centimeter to the millimeter level. The carrier phase is an ambiguous measurement of distance, but it is more precise than the pseudorange, typically by two orders of magnitude.

````{figure} ../../figures/GNSS/graphC1.png
---
name: graphsC1
width: 60%
align: center
---
Example of time series of (at left) C1 pseudorange measurements, in meters, of a stationary, permanent receiver in Delft.
````

{numref}`Figure {number} <graphsC1>` shows measurements of one satellite, collected by a stationary receiver in Delft as a function of time. A pass-over of a GNSS satellite typically takes several, up to 7 hours. With a nearly circular orbit of the GNSS satellite around the Earth, the distance from satellite to receiver is shortest when the satellite is directly overhead. You can see that the satellite appears above the horizon later during the day at another location in the sky due to the Earth's rotation and the satellite orbiting the Earth.


### Ionospheric delays and multi-frequency ranging

One of the major error sources in GNSS is due to the ionosphere, see {numref}`Figure {number} <signalpath>` and Table 1. The ionosphere is an ionized part of the Earth's upper atmosphere. There solar radiation separates electrons from neutral gas atoms and molecules. The free electrons in the ionosphere delay the radio signals, and thus affect the range measurements, with delays in terms of distance ranging from a few meter to hundreds of meters.

The largest delays occur round the geomagnetic equator around local noon, and during solar maxima. The ionospheric delay may be highly variable, as a function of both time and space.

One way of dealing with the ionospheric delay is to track signals from the same satellite on two or more frequencies. The ionosphere delay scales,
to a very good approximation, with the inverse of the square of the radio frequency of the signal, and this relation can be used to create the so-called
ionosphere-free range measurements (a linear combination of measurements at two different frequencies, from which the ionospheric delay has been
removed). For this reason the GNSS satellites were originally designed to transmit ranging signals on both the L1 (1575.42 MHz) and L2 (1227.60 MHz) frequency.

## Positioning

GNSS positioning is based on the concept of multi-lateration. By measuring distances to a number of GNSS satellites, as shown in {numref}`figure {number} <GNSSpositioning>`, and using the known satellite positions, a GNSS receiver can compute its own position. The satellite positions are indeed assumed to be known, since the ground segment is constantly determining where the satellites are, and their predicted positions are broadcasted with the navigation message.

To estimate the three position coordinates of the receiver $x_r$, $y_r$, $z_r$, and the receiver clock offset $b_r$, a GNSS receiver needs to track at least 4 satellites.

````{figure} ../../figures/GNSS/GPSpositioning.png
---
name: GNSSpositioning
width: 60%
align: center
---
GNSS positioning --- in three dimensions --- is based on measuring pseudoranges to at least four satellites, of which the positions are known. Visualization by Axel Smits.
````

### Geometric interpretation

Knowing the distance to an object (satellite) at a known position, translates into being on a circle (in 2D) or a sphere (in 3D) around this object with the satellite in the center.
As we have seen, the GNSS pseudorange measurement relates to the geometric range (distance) from satellite to receiver plus an offset caused by the receiver clock. This means, the pseudorange gives us the distance from satellite to receiver, but it may or will be too small, or too large by a certain amount, namely the receiver clock offset $b_r$. The good news is that the receiver clock offset is the *same* for all pseudoranges measured by the receiver at a specific time. If the receiver clock is ahead of GNSS-time, all pseudoranges will be measured too long, and by the same amount. This leads us to the approach of solving for three position coordinates and the receiver clock error at the same time, and hence, requiring pseudorange measurements to at least four satellites (rather than three).

To see the effect of the receiver clock error on the positioning problem at work, we consider a simple two-dimensional positioning example (in which we assume that there are no remaining errors present in the pseudorange measurements).
So, in two dimensions, we would need to solve for two receiver position coordinates and one receiver clock error, hence in total three unknown parameters,
so we need at least three pseudorange measurements.

````{figure} ../../figures/GNSS/trilateration_greenblue.PNG
---
name: trilaterationgreenblue
width: 80%
align: center
---
Two-dimensional positioning example with three satellites (at known positions, represented by the black dots). The measured pseudoranges are visualized by circles, in green at left (with clock error of -1), and in blue at right (with clock error of 0).
````

````{figure} ../../figures/GNSS/trilateration.png
---
name: trilateration
width: 60%
align: center
---
The process of determining the receiver clock offset: the measured pseudoranges have to be reduced or enlarged, but all with exactly the same amount, in order to meet at one physical position. The amount to make that happen is the receiver clock offset. The different colors represent different values for the receiver clock offset.
````

In {numref}`figure {number} <trilaterationgreenblue>` at left, the measured pseudoranges are shown in green, and obviously these three green circles do not all meet in one point. The pseudoranges are 'too short', the reason obviously being the receiver clock lagging behind. Without the clock error (and again in the absence of any other errors), we would have obtained the circles as shown in blue on the right, where the intersection of all three circles is in one point. Hence, we need to find the clock offset such that we find the 'perfect' intersection and hence we need to solve for the two position coordinates and the receiver clock offset at the same time. This clearly demonstrates that positioning and timing are intimately related!

### Pseudorange observation equation

With expanding the one-way geometric range $l_{r}^{s}$ between satellite $s$ and receiver $r$ as

$$
\begin{equation}
l_{r}^{s} = \sqrt{(x^s-x_r)^2 + (y^s-y_r)^2 + (z^s-z_r)^2}
\end{equation}
$$

using a three-dimensional Cartesian coordinate system as shown in {numref}`figure {number} <ECEF>`, the pseudorange observation turns into

$$
P_{r}^{s} = \sqrt{(x^s-x_r)^2 + (y^s-y_r)^2 + (z^s-z_r)^2} + b_r + \epsilon_{r}^{s}
$$

where we omitted the argument of time $t$. The satellite position coordinates at time of signal transmission are
$x^s$, $y^s$ and $z^s$, and the receiver position coordinates at time of signal reception are $x_r$, $y_r$ and $z_r$.
Recall that the approximate satellite position and clock offset are available to the user through the navigation data message.

Parameter $b_r$ equals the receiver clock offset $\delta t_r$ multiplied by the speed of light $c$. Note that we included the (unavoidable) random measurement error $\epsilon_{r}^{s}$ on the right hand side the equation.

````{figure} ../../figures/GNSS/ECEF.png
---
name: ECEF
width: 40%
align: center
---
Three-dimensional Cartesian Earth-Centered Earth-Fixed (ECEF) coordinate system for GNSS positioning.
````

### Positioning: parameter estimation

If we obtain pseudorange observations of four satellites, we should now be able to solve the corresponding system of equations (four equations, four unknowns). However, obviously the equations are still non-linear, and hence you cannot yet put the sytem of equations in matrix-vector format as you learned in linear algebra. Moreover, in practice, we typically observe more than four satellites, and of course we would like to use all of them (recall the principle of reducing measurement uncertainty by taking more measurements). Later in the course you will learn how to use least squares estimation and linearization to solve this problem of estimating the four unknown parameters.

### Reference systems

Relying, by default, on the given satellite positions in the navigation message of the GNSS signal, GNSS positioning yields Cartesian coordinates
$(x,y,z)$ in WGS84, the World Geodetic System 1984, which is an Earth-Fixed, Earth-Centered (ECEF) coordinate system, as presented in {numref}`figure {number} <ECEF>`. These Cartesian coordinates can be converted into geographic, or ellipsoidal coordinates latitude $\varphi$, longitude $\lambda$,
and ellipsoidal height $h$, see [Coordinate Reference Systems](CRS).

In differential mode (introduced in the next section), the position coordinates for the user receiver are in the same reference system as the position coordinates of the base, or reference station, generally provided in a local or regional reference system (e.g., ETRS89 in Europe, a realization of the European Terrestrial Reference System).

### GNSS accuracy and error sources

The quality of the GNSS position solution is largely dependent on the number of available satellites and their geometry with respect to the user. If enough satellites are visible on all sides of the receiver, at high and low elevation angles, a good position accuracy can be expected.

The only weakness in the geometry is the fact that there are no satellites visible beneath the receiver, as one cannot track and observe satellites below the local horizon. As a result vertical position accuracy is generally poorer than the horizontal accuracy by about a factor of 1.5.

In many practical situations one or more satellite signals are *blocked* by surrounding buildings or other obstacles which is called shadowing. In this case GNSS performance might be significantly degraded. Furthermore, in built-up areas, GNSS receivers often experience signal reflections,
i.e., signals arrive at the receiver after bouncing off an object. Since the reflected signal path is always longer than the direct path, this causes a corresponding error in the range measurement. It is also possible that both the direct and reflected signals arrive at the receiver,
which is referred to as *multipath*. In this case, the receiver must deal with the superposition of these signals, generally resulting in a biased range measurement, see {numref}`figure {number} <multipath>`.

Carefully selecting the location for a survey can help to keep the impact of multipath at a minimum, as well as the use of a good antenna.

````{figure} ../../figures/GNSS/multipath.png
---
name: multipath
width: 50%
align: center
---
Multipath: the direct line of sight signal from the satellite is received, though as well as a signal which has been reflected by the building. The reception of also a reflected signal, which has made a detour, will generally cause a bias in the measurement.
````

````{figure} ../../figures/GNSS/errorsources.png
---
name: signalpath
width: 50%
align: center
---
GNSS error sources.
````

The accuracy of *standalone positioning* with GNSS, also referred to as single-point positioning, or absolute positioning, in the order of 5-15 meters under reasonable satellite visibility, is limited by the accuracy of the range measurements.

The GNSS pseudorange measurements contain errors due to inaccurate satellite orbit and clock information,
delays along the path of the radio signal, including atmospheric delays (ionosphere and troposphere), local effects including multipath, and measurement noise, see {numref}`figure {number} <signalpath>` and the table below.

| error source    | 95%-value |
|:----------------|:---------:|
| satellite orbit |    2 m    |
| satellite clock |   2-5 m   |
| ionosphere      |  15-90 m  |
| troposphere     |   20 m    |
| multipath       |  1-10 m   |
| receiver noise  |   1-3 m   |
| total range     |  5-10 m   |

Table 1: GNSS error budget for standalone positioning, see also {numref}`figure {number} <signalpath>`. The errors are given in the range domain, using the satellite (broadcast) navigation data message, and after Klobuchar ionospheric model
correction (which in practice yields a 50\% reduction of the ionospheric delay error), as well as tropospheric delay correction based on an a-priori model (which yields about 90\% of reduction of the tropospheric delay error). The larger values for ionospheric and tropospheric delay may occur for slant ranges to satellites at low elevation.

Finally it is mentioned that a GNSS receiver, using electromagnetic signals received from the satellites,
determines the position of the antenna phase center (typically a point inside or slightly above the antenna)
as this is where the radio signals actually arrive.
Handling the so-called antenna Phase Center Offset (PCO) with respect to the bottom of the antenna, usually a cm to dm-effect,
is important in high-precision positioning discussed in the next section.

````{figure} ../../figures/GNSS/CTB3310surveymarker.jpg
---
name: CTB3310surveymarker
width: 40%
align: center
---
Survey-marker at TU Delft campus with accurate ground-truth coordinates: $X$ = 3923768.0147 m, $Y$ = 300255.7048 m, $Z$ = 5002640.2228 m (ITRF2014 at epoch 2021.50).
````

````{figure} ../../figures/GNSS/spp_scatter.png
---
name: spppos
width: 60%
align: center
---
Example of GNSS standalone positioning for a duration of 5000 seconds at a 5 second interval, on September 2nd, 2021, with measurements to about 25 GNSS satellites. At left: scatter of horizontal position error, at right: time series of vertical position error.
````

### Standalone positioning: example

With the equipment of {numref}`figure {number} <ublox>` a short experiment was carried out, lasting 5000 seconds. The antenna was installed on a survey-marker on the TU Delft campus, of which accurate position coordinates were already available, see {numref}`figure {number} <CTB3310surveymarker>`.
The receiver ran in so-called standalone positioning or single-point positioning mode,
and every 5th position solution was saved, hence the results shown in {numref}`figure {number} <spppos>` are obtained at a 5 second interval.

The graph at left shows the horizontal position scatter, North-coordinate versus East-coordinate, and the graph at right shows the vertical position (Up) as a function of time.
With the given coordinates of the marker, we actually present the position *error* in {numref}`figure {number} <spppos>`,
i.e., the difference of the measured position coordinate and the known ground-truth position coordinate. Hence, the origin of this graph refers to the 'true' position.
The position errors are expressed in a local topocentric coordinate system, in terms of local East, North and Up.

Table 2 presents the resulting empirical mean, standard deviation (std) and the root mean square (rms), see Chapter [Expectation (mean) and variance](meanvar) and Chapter 6 of Tiberius et al. (2022), of the position error in East, North and Up, showing a better than 1 meter accuracy of GNSS standalone positioning using over 25 GNSS satellites.

|            | East | North |  Up   |
|:-----------|:----:|:-----:|:-----:|
| mean \[m\] | 0.51 | 0.23  | -0.47 |
| std \[m\]  | 0.15 | 0.35  | 0.41  |
| rms \[m\]  | 0.53 | 0.42  | 0.62  |

## GNSS positioning modes

Several techniques have been developed to improve on the GNSS Standard Positioning Service (SPS) accuracy (standalone positioning, as discussed in the previous section).
Firstly, GNSS satellites broadcast signals on multiple frequencies, and sometimes even with multiple PRN codes per frequency, providing additional measurements.

Fortunately, even more accurate positioning modes are available, all relying on a kind of *augmentation*. This means that, next to the measurements collected by the user receiver, in addition measurements are used of a nearby permanent GNSS receiver, and/or that one relies in addition on data products derived from a network of permanent tracking stations. Such a network could provide precise estimates of the satellite positions for instance (more precise than what we by default encounter in the navigation message on the GNSS signal).

### Relative positioning, or DGNSS

Differential GNSS (DGNSS) uses a data link to a nearby base or reference station, i.e., another GNSS receiver at an accurately known position, and the *relative position* between the two is obtained. Measurement data from this base station are used, to reduce the effects of the atmospheric delays, satellite clock offsets and orbit errors. This can be achieved by differencing the observations from both receivers to the same satellites, which eliminates these (common) errors, which affect both receivers almost identically if the distance between them
is small enough, typically in the order of 5 to 10 km, considering that the satellites are at 20,000 km distance, see {numref}`figure {number} <dGNSS>`.

From the differenced observations, the so-called baseline (vector) between the two receivers can be computed through least squares estimation. The position of the rover is then obtained by adding the baseline vector to the accurately known coordinates of the reference station. Generally the term 'DGNSS' is used for relative positioning, though using only pseudorange measurements.

````{figure} ../../figures/GNSS/relativepositioning.png
---
name: dGNSS
width: 30%
align: center
---
Relative GNSS positioning combines measurements from a roving receiver with measurements from a reference (or base) station. The position of the rover is actually computed *relative* to the position of the base station. A number of errors, including atmospheric errors, is almost identical for two receivers in close proximity to each other. Hence, these errors cancel in relative positioning.
````

#### Real-Time Kinematic (RTK)

To obtain the highest possible accuracy from GNSS, it is no longer sufficient to use only the pseudorange code measurements, but rather the *carrier phase* measurements, introduced in Section *Ranging*, are required.
As mentioned before and illustrated in {numref}`figure {number} <ambiguity>` the measurement of fractional phase differences does pose the problem of the unknown initial number of carrier wave cycles, also called the carrier wave *ambiguities*, which need to be estimated together with the other unknown parameters. For relative positioning this is visualized in {numref}`figure {number} <ambiguouspositioning>`. Basically the range observed with carrier phase measurements is equal to the radius of one of the circles. Recall: the difference in radius of two circles is approximately 20 cm (one wavelength), the total distance more than 20,000 km! For both satellites (in reality more) we therefore have many options and hence there are many intersections to choose from. Resolving the ambiguities is a complex problem beyond the scope of this course. Important to remember is that if we can resolve the correct ambiguities, we benefit from the very high precision of the carrier phase measurements measurements. 

````{figure} ../../figures/GNSS/CPbasedpositioning.png
---
name: ambiguouspositioning
width: 40%
align: center
---
Geometric interpretation of relative positioning with carrier phase measurements, which are inherently *ambiguous*. The blue circle arcs, as possible solution for the rover receiver position result from the carrier phase measurement to the blue satellite, and the green circle arcs to those to the green satellite. The arcs are spaced by one wavelength $\lambda$ of the carrier wave -- we do not know which circle is the correct one, which is what we refer to as the 'ambiguity'.
````

Relative positioning, including resolving the ambiguities, is referred to as *Real-Time Kinematic (RTK)* positioning, or Carrier Phase based relative positioning (if performed in post processing). For more details see for instance Tiberius et al. (2022).


````{figure} ../../figures/GNSS/06GPSnetwork.png
---
name: 06GNSSnetwork
width: 50%
align: center
---
Example of network of permanent GNSS tracking stations, of a commercial network RTK service provider in the Netherlands, Belgium and Luxemburg. Image obtained with permission from [06-GPS](https://www.06-GPS.nl) (06-GPS)
````

The requirement for a nearby reference receiver is a disadvantage of RTK, considering effort and/or cost.
With RTK the coverage area of a reference receiver or station typically has a radius of ten, or tens of kilometers.
In many regions and countries, networks of reference stations, or Continuously Operating Reference Stations (CORS) have been deployed in order to cover the entire area, and in this scenario sometimes the term *network-RTK* is used, see {numref}`figure {number} <06GNSSnetwork>`, where reference stations generally have a 30-40 km inter-distance. An example of an application of RTK positioning in road construction is shown in {numref}`figure {number} <excavator>`.

````{figure} ../../figures/GNSS/excavator.png
---
name: excavator
width: 50%
align: center
---
Excavator in the process of constructing a motorway embankment. RTK-GNSS provides accurate real-time position information to guide this machine (note the two GNSS-antennas on the back of the engine). Image courtesy of [Heijmans](https://www.heijmans.nl/).
````

Many high-end GNSS receivers have RTK functionality built-in, but it can also be performed with professional software,
or even with open source software such as the RTKLIB program package (Takasu).



#### RTK --- carrier phase positioning: example

With the equipment of {numref}`figure {number} <ublox>` a short experiment was carried out, lasting 1000 seconds.
Using measurements from a permanent GNSS reference station (only 2 km away, see {numref}`figure {number} <skyplot>`),
received in real-time, the receiver provided so-called RTK-fixed solutions (in ETRF2000). For every epoch, i.e., once every second, a new position solution was computed, see the results in {numref}`figure {number} <rtkfix>`. The graph at left shows the horizontal position scatter, North-coordinate
versus East-coordinate, and the graph at right shows the vertical position (Up) as a function of time.

These measurements were taken at a survey-marker of which accurate position coordinates were already available, see {numref}`figure {number} <CTB3310surveymarker>`. That is how we can actually present the position *error* in the graph of {numref}`figure {number} <rtkfix>`, i.e., the difference of the measured position coordinate and the known ground-truth position coordinate. The position errors are expressed in a local topocentric coordinate system, in terms of local
East, North and Up, see Section 29.4 in Tiberius et al. (2022).

````{figure} ../../figures/GNSS/RTKfix_scatter.png
---
name: rtkfix
width: 60%
align: center
---
Example of Carrier Phase Real-Time Kinematic (RTK) positioning for a duration of 1000 seconds, on August 27th, 2021, with measurements of about 25 GNSS satellites, and successfully fixing the carrier phase ambiguities (RTK-fixed solution). At left: scatter of horizontal position error, at right: time series of vertical position error.
````

Table 3 presents the resulting empirical mean, standard deviation (std) and the root mean square error
(rms), see Chapter [Expectation (mean) and variance](meanvar) and Chapter 6 in Tiberius et al. (2022), confirming centimeter-accuracy of RTK-GNSS positioning.
This is an improvement by a factor of 100 compared to the standalone positioning results in {numref}`figure {number} <spppos>`.

|            |  East  | North  |   Up   |
|:-----------|:------:|:------:|:------:|
| mean \[m\] | 0.0016 | 0.0021 | 0.0068 |
| std \[m\]  | 0.0033 | 0.0039 | 0.0072 |
| rms \[m\]  | 0.0037 | 0.0044 | 0.0099 |


#### RTK --- carrier phase positioning: Digital Terrain Model (DTM)

Another short experiment was carried out to result in a centimeter-accurate 3D Digital Terrain Model (DTM)
of an embankment on the TU Delft campus, see {numref}`figure {number} <talud>`. The RTK survey of this bank of earth took only 15 minutes: walking with the GNSS-receiver in a grid-like pattern over this bank, and recording measurements every 1 second. 

````{figure} ../../figures/GNSS/talud.png
---
name: talud
width: 90%
align: center
---
Example of a centimeter-accurate 3D Digital Terrain Model (DTM) resulting from Carrier Phase Real-Time Kinematic (RTK) positioning. The DTM is presented in the national RD-NAP reference system (see Chapter 35 in Tiberius et al. (2022).
````

The RTK-fixed position solutions have been interpolated, and the resulting DTM is shown at right in {numref}`figure {number} <talud>`. With the DTM one can easily evaluate numerically the amount of earthwork needed to create or remove this bank, in this case 442 $\mathrm{m}^3$.

#### Precise Point Positioning (PPP)

In those instances where a nearby reference receiver (or network) is not available or cost-prohibitive,
Precise Point Positioning (PPP) is an attractive alternative.
PPP only relies on a *global* or regional, very sparse network of reference receivers, which
track the GNSS satellites and compute corrections to errors, in particular for the satellite orbits and clocks.

PPP suffers from a longer convergence period than RTK, think of several to tens of minutes before an accuracies at decimeter to centimeter level can be reached. 

### Concluding remarks on processing strategies

More GNSS processing strategies exist then treated here, see Tiberius et al. (2022) or Teunissen and Montenbruck (2017), but the most important ones for Earth, Climate & Technology are summarized below.

* Standard positioning: based on pseudorange measurement, without external corrections, accuracy of several meters (which will only significantly improve after a few hours if the receiver does not move).
* Differential GNSS: based on relative positioning with pseudoranges, decimeter-accuracy in a few minutes.
* Real-time Kinematic and Carrier Phase based relative positioning: relative positioning with carrier phase (and pseudorange) measurement, centimeter-accuracy in real-time.
* Precise Point Positioning: single-receiver positioning using corrections from a sparse network of reference receivers using carrier phase and pseudorange observations, centimeter- to decimater-accuracy with convergence times from several up to tens of minutes.

````{figure} ../../figures/GNSS/ubloxZED_F9P_NEW.JPG
---
name: ublox
width: 50%
align: center
---
At left: dual-frequency, multi-constellation GNSS receiver with receiver board at bottom, small patch-antenna (black) on top, and smartphone with Android positioning app at right; a total equipment cost of below 500 Euro (u-blox ZED-F9P), yet capable of providing cm-accurate RTK-GNSS positioning. At right: screenshot of SW Maps app by Softwel (P) Ltd.
````

High-accuracy positioning techniques, such as RTK and PPP, are nowadays implemented on small and low-cost devices. An example is shown in {numref}`figure {number} <ublox>`. The smartphone retrieves GNSS differential corrections (or measurements)
of a nearby reference station through an Internet-connection, and forwards these to the GNSS receiver, which is connected
via USB to the smartphone. The firmware on the GNSS receiver chip combines the corrections with the measurements of the rover receiver, and delivers a centimeter accurate RTK-position solution, which it relays back to the app on the smartphone.
This allows for centimeter accurate navigation, in real-time, with your smartphone in combination with the separate small receiver.

As already hinted at, the GNSS position accuracy improves when the measurement time duration increases. One important factor here is the *dynamic model* of the receiver motion, or how the measurement epochs can be 'linked' to each other.
If the receiver is stationary, the improvement will be most notable, as we can basically estimate a single position from many measurements (a *static* solution). 

For a moving receiver the accuracy can also improve over time, if we can exploit the fact that some of the other parameters are constants, e.g., the ambiguities, or, if the movement can be constrained or predicted to some extent based on the current position (e.g., a car driving along a straight line, at constant velocity). 

In a *kinematic* solution, position coordinates are computed for each measurement instant (for instance every 1 second), to accomodate the fact that the receiver is/was actually moving during the survey. As a result one then obtains a *list* of position estimates, e.g., one every second, instead of one overall position solution as with a static survey. The list describes the *track* or *trajectory* of the moving receiver.

Two related issues are:

1. The difference between *real-time* processing, and *post-processing* (for instance after whole survey has been completed), where post-processed results are generally more accurate, but obviously not available right on the spot, and hence not suitable for certain applications.
2. The measurement rate of the receiver: GNSS receivers often take measurements
once every second (1 Hz) or at 10-20 Hz. Technically up to a 100 Hz measurement
rate is possible. To reduce the computational burden, data storage, and power requirement, lower measurement rates (e.g. once per 30 seconds) are common in applications where objects move only very slowly, like in geoscience on measuring tectonic plate motion.

The impact of the measurement rate on the position accuracy is marginal (a higher data rate can slightly improve precision), because the measurement errors are generally correlated in time. This means that measurements taken in quick succession are not independent, and thereby do not offer, precision-wise, a lot of new/additional information.

Factors that improve the accuracy of GNSS positioning are better and more signals and pseudo random noise codes, as well as more satellites, which is especially favourable in environments where signals may be blocked (open pit mines, urban areas).


### GNSS applications

There are many different applications of GNSS positioning each with its own requirements and, related to that, a preferred processing strategy.

* Surveying for creating maps and construction works, requires cm to mm position accuracy and will use RTK if available, or PPP otherwise, see {numref}`Figures {number} <talud>` and {numref}`{number} <waterscooter>`.
* Deformation monitoring, due to Earthquakes, volcanic activity, mining or injection / extraction of groundwater and other resources, as well as any number of scientific applications require the highest possible accuracy and use carrier phase based positioning.
* Machine guidance, as shown in {numref}`figure {number} <excavator>` and (semi-)autonomous navigation require high accuracy and reliability; this can be achieved by using RTK / Carrier Phase based relative positioning and PPP. This is for applications in applications in remote sensing, mining, agriculture, offshore operations (e.g., when constructing wind farm at sea), etcetera.
* Smartphones, car navigation, and personal navigation usually have the lowest requirements, and the GPS (GNSS) standard positioning service suffices.


````{figure} ../../figures/GNSS/Zandmotor.png
---
name: waterscooter
width: 90%
align: center
---
Both the on- and offshore part are regularly surveyed, to monitor the development of the Zandmotor (The Sand Engine), at the Dutch North-Sea coast, near Ter Heijde. This ‘building with nature’ project started in 2011, and at bottom an aerial photo of the Zandmotor is shown, looking in Southern direction. High-precision RTK-GNSS is used for positioning the quad on shore, and the jet-ski in the water (note the GNSS-antenna at the back of the jet-ski, in the inset). The measurements by the quad result in a Digital Terrain Model (DTM), and echo sounder depth measurements by the jet-ski result in a seafloor-map. Photo at top by Matthieu de Schipper de Schipper [n.d.]. Photo at bottom by Pmblom - own work, May 2016, taken from Wikimedia Commons Wikimedia Commons [n.d.] under CC BY-SA 4.0 license.
````

There is also a number of GNSS applications, in which the position solution is not the (primary) goal. Accurate time which is obtained through determining also the receiver clock offset $b_r$, is used in timing applications. The standard positioning service allows for timing at the 10-100 ns level, and this is used for instance in telecommunication, see {numref}`figure {number} <KPNtelecommast>`, electrical power grids, and financial networks.


````{figure} ../../figures/GNSS/KPNmastZvbh.jpg
---
name: KPNtelecommast
width: 40%
align: center
---
GNSS receivers are commonly used to synchronize base stations for telecommunication. Requirements on time ­synchronization for this application lie in the order of $\mu s$. The photo shows a base station with an height of 37 m.
````

Nuisance parameters such as the atmospheric delays can also be used as observational input for instance to determine the state of the Earth's ionosphere, or derive troposphere delays, for instance as input for Numerical Weather Prediction (NWP).

GNSS radio signals can also be used outside of their intended purpose, e.g., to determine sea-level height by measuring reflected GNSS signals from orbit.

### Resources

This part provides an introduction to positioning with GNSS/GNSS. For a lot more of technical and mathematical modeling information
on GNSS and GNSS positioning, navigation and timing, the reader is referred to Teunissen and Montenbruck [2017] and Morton et al. [2021]. These textbooks also cover a wide
range of applications.

The first source of information on GNSS, as well as the point of contact is the [Navigation Center of the US Coast Guard](http://www.navcen.uscg.gov/)(United States Coast Guard).
Official U.S. government information about GNSS is available through (https://www.GNSS.gov/) (US Government).

The first source of information on Galileo and point of contact is the European Union Agency for the Space Programme ([EUSPA](https://www.euspa.europa.eu/)).

The [IGS](https://igs.org/) is the International GNSS Service, a voluntary federation of universities and research institutions, operating permanent GNSS stations worldwide,
and providing GNSS data and products for high(est)-precision applications (IGS).

### Exercises

This section presents a couple of questions and problems on GNSS positioning. Answers are at the end of the Chapter.

**Question 1** What are the largest remaining error sources in short-baseline DGNSS, explain your answer.

**Question 2** If a certain application requires decimeter positioning accuracy, which GNSS positioning modes can be considered?
And for how long a time would we need to collect measurements?

**Question 3** The principle of GNSS satellite positioning and navigation consists of determining the range
from satellite to receiver through measurement of the signal travel time. When the receiver clock is ahead of time by 0.1 $\mu$s, by how much is the measured range to the satellite too long or too short due to this clock error?


````{figure} ../../figures/GNSS/1D_GPSpositioning.png
---
name: 1D_GNSSpositioning
width: 60%
align: center
---
One-dimensional GNSS positioning (Question 4).
````

**Question 4** Let's simplify the GNSS positioning problem to a single dimension. There are two satellites A and B,
and the user receiver is at R, see {numref}`figure {number} <1D_GNSSpositioning>`. The positions of the satellites are known, A is at $x_A=0$, and B is at $x_B=10$.
The position of the user $x_R$ is unknown. Two pseudoranges have been measured: $p_{AR} = 9$ and $p_{BR} = 7$.
Determine the position (coordinate) of the user at R.

**Question 5** The GNSS relative positioning problem has been simplified to a single dimension. There is one satellite 'sat' (or just 's')
and it is visible at the local horizon. The receivers '1' and '2', and the satellite are all on a straight line (along the x-coordinate axis),
see {numref}`figure {number} <singledifference>`. The radio signals from the satellite to the two receivers pass through the Earth's atmosphere (layer 'atm')
and get thereby delayed; the delay, expressed in units of range, is denoted by $d^s$. This delay is unknown (but *equal* for the signals to both receivers).
The satellite position is known, $x^{s} = -20$, and the position of receiver 1 as well $x_1 = 5$. Compute the position of receiver 2, $x_2$,
based on the pseudorange measurements $p_{1}^{s} = 32$ and $p_{2}^{s} = 37$.
In this case, you can again assume that all clocks run perfectly on time – there are no clock offsets involved.

````{figure} ../../figures/GNSS/singledifference.png
---
name: singledifference
width: 60%
align: center
---
Relative positioning in one dimension (Question 5).
````

### Solutions

```{admonition} Answer 1
:class: tip, dropdown
 The atmosphere delays as well as the satellite orbit and clock errors are eliminated in DGNSS, see {numref}`figure {number} <dGNSS>`, which leaves multipath and (pseudorange) measurement noise as the largest error sources,
see {numref}`figure {number} <signalpath>` and Table 1.
```

```{admonition} Answer 2
:class: tip, dropdown
Real-Time Kinematic (RTK) provides decimeter or even centimeter accuracy as soon as the ambiguities can be
fixed, which generally is (well) within 100 seconds of measurements, and even faster in post-processing.
PPP can also provide decimeter accuracy after several minutes. DGNSS can reach decimeter accuracy as
well, but may considerable time to allow for averaging (with static positioning only), for instance one hour.
Standalone GNSS often does not reach decimeter accuracy even after one or several days (averaging with static positioning).
```


```{admonition} Answer 3
:class: tip, dropdown
When the receiver clock is ahead of time, the clock error $\delta t_{r}$ is positive, hence $t_{r} > t$. Next, we know that $c \delta t_{r}\approx 3\times 10^8\cdot 0.1\times 10^{-6} = b_r = 30$ m, we find that
the pseudorange $p_{r}^{s}$ is too long by 30 m compared to the actual distance $l_{r}^{s}$.
```

```{admonition} Answer 4
:class: tip, dropdown
 Looking at {numref}`figure {number} <1D_GNSSpositioning>` we identify two geometric ranges, namely $l_{AR} = x_R - x_A$
and $l_{BR} = x_B - x_R$ (mind to define these distances to be positive). Then we can formulate two observation equations:

$$
\begin{align*} p_{AR} & = & l_{AR} + b_R \\
p_{BR} & = & l_{BR} + b_R    \end{align*}
$$

which gives

$$
\begin{align*} p_{AR} & = & x_R - x_A + b_R \\
p_{BR} & = & x_B - x_R + b_R    \end{align*}
$$

and with the given satellite positions, we obtain

$$
\begin{align*} p_{AR} + x_A & = & x_R + b_R \\
p_{BR} - x_B & = & - x_R + b_R    \end{align*}
$$

We have two equations with two unknown parameters, namely $x_R$ and $b_R$, which we can solve, giving $x_R = 6$ and $b_R = 3$.
The user position coordinate equals $x_R = 6$, and we are typically not interested in the receiver clock offset.
It is easily verified that correcting the measured pseudoranges for the receiver clock offset yield the actual distances
from the two satellites to the receiver: $p_{AR} - b_R = 9-3=6$ and $p_{BR} - b_R = 7-3=4$.
```

```{admonition} Answer 5
:class: tip, dropdown
The pseudorange observation equation needs to be adapted. There is no clock offset involved at all,
so parameter $b_r$ cancels, but now, we face an unknown atmospheric delay $d^s$. Hence

$$
\begin{align*} p_{1}^{s} & = & l_{1}^{s} + d^s \\
p_{2}^{s} & = & l_{2}^{s} + d^s    \end{align*}
$$

Looking at {numref}`figure {number} <singledifference>` we identify two geometric ranges, namely $l_{1}^{s} = x_1 - x^s$ and $l_{2}^{s} = x_2 - x^s$ (mind to define these distances to be positive). Then the two observation equations become:

$$
\begin{align*} p_{1}^{s} & = & x_1 - x^s + d^s \\
p_{2}^{s} & = & x_2 - x^s + d^s    \end{align*}
$$

where there are two unknown parameters, namely $x_2$ and $d^s$. With the given measurements and coordinates, this is easily solved, to
yield $x_2 = 10$ and $d^s = 7$. Alternatively one could take the difference of the two pseudorange measurements
$p_{2}^{s} - p_{1}^{s} = x_2 - x_1$, which gives an identical result for $x_2$, and one is generally not interested in parameter $d^s$.
```


## References

06-GPS. Image of network of permanent GNSS tracking stations in the Netherlands, Belgium and Luxemburg. Sliedrecht, The Netherlands, 2021. URL https://www.06-GPS.nl/.
24

Boeing. Image of GNSS block IIF satellite. Chicago, Illinois, n.d. URL https://www.boeing.com/space/global-positioning-system/.

M. de Schipper. Photo of RTK-GNSS positioning with a quad on shore, and a jet-ski in the water, at the Zandmotor, n.d.

European GNSS Agency. GSA GNSS market report. Technical report, European Union Agency for the Space Programme (EUSPA), 2019. URL https://www.euspa.europa.eu/.
European Union Agency for the Space Program (EUSPA). European Union Agency for the Space Programme (EUSPA), n.d. URL https://www.euspa.europa.eu/. website.

Heijmans N.V. Photo of excavator in the process of constructing a motorway embankment, guided by RTKGNSS. Rosmalen, The Netherlands, n.d. URL https://www.heijmans.nl/.

International GNSS Service (IGS). International GNSS Service (IGS), n.d. URL https://igs.org/. website.

J. Morton, F. van Diggelen, J. Spilker, and B. Parkinson, editors. Position, Navigation, and Timing Technologies in the 21st Century: Integrated Satellite Navigation, Sensor Systems, and Civil Applications, Volume 1 and 2. Wiley - IEEE Press, 2021. doi: http://dx.doi.org/10.1002/9781119458449.

A. Smits. Visualization of GNSS positioning, n.d. Delft University of Technology.

T. Takasu. RTKLIB: An Open Source Program Package for GNSS Positioning, n.d. URL http://www.
rtklib.com/. website.

P. Teunissen and O. Montenbruck, editors. Springer handbook of Global Navigation Satellite Systems. Springer
Handbooks. Springer Verlag, 2017. doi: http://dx.doi.org/10.1007/978-3-319-42928-1.

C. Tiberius, H. van der Marel, R. Reudink, and F. van Leijen. Surveying and Mapping. TU Delft OPEN Books, Nov. 2022. doi: 10.5074/T.2021.007. URL https://books.open.tudelft.nl/home/catalog/book/163.

United States Coast Guard. Navigation Center, n.d. URL https://www.navcen.uscg.gov/. website of the United States Coast Guard (USCG), U.S. Department of Homeland Security, Navigation Center. U.S. government. 

Official U.S. government information about the Global Positioning System (GNSS) and
related topics, n.d. URL https://www.GNSS.gov/. GNSS.gov website.

Wikimedia Commons. Wikimedia Commons, n.d. URL https://commons.wikimedia.org/. media file repository, for public domain and freely licensed educational media content.