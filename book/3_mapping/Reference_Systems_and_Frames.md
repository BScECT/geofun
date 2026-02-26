# Coordinate Reference Systems

Coordinate Reference Systems (CRSs) allow us to describe, record, and
compare the position, motion, and relationships of points or objects.
The need to do so is widespread. Astronomers, for example, require a CRS
to locate stars, galaxies, and other celestial objects in the sky.
Engineers use CRSs in the design and construction of infrastructure,
mechanical components, and structures. In robotics, CRSs are essential
for controlling robot motion and enabling interaction with the
environment. In computer graphics, CRSs play a key role in animating
objects, generating 3D models, and displaying images. These are just a
few examples.

In the field of Earth, Climate and Technology (EC&T), CRSs are also used
extensively. In most cases they provide the spatial reference that is a
defining characteristic of geodata. This alone makes it essential for
EC&T engineers and scientists to have a basic understanding of CRSs, how
they are defined and realized in practice, and how to transform
coordinates between different CRSs. The importance of this knowledge and
these skills is further reinforced by:

1.  **The sheer number of CRSs in use.** There are over 10,000 CRSs
    (<https://epsg.io/>), although most can be traced back to a few
    basic types. Any attempt to combine or compare geodatasets requires
    them to be represented in the same CRS.

2.  **The role of CRSs in analysis.** Certain operations or analyses can
    be made much simpler—or more accurate—by transforming data into a
    different CRS. For example, calculating distances between points is
    considerably easier on a plane than on a reference ellipsoid.

3.  **The CRS in which the measurements are collected is typically not
    the target CRS.** Measurements are often collected in a CRS tied to
    the sensor itself. As noted above, once these measurements need to
    be integrated with other datasets, they must be transformed into
    another CRS. This may involve a chain of transformations. For
    instance, when acquiring imagery from a satellite, a series of steps
    is required to transform pixel coordinates into a CRS that is
    referenced to the Earth.

In this chapter, we will focus on the CRSs used to describe positions of
points / objects on or near the Earth’s surface. CRSs used to describe
Earth’s rotation or satellite orbits will *not* be considered here. The
chapter begins with an introduction to coordinate systems, vertical
coordinate systems, datums and frames, and map projections. Thereafter,
we will explore different types of CRSs in more detail and discuss some
of the most important examples. Finally, we will then introduce datum
transformations.

This chapter is limited to *spatial* CRSs. In certain sub-disciplines
within EC&T—such as the atmospheric sciences and
oceanography—three-dimensional systems are employed in which horizontal
position is combined with a non-spatial parameter or function that is
treated as a coordinate. The relationship between this parameter and
spatial dimensions is usually non-linear. Latitude, longitude, and
pressure is a commonly encountered example. These spatial reference
systems are referred to as *parametric* CRSs.

The terminology adopted here follows, as closely as possible, the
definitions of the International Organization for Standardization (ISO)
19111 *Referencing by coordinates* (ISO, 2019).

The material presented in this chapter is largely based on three key
references; these are Iliffe and Lott (2008), Tiberius et al. (2022),
and Hofmann-Wellenhof & Moritz (2006).

## Coordinate Systems

A coordinate system is an *arrangement of reference lines or curves used
to identify the location of points in space* (British Encyclopaedia,
[https://www.britannica.com/science/coordinate-system)](https://www.britannica.com/science/coordinate-system).
To identify the location, we use numbers (i.e., coordinates)
representing things like distances or angles (see Fig. 1). The number of
coordinates needed to uniquely describe the position is determined by
the dimension of the space; i.e., the number of axes associated with the
system. In the three-dimensional space, we need three coordinates to
describe the position of any point *P*.

Include interactive figures 2.4.1 and 2.4.6 from Baker & Haynes (2020,
Chapter 2)
<https://github.com/dantheboatman/EngineeringStatics/blob/master/source/ptx/Chapter_02.ptx>

**Fig. 1:** Rectangular (a) and spherical coordinates (b).

For each axis of a coordinate system it is necessary to define certain
attributes (Iliffe and Lott, 2008):

- Name and/or abbreviation for the axis.

- The sequence of the axes. Coordinates are listed in this order.

- The direction in which coordinates increment along the axis.

- The units for measurements on the axis.

If any of the attributes are changed, then the coordinate system is
changed.

Many different coordinate systems exists (e.g., Neutsch, 2011). A
comprehensive introduction to all of them is therefore not feasible.
However, it is also unnecessary; for the purpose for which we need them,
we can limit ourselves to a small subset. These include the 2D/3D
Cartesian, the spherical, and the ellipsoidal coordinate systems. All of
these are so-called orthogonal coordinate systems, meaning that the
coordinate directions are all perpendicular and, therefore, independent.
The Cartesian coordinate systems are, however, *rectangular* coordinate
systems; i.e., the axes are pair-wise perpendicular and intersect at the
origin. The spherical and ellipsoidal coordinate systems are both
examples of so-called *curvilinear* coordinate systems; i.e., the
coordinate axes are curved. In the following subsections, we introduce
the 3D Cartesian, spherical, and ellipsoidal coordinate systems.

### **3D Cartesian Coordinate Systems**

3D Cartesian coordinate systems can be considered a straightforward
extension of 2D Cartesian coordinate systems by adding a third axis.
Each coordinate of a point *P*, is the signed distance from *P* to the
plane defined by the other two axes (see {numref}`refsys2`). The sign is determined
by the orientation of the corresponding axis. Together, the coordinates
form a triplet that is typically denoted as *X,Y,Z*.


````{figure} ../figures/part-a_refsys2.png
---
name: refsys2
width: 30%
align: center
---
The 3D Cartesian coordinate system.
````

Although the positive and negative directions of the axes are arbitrary,
we typically use so-called *right-handed* coordinate systems. That is,
if the thumb of your right hand points in the positive direction of the
Z-axis and your forefinger in the positive direction of the X-axis, your
middle finger, extended at right angles to your thumb and forefinger
points in the positive direction of the Y-axis.

To define a 3D Cartesian coordinate system, we need to:

1\) fix the location of the origin;

2\) define the direction of two of the axes;

3\) define the unit of length, referred to as the scale.

### **Spherical Coordinate Systems**

A point *P* in space can also be described using spherical coordinates
(*ψ, λ, r*), where *ψ* is the angle of the position vector (vector from
the origin to *P*) with the XY-plane, λ is the angle between the X-axis
and the projection of the position vector onto the XY-plane, and *r* is
the length of the position vector (see Fig. 1b). *ψ, λ,* and *r* are
referred to as, respectively, the geocentric latitude, the longitude,
and the geocentric radius. The relationship between Cartesian and
spherical coordinates is given by:

$$
\begin{aligned}
X &= r\cos\psi\cos\lambda \\
Y &= r\cos\psi\sin\lambda \\
Z &= r\sin\psi
\end{aligned}
$$

The inverse relationship is given by:

$$
\begin{aligned}
\psi &= \arctan\left( \frac{Z}{\sqrt{X^{2} + Y^{2}}} \right) \\
\lambda &= \arctan\left( \frac{Y}{X} \right) \\
r &= \sqrt{X^{2} + Y^{2} + Z^{2}}
\end{aligned}
$$

### **Ellipsoidal Coordinate Systems**

In an ellipsoidal coordinate system, we locate a point relative to an
ellipsoid (of revolution) — the 3D surface formed by rotating an ellipse
about its minor axis. In doing so, we use the geographic (or geodetic)
latitude *φ*, longitude *λ*, and height *h* (See {numref}`refsys3`). *φ* is the
angle measured in the meridian plane between the equatorial plane and
the surface normal and *λ* is the angle measured in the equatorial plane
between the zero meridian (X-axis) and the meridian plane of *P*. Here,
*φ* is positive northwards and negative southwards and *λ* is positive
as reckoned towards the east. The height *h* represents the distance
between *P* and the ellipsoid measured along the ellipsoid’s normal
(i.e., the line perpendicular to its surface).

````{figure} ../figures/part-a_refsys3.png
---
name: refsys3
width: 40%
align: center
---
Ellipsoidal and Cartesian coordinates. The ellipsoidal latitude φ is also known as geodetic or geographic latitude. The ellipsoidal coordinates φ and λ are also called geographic coordinates (Tiberius et al., 2022, Fig. 29.2).
````

The shape of an ellipsoid is defined by two parameters. The first is the
semi-major axis or the equatorial radius *a*. The other parameter is
either the semi-minor axis (or polar radius), *b*, or the flattening,
*f*, or the eccentricity, *e*. They are related by:

$$ f = \frac{a - b}{a},e^{2} = 2f - f^{2} = \frac{a^{2} - b^{2}}{a^{2}},b = a(1 - f) = a\sqrt{1 - e^{2}}$$ .

The relationship between Cartesian and geographic coordinates is given
by:

$$
\begin{aligned}
X &= \left( \overline{N} + h \right)\cos\varphi\cos\lambda \\
Y &= \left( \overline{N} + h \right)\cos\varphi\sin\lambda \\
Z &= \left( \overline{N}\left( 1 - e^{2} \right) + h \right \sin\varphi
\end{aligned}
$$

whereas the inverse relationship is given by the iterative formula:

$$
\begin{aligned}
\varphi &= \arctan\left( \frac{Z + e^{2}\overline{N}\sin\varphi}{\sqrt{X^{2} + Y^{2}}} \right) (iterate four times, start with \overline{N}\sin\varphi = Z) \\
\lambda &= \arctan\left( \frac{Y}{X} \right) \\
h &= \frac{\sqrt{X^{2} + Y^{2}}}{\cos\varphi} - \overline{N}
\end{aligned}
$$

$\overline{N}$, referred to in both equations, is the radius of
curvature in the *prime vertical normal section* (see {numref}`refsys4`). That is,
it is the distance between the surface of the ellipsoid and the polar
axis measured along the line normal to the surface of the ellipsoid that
goes through *P*. The prime vertical normal section is the curve formed
by the intersection of the normal plane—a plane passing through the
ellipsoid’s surface normal at a given point—and the surface of the
ellipsoid, which has the minimum curvature. This section is oriented in
the east–west direction and is one of the two principal normal sections.
The other is the meridian normal section, which is perpendicular to the
prime vertical section (i.e., it lies in the north–south direction) and
has maximum curvature. Its radius of curvature is referred to as
$\overline{M}$. Both radii of curvature increase toward the poles (see {numref}`refsys5`). Their equations are:

$$
\begin{aligned}
\overline{N}(\varphi) $= \frac{a}{\sqrt{1 - e^{2}\sin^{2}\varphi}} \\
\overline{M}(\varphi) $= \frac{a\left( 1 - e^{2} \right)}{\left( 1 - e^{2}\sin^{2}\varphi \right)^{\frac{3}{2}}}
\end{aligned}
$$

````{figure} ../figures/part-a_refsys4.png
---
name: refsys4
width: 40%
align: center
---
Ellipsoidal, geodetic or geographic latitude φ, geocentric (or spherical) latitude ψ, radius of curvature formularadius r, ellipsoidal height h, semi-major axis a and semi-minor axis b of the ellipsoid. The dashed line shows the local tangent plane to the ellipsoid. (Tiberius et al., 2022, Fig. 29.3).
````

````{figure} ../figures/part-a_refsys5.png
---
name: refsys5
width: 40%
align: center
---
Radius of curvature formulaand formulaas function of latitude φ. The dashed lines represent the semi-major axis a and semi-minor axis b. (Tiberius et al., 2022, Fig. 29.4).
````

## Height Coordinate Systems

The coordinate systems introduced in Sect. 2 allow us to describe
positions in three-dimensional space. However, none of them are suitable
for expressing vertical positions, whether heights on land or depths at
sea. For heights on land, this limitation is related to how we define
*horizontal* and *vertical* with respect to the physical Earth.

If two points have the same vertical position, we would expect the line
connecting them to be a horizontal one—in other words, level. Imagine
the two points were chosen within a body of water: in the absence of
driving forces such as wind, we would expect no water to flow between
them. If the vertical positions were expressed, for example, with
respect to a reference ellipsoid (i.e., the points had the same
ellipsoidal height), this would *not* necessarily be the case, since
whether or not water flows between two points is determined by gravity.

Our notion of vertical is also governed by gravity. Indeed, we expect
the height of a falling object above the ground to equal the distance it
travels before hitting the surface.

Both notions illustrate that, unlike horizontal positions, vertical
positions (heights) cannot be defined purely geometrically: they must be
tied to the Earth’s gravity field. In this section, we will briefly
discuss the underlying theory and explain why this relationship leads to
different ways of expressing height.

For completeness, we note that for depths at sea different
considerations apply: here so-called *tidal datums*—vertical reference
surfaces associated with a particular phase of the tide—are commonly
used. These fall outside the scope of this section, which is restricted
to height coordinate systems commonly used to express heights on land.

### Level Surfaces and Earth’s Gravity Potential

A truly horizontal surface, also called a level surface, is an
equipotential surface of the Earth’s gravity field. That is, a surface
on which the gravity potential (denoted by *W*, with units of
m<sup>2</sup>/s<sup>2</sup>) is constant.

In physics, *potential refers to the capacity to do work or to cause
change*. The gravity potential at a point can therefore be thought of as
a measure of how much potential energy a unit mass would have due to
Earth’s gravity at that location. In simple terms, it tells us how
“deep” or “high” that point lies in Earth’s gravitational field. If two
points have the same gravity potential, no work is needed to move a
small mass from one point to the other. However, moving a mass from a
lower to a higher potential requires work against gravity.

The gravity potential of the Earth, *W,* is the sum of the gravitational
potential (*V*) and the centrifugal potential (*Φ*), both of which are
*scalar* potentials. The key property of a scalar potential field is
that the difference in potential energy of an object between two
positions depends only on the positions themselves, not on the path
taken between them.

The gravitational potential *V* at a point *P* represents the work done
by gravitation to move a unit mass from infinity (where *V*=0) to the
point *P*. As such, *V* is negative. **In geodesy, however, the negative
sign is omitted.** Following this convention, for a point mass *V=Gm/l*,
where *G* is Newton’s gravitational constant (6.67428 ± 0.00067 ×
10<sup>-11</sup> m<sup>3</sup> kg<sup>-1</sup> s<sup>-2</sup> ), *m* is
the attracting mass, and *l* is the distance between *P* and *m*. For
the Earth—being a three-dimensional body with volume *v* and variable
density *ρ*—the expression for *V* becomes:

$$
V\left( X_{P},Y_{P},Z_{P} \right) = G\iiint_{v}^{}\frac{\rho(\xi,\eta,\zeta)}{l}d\xi d\eta d\zeta,
$$

where the coordinates of the attracted point *P* are given by
*X*<sub>P</sub>*, Y*<sub>P</sub>*, Z*<sub>P</sub> and that of the mass
element *m* by *ξ, η, ζ*.

The centrifugal potential arises from the fact that the Earth rotates
about its own axis. In a Cartesian coordinate system co-rotating with
the Earth and with its origin at the Earth’s centre, the potential is
given by
$\Phi = \frac{1}{2}\omega^{2}\left( X_{P}^{2} + Y_{P}^{2} \right).$Here,
*ω* is the angular velocity of the Earth’s rotation and
(*X*<sub>*P*</sub><sup>2</sup> + *Y*<sub>*P*</sub><sup>2</sup>)
represents the squared distance from the polar axis to the point *P*.

### Plumb Lines and Gravity

Gravity potential *W* and gravity are closely related. The gravity
vector **g** is the gradient of the scalar potential *W*. The vector
**g** represents the total force (gravitational plus centrifugal) acting
on a unit mass.

The differential of *W (dW)* can be written as the scalar product of the
two vectors **g** and *d***x**=\[*dx,dy,dz*\], that is,

*dW* = **g**·*d***x**

If *d***x** is taken along an equipotential surface where *W*=constant,
the potential remains constant and *dW=0*, from which it follows that
**g·***d***x**=0. Since the scalar product of two vectors equals zero
only when they are perpendicular, it follows that *the gravity vector is
orthogonal to the equipotential surface passing through the same point*.

The direction of the gravity vector at a given point defines the
direction of the *plumb line*, or the vertical at that point.
Equivalently, the gravity vector at any point is tangent to the plumb
line at that location. Plumb lines intersect all equipotential surfaces
orthogonally. The path followed by a freely falling object is described
by the plumb line. Therefore, heights and height differences are
naturally expressed as distances measured along the plumb line.

Heights defined along the plumb line are known as *orthometric heights*
(denoted *H*, see {numref}`refsys6a`). The distances are taken with respect to an
equipotential surface that is defined as the reference surface, referred
to as the *geoid*. The gravity potential of the geoid is denoted as
*W<sub>0</sub>*.

If the vector *d***x** is taken along the plumb line, in the direction
of increasing height *H*, then its length is ∥*d***x**∥ = *dH*, and its
direction is opposite to that of the gravity vector **g**, which points
downward. Hence, the angle between *d***x** and **g** is 180°. Using the
definition of the scalar product (for two vectors **a** and **b**, it is
defined as **a**⋅**b**=∥**a**∥∥**b**∥ cos *α*, where *α* is the angle
between them), we obtain

**g** · *d***x** = *g* *dH* cos 180° = *−g dH*.

From this, we find (see first equation of this section):

*dW = −g dH*,

which relates the orthometric height *H* to the potential *W*.

The previous equation can also be written as

*g= - ∂W/∂H*,

which shows that gravity is the negative vertical gradient of the potential *W*.

### Heights

For a spherical, non-rotating Earth with a radially symmetric mass
distribution (i.e., one that depends only on the distance to the Earth’s
centre), the gravity vectors would everywhere point toward the Earth’s
centre, while their magnitude would depend solely on altitude. The
equipotential surfaces of the gravity field associated with such an
Earth would be concentric spheres, and the geometric separation between
any two equipotential surfaces would be constant. Thus, in such a model
Earth, there is no discrepancy between the geometric and physical
interpretations of heights and height differences.

The real Earth, however, satisfies none of these conditions. First, the
Earth rotates about its own axis, which results in a latitude-dependent
centrifugal acceleration directed outward from the rotational axis and
forming part of the gravity measured at the Earth’s surface. The
centrifugal force due to rotation also causes the Earth to flatten at
the poles and bulge at the equator, so that its shape is no longer well
approximated by a sphere but rather by an ellipsoid of revolution. This
deformation further affects the gravity measured at the surface: the
closer one is to the equator, the farther one is from the Earth’s
centre, and therefore the smaller the magnitude of the gravitational
acceleration.

On regional and local scales, topography introduces additional
disturbances in the gravity field, affecting both its magnitude and
direction. The same applies to variations in the Earth’s internal mass
distribution caused by different materials and deeper tectonic
structures. All these factors leave their imprint on the Earth’s gravity
field.

Equipotential surfaces of the Earth’s gravity field therefore have a
complex shape and are not parallel to one another. Because *W* is
analytic outside the Earth, level surfaces that lie entirely outside the
Earth are analytic surfaces, although they lack simple analytical
expressions. This is not true for level surfaces that lie partly or
completely within the Earth. These surfaces are continuous and smooth
(i.e., without edges), but they are no longer analytic; the curvature of
interior level surfaces changes discontinuously with the density.

Given our expectation that two points of equal height should lie in the
same level surface, it follows from the above that *this does not hold
for orthometric heights*. In other words, two points with the same
gravity potential in general do not have the same geometric distance
(measured along the plumb line) to the equipotential surface used as the
reference. *Rather than expressing vertical position as a length, we
should therefore express it as a difference in potential*. The quantity
used for this purpose is the *geopotential number* C, defined as


$$
C = W_{0} - W_{P} = \int_{0}^{H}gdH = H\frac{1}{H}\int_{0}^{H}gdH = H\overline{g},
$$

where $\overline{g}$ is the mean value of the gravity along the plumb line
between the geoid and the surface point *P*. The geopotential number *C*
is measured in geopotential units (g.p.u.), where 1 g.p.u. = 1 kgal m =
1000 gal m, and note that 1 gal = 10<sup>−2</sup> m s<sup>−2</sup>.

Expressing vertical positions by potential differences, however, does
not meet practical needs. For this reason, several alternative height
coordinate systems have been defined, in which height can be expressed
in the general form

Height =$\frac{C}{G_{0}}.$

These height systems differ according to the choice of the gravity value
*G<sub>0</sub>* in the denominator. The principal systems are:

- **dynamic height** – where *G<sub>0\ </sub>*= *γ<sub>0\ </sub>*=
  constant,

- **orthometric height (*H*)** – where *G<sub>0\ </sub>*=$\overline{g}$,

- **normal height (*H<sup>N</sup>***)– where
  *G<sub>0\ </sub>*=$\overline{\gamma}$,

In the case of normal heights, the Earth’s gravity field is replaced by
the gravity field of a reference ellipsoid (which can be computed
analytically) and heights are measured along the ellipsoidal normal (see
Fig. {numref}`refsys6b`). Without going into further details, normal heights can be
interpreted as heights with respect to the quasi-geoid. In areas with
moderate to little topography, the differences between the geoid and
quasi-geoid as well as the differences between orthometric and normal
heights are small (mm-cm). In mountainous regions, the differences can
reach multiple meters (Foroughi and Tenzer, 2017). *The key advantage of
the normal height system versus the orthometric height system is that
the first does not require any information about the Earth’s density
distribution*. The advantages and disadvantages of the different systems
are summarised in Table 1.1.

````{figure} ../figures/part-a_refsys6a.png
---
name: refsys6a
width: 40%
align: center
---
The orthometric height HO: the curved-line distance measured along the plumb line from the point P0 on the geoid to the point of interest P on the Earth’s surface. The geoid height N: the straight-line distance measured along the ellipsoidal surface normal from the point Q0 on the ellipsoid to the point P0 on the geoid. (Note: the curvature of the equipotential surfaces and plumb lines is exaggerated for illustrative purposes). Adapted from Featherstone & Kuhn (2006), Fig. 2. |
````

````{figure} ../figures/part-a_refsys6b.png
---
name: refsys6b
width: 40%
align: center
---
The normal height HN: the curved-line distance measured along the normal gravity plumb line from the point on the reference ellipsoid to the point Q on the telluroid. The quasi-geoid height: the straight-line distance measured along the ellipsoidal surface normal from formulaon the ellipsoid to the point formulaon the quasi-geoid. By definition, this distance equals the height anomaly: the straight-line distance measured along the ellipsoidal normal from the point P on the Earth’s surface to the point Q on the telluroid. Adapted from Featherstone & Kuhn (2006), Fig. 3.
````

Table 1.1: A comparison of height systems with respect to various properties that distinguish them. Taken and adapted from Meyer et al. (2006).

|  | Uncorrected diff. leveling | Dynamic | Orthometric | Normal | Ellipsoidal |
| --- | --- | --- | --- | --- | --- |
| G0 | N/A | γ0 = constant | formula | formula | N/A |
| Do points with equal height define level surface? | No | Yes | No | No | No |
| Small correction to leveling data? | n/a | No | Yes | Yes | N/A |
| Geometrically meaningful? | Yes | No | Yes | Yes | Yes |
| Physically meaningful? | Yes | Yes | Yes | No | No |
| Does not require info about Earth’s density distribution | Yes | Yes | No | Yes | Yes |

## Datums and Frames

Before a specific coordinate system can be used to describe the
horizontal and/or vertical position of points on the Earth, it must be
referenced to the Earth. For an ellipsoidal coordinate system, for
example, this entails fixing the parameters that define the size and
shape of the reference ellipsoid, as well as its position relative to
the Earth (three parameters defining the origin), its orientation (three
parameters), and the scale (one parameter). An orthometric height system
is referenced to the Earth by defining the zero-height surface, its
orientation (i.e., the direction of the vertical axis), and the scale.

These definitions constitute what is known as the *datum*. In other
words, a datum is the information required to fix a coordinate system to
an object such as the Earth (Iliffe and Lott, 2008). Together with the
coordinate system, the datum defines the *coordinate reference system
(CRS)*, also known as the spatial reference system.

*The datum specifies how the CRS relates to the Earth, while the
coordinate system specifies how coordinates are expressed within that
datum.*

Several types of datums can be distinguished. In this chapter, we
introduce geodetic datums, vertical datums, and engineering datums. For
each, we describe the information they specify.

In addition to datums, geodesy distinguishes reference frames. In this
respect, geodetic terminology departs from the ISO 19111 standard, which
treats the terms “datum” and “reference frame” as synonymous. In the
final subsection, we define what is meant by a reference frame and
explain why it is distinguished from a datum.

### Geodetic Datums

A geodetic datum describes the relationship between a reference sphere
(for spherical coordinates) or a reference ellipsoid (for ellipsoidal
coordinates) and the Earth. The sphere or ellipsoid of revolution is a
mathematical approximation of the Earth’s shape. The actual shape of the
Earth is represented by the equipotential surface that best fits mean
sea level—the geoid (see Sect. 3.2). The sphere or ellipsoid therefore
serves as an approximation to the geoid.

Before the satellite era, the parameters defining the size and shape of
the ellipsoid of revolution were estimated from local or regional
measurements. This explains why multiple reference ellipsoids exist.
Today, the GRS80 ellipsoid (see Table 1.2) is the standard.

| ellipsoid | *a* \[m\] | *1/f* \[-\] | *GM* \[m<sup>3</sup>/s<sup>2</sup>\] |
|:------------|:-------------|:------------------------|:--------------------|
| Bessel (1841) | 6 377 397.155 | 299.152 812 8 |  |
| GRS80 | 6 378 137 | 298.257 222 100 882 711 243 | 3 986 005·10<sup>8</sup> |
| WGS84 | 6 378 137 | 298.257 223 563 | 3 986 004.418·10<sup>8</sup> |

**Table 1.2.** Common ellipsoids with semi-major axis *a*, inverse
flattening *1/f*, and, where available, the associated value of GM. The
full list of ellipsoids is much longer. The very small difference in
flattening between WGS84 and GRS80 results in differences of at most
0.105 mm and is negligible for all practical purposes. (After Tiberius
et al., 2022.)

As noted in the introduction, a geodetic datum includes not only the
parameters describing the size and shape of the sphere or ellipsoid, but
also the position of the origin, the orientation of the axes, and the
scale (unit). In the pre-satellite era, the datum was chosen so that the
ellipsoid provided the best possible approximation to the *local* geoid.
This was achieved by specifying a point—sometimes referred to as the
fundamental point—for which the separation between the ellipsoid and the
geoid was zero, and for which the ellipsoidal normal coincided with the
direction of local gravity. Furthermore, the orientation of the minor
axis of the ellipsoid was chosen to be parallel to the Earth’s rotation
axis, and a prime meridian was defined for zero longitude. As
illustrated in Fig. {numref}`refsys7`, alignment to the local geoid means that even when
the same reference ellipsoid is used, different geodetic datums may be
obtained.

````{figure} ../figures/part-a_refsys7.png
---
name: refsys7
width: 40%
align: center
---
The shape of the Earth, i.e. the geoid (blue dashed line) with its best fitting reference ellipsoid (blue solid line). The red reference ellipsoids have a different size and shape compared to the one the best fits the global geoid. Both are positioned and oriented in such a way that they fit the local geoid best in different locations resulting in different geodetic datums.
````

Modern, global geodetic datums—such as those used in GNSS
positioning—are based on a geocentric 3D Cartesian coordinate system
whose origin coincides with the Earth’s centre of mass. Its *z*-axis
aligns with the actual rotation axis of the Earth. Both the direction
and speed of this rotation axis are determined by the International
Earth Rotation and Reference Systems Service (IERS; McCarthy and Petit,
2003). The prime meridian is the international reference meridian
defined by the IERS, which is, in principle, coincident with the
meridian passing through the old Greenwich Observatory. When ellipsoidal
coordinates are computed, the GRS80 ellipsoid is used.

### Vertical Datums

A vertical datum describes how an adopted height coordinate system is
fixed to the Earth. Since these lecture notes consider only
gravity-related heights, the discussion is restricted to *gravity-based*
vertical datums. A vertical datum defines the reference level (i.e., the
origin) and assigns it a numerical value—either by defining a reference
equipotential surface through the *W<sub>0</sub>* value, or by assigning
a potential (or height) value to a fundamental benchmark or cluster of
benchmarks also referred to as the datum point(s). In addition, a
vertical datum defines the orientation of the vertical axis and the
scale.

The alternative ways of defining a vertical datum correspond to
different methods of height determination. The second method is
historically the oldest and applies to height determination by means of
*spirit levelling*, potentially augmented by gravimetric observations.
The first method applies when heights are determined using what is
commonly referred to as *GNSS/levelling*; in this case, orthometric (or
normal) heights are obtained by differencing GNSS-derived ellipsoidal
heights and geoid (or quasigeoid) heights.

Historically, vertical datums were often defined using
observation-derived (mean) water levels at one or more locations. In the
Netherlands, for example, the Amsterdam Ordnance Datum—*Normaal
Amsterdams Peil (NAP)*—is based on water-level measurements in the IJ
(then still connected to the Zuiderzee), recorded daily at high tide
between 1683 and 1684. The resulting average high-water level was
adopted as the datum of what was then known as the *Amsterdams Peil*.
This datum was materialised by eight large marble stones installed into
locks around the IJ, each containing a horizontal groove indicating the
reference height. The Amsterdams Peil was subsequently transferred by
spirit levelling across the Netherlands and is now known as NAP.
Although the original stones are no longer used—and the datum is today
realised through six underground benchmarks in the Veluwe and Utrecht
Hill Ridge areas—the definition of the datum itself has remained
unchanged.

When countries or regions define their vertical datums based on local
water-level observations, systematic differences between datums
inevitably arise. Regardless of the chosen water level (e.g., mean water
level), it represents a quantity that varies in both space and time.
Consequently, the height of a point relative to datum A will generally
differ from its height relative to datum B. Within Europe, such
differences can amount to approximately 2.30 m (see Fig. {numref}`refsys8`).

````{figure} ../figures/part-a_refsys8.png
---
name: refsys8
width: 40%
align: center
---
The differences between the national vertical datums and the one adopted for the European vertical vertical reference system. Taken from www.bkg.bund.de.
````

### **Engineering datums**

An engineering datum describes the relationship of a coordinate system
to a local reference. This reference may be any moving object, such as a
vehicle, aircraft, or ship, but it may equally be a fixed local area,
such as a construction site or building.

For Earth-fixed objects, the datum typically includes physical marks or
survey points that define the coordinate system (usually Cartesian).
Coordinates are assigned to these points, and their numerical values are
generally chosen to avoid negative numbers. To establish axis
orientation, a second point—which must be visible from the datum
point—is identified as a reference object. This reference point is
assigned a direction (a bearing), often set to 0°, or chosen to align
approximately with true north.

For moving platforms, a physical point on the platform may be selected
as the origin of the coordinate system, or the origin may be a virtual
point defined at the intersection of the coordinate axes, which are
themselves aligned with structural elements of the platform (e.g., the
centreline of a ship or the longitudinal axis of an aircraft).

### Datums versus Reference Frames

The ISO 19111 standard treats the terms ‘datum’ and ‘reference frame’ as
synonymous, stating that “*geodetic and vertical datums are referred to
as reference frames”.* Consistent with the definition of a datum adopted
above, ISO 19111 defines a datum as a “*parameter or set of parameters
that realize the position of the origin, the scale, and the orientation
of a coordinate system*”. Strictly speaking, however, and in accordance
with geodetic literature (e.g., Drewes, 2009) a clear conceptual
distinction exists between a datum and a reference frame.

Following the definition of the International Association of Geodesy
(<https://geodesy.science/glossary/reference-frame/>), a reference frame
is understood as the physical realization of a reference system. This
realization consists of a set of physical (materialized) points whose
horizontal and/or vertical positions—and possibly velocities—are known
within a specific CRS. This set of accessible points enables users to
determine the coordinates of their own points of interest with respect
to that CRS.

In the context of a levelling-based vertical (height) reference frame,
the frame consists of a network of benchmarks (see {numref}`refsys9`), typically
installed in buildings, bridges, or other stable structures, for which
heights—and in some cases vertical motions—have been determined. A user
requiring the height of a point *P* performs levelling to one or more
benchmarks and computes the height of *P* as the sum of the benchmark
height and the measured height difference. The benchmark heights
themselves are estimated through a network adjustment of levelling
observations—potentially integrated with gravity data—which connect all
benchmarks to the datum point(s) and thereby reference the estimated
heights to the adopted vertical datum. *In this adjustment, the height
assigned to the datum point(s) is fixed and not subject to estimation*.

Each time new levellings are performed between the datum point(s) and
the benchmarks, and the benchmark heights are re-estimated, a new
reference frame is obtained. This new frame will differ from the
previous one because: (i) repeated levellings will not yield identical
height differences due to measurement uncertainty; (ii) new benchmarks
may have been installed and/or existing ones removed; and/or (iii) some
points may have experienced vertical motion. However, as long as the
assigned height of the fundamental benchmark(s) remains unchanged, the
datum itself has not changed.

````{figure} ../figures/part-a_refsys9.png
---
name: refsys9
width: 40%
align: center
---
A height benchmark in the CiTG building.
````

This example illustrates that a new vertical reference frame can be
realized without redefining the vertical datum. The converse, however,
is not true: redefining or rematerializing the datum—for example, by
establishing a new fundamental benchmark that fixes the
datum—necessarily requires the computation of a new reference frame.
This principle applies equally to other types of datums (e.g., geodetic
datums). As stated by Drewes (2009): “*reference systems, the geodetic
datum, and reference frames form an order of hierarchy: (i) The
definition of a reference system must be completely unaffected by the
realization of the reference frame and the geodetic datum, i.e., the
realization of the system by the frame and the allocation of the datum
must not change the definition. (ii) The realization of the datum has to
be done by methods independent of the measurements of the reference
frame, i.e., measurement errors or physical changes altering the
observations of the frame must not affect the datum. (iii) The
mathematical realization of the reference frame has to be done by
algorithms that keep the datum parameters fixed and follow strictly the
principles defined by the reference system”*.

Using the terms datum and reference frame interchangeably reflects the
practical reality that a reference frame provides direct operational
access to the datum. In the context of a levelling-based vertical
reference frame, this means that a user requiring heights relative to
datum A does not need to perform levelling all the way from the datum
point itself. Nevertheless, such a reference frame can only be computed
because a datum has first been defined and materialized.

## **Map Projections**

One widely used type of coordinate reference system (CRS) is the
*projected* CRS, in which positions on Earth are represented using
Cartesian coordinates—typically called eastings (*E*) and northings
(*N*)—on a flat, two-dimensional surface produced by a specific map
projection. There are two main reasons for using projected CRSs. The
first is that we need them to display maps on paper or a screen. The
second is that many geometric operations, such as calculating distances
and areas, are simpler and more efficient in a planar Cartesian system
than on a sphere or ellipsoid. *Nevertheless, the fundamental coordinate
system underlying all projections remains the ellipsoidal one.* In the
terminology of ISO 19111, every projected CRS is defined as a *derived*
CRS whose *base* CRS is a geographic CRS.

Representing the curved Earth on a flat surface inevitably introduces
distortions. For this reason, many different map projections exist, each
optimized for particular applications, regions, or properties. For
engineers and scientists in EC&T, it is important to understand the
underlying concepts so that they can (i) make informed choices about
which projection is most suitable, and (ii) perform both forward and
inverse projections correctly. This section begins by introducing the
fundamental concepts, followed by a description of the defining
parameters of various projections.

### **Fundamental Concepts**

#### **Grids and Graticules**

Maps typically display the projected meridians and parallels that result
from transforming geographic coordinates onto a plane; this network is
called the *graticule*. Its appearance depends on the chosen
projection—graticule lines may appear straight, curved, or in more
complex forms.

The graticule itself is not the basis of the projected CRS. Instead, the
projected CRS uses a Cartesian coordinate system, known as the grid.
Calculations of distances, areas, and bearings are performed using grid
coordinates.

#### **Distortion**

Because every projection introduces distortion, we require measures to
quantify it. The most basic measure is the scale factor, denoted *k*
(not to be confused with map scale):

*k* = distance on projection / distance on ellipsoid.

The value of *k* varies from point to point and often also with
direction, so it applies only to short distances. For longer lines, the
appropriate measure is the integrated mean of the scale factor along the
entire line.

A classical way to visualize distortion is using Tissot’s indicatrix—the
shape resulting from projecting an infinitesimally small circle from the
sphere or ellipsoid onto the map. It depends on the scale factors along
the meridian and parallel and on the angle between them. The result is
an ellipse whose axes indicate the directions of maximum and minimum
scale distortion. See {numref}`refsys10` for an example.

````{figure} ../figures/part-a_refsys10.png
---
name: refsys10
width: 40%
align: center
---
Tissot's indicatrices on the Mercator projection. Stefan Kühn, CC BY-SA 3.0 <http://creativecommons.org/licenses/by-sa/3.0/>, via Wikimedia Commons.
````


### **Projections Surfaces**

Historically, many projections were conceptualized using projection (or
developable) surfaces—surfaces such as planes, cylinders, or cones ({numref}`refsys11`) that can be unrolled onto a flat sheet without further distortion.
In this approach, the projection surface is placed either tangentially
(touching the globe) or secantly (cutting through it), geographic
features are transferred to the surface, and the surface is then
flattened. At the line or point of contact, distortion is minimal and
*k*=1.

The choice of projection surface depends on the geographical extent of
the region to be mapped and determines broad characteristics of the
projection. For example, a cylindrical surface that touches the Earth
along the equator is well suited for mapping equatorial regions.

Using the type of projection surface, projections may be broadly
classified as:

**Cylindrical projections** – The projection surface is a cylinder. The
resulting maps are rectangular. Meridians and parallels appear as
straight lines intersecting at right angles (in the normal or transverse
aspect, see {numref}`refsys11`). Meridians are equally spaced, while spacing
between parallels increases toward the poles. Cylindrical projections
are conformal and preserve directions along straight lines. The line(s)
of tangency or secancy have no distortion. Other geographical properties
vary according to the specific projection.

**Conic projections** – The projection surface is a cone. Parallels
appear as arcs of concentric circles, and meridians converge toward the
poles. These are often used for regions with a large east–west extent.

**Planar (Azimuthal) projections** – The projection surface is a plane
that may touch or intersect the globe at any point. If it touches a
pole, meridians appear as straight lines and parallels as concentric
circles. At the point of contact, directions are accurate.

````{figure} ../figures/part-a_refsys11.png
---
name: refsys11
width: 40%
align: center
---
Cylindrical, conic and azimuthal map projections. Image of cylindrical, conic and azimuthal map projection, by Traroth, March 2005, taken from Wikimedia Commons, under CC BY-SA 3.0 license.
````

The projection surface can be oriented in different ways, described by
its *aspect*. It may be normal (aligned with Earth’s rotation axis),
transverse (perpendicular to it), or oblique (any angle in between) (see
{numref}`refsys12`).

````{figure} ../figures/refsys_12.png
---
name: refsys12
width: 40%
align: center
---
Normal, transverse and oblique projection for a cylinder. Image on cylindrical projection aspects by Peter Mercator, own work, November 2009, taken from Wikimedia Commons. Public Domain.
````

Although these geometric models are conceptually useful, in practice a
map projection is defined mathematically as a transformation: *(E,N) =
f(φ, λ)*.

#### Projection origin

Map projections also differ in the point of perspective from which the
surface is conceptually projected. {numref}`refsys13` illustrates three common
cases: gnomonic, stereographic, and orthographic projections.

````{figure} ../figures/refsys_13.png
---
name: refsys13
width: 40%
align: center
---
Cross-section of azimuthal map projection, the mapping surface being a flat plane, with central point of projection, so-called gnomonic (left), stereographic projection (middle), and orthographic projection (right). Taken from Tiberius et al. (2022).
````

#### **Preserved Properties**

Although all projections distort shape, area, and scale, we can choose
which properties to preserve. This provides another classification
scheme, complementary to the classification by projection surface:

- **Equidistant projections** – Preserve true distance along one or more
  lines, or from one or two points to all other points on the map.

- **Equal-area projections** – Preserve the relative area of regions.
  Shape, angle, and scale may be distorted, and meridians and parallels
  may not intersect at right angles.

- **Conformal projections** - Preserve the shape of *small* areas by
  maintaining angles. Scale varies with location but not direction.
  However, they cannot preserve the shape of large regions.

- **Gnomonic projections** – Preserve great-circle paths as straight
  lines, so the shortest route between two points appears as a straight
  line.

- **True-direction (azimuthal) projections** - Preserve the correct
  direction (azimuth) from the central point to all other points.

This list is not exhaustive. Some projections are neither equal-area,
equidistant, nor conformal. The choice of projection depends on the
intended application and the acceptable trade-offs in geometric
distortion.

### **Defining Parameters**

Each map projection requires a set of *defining* parameters. These
specify the origin and allow the projection to be customized for a
particular region. They are sometimes divided into angular parameters
(expressed in geographic coordinates) and linear parameters (expressed
in projected coordinates). We distinguish between mandatory parameters
and projection-specific parameters.

Mandatory parameters (define the geometric centre of the projection and
coordinate system offsets):

- **Latitude of the true origin** – Defines the origin of the
  Y-coordinates. While it often coincides with the geometric centre of
  the projection, it does not always imply the point of zero distortion.
  For example, in a conic projection, this anchors the cone's apex
  (i.e., point where all the lateral edges meet) relative to the pole.
  In many world projections, it is defined to be the equator.

- **Longitude of the true origin** (equivalent to the central meridian
  for cylindrical and other projections) – Defines the origin of the
  X-coordinates. In cylindrical projections (like Transverse Mercator),
  this line is usually a straight vertical line. Maps are typically
  symmetrical around this line, and distortion increases with distance
  from it.

- **False easting** - A constant value added to all X-coordinates to
  ensure they are positive.

- **False northing** - A constant value added to all Y-coordinates to
  ensure they are positive.

Projection-specific parameters include:

- **First (or only) standard parallel** – For conic projections, defines
  the latitude where the projection surface touches or intersects the
  globe (where *k*=1.0).

- **Second standard parallel –** For *secant* conic projections, defines
  the second line of latitude where the projection surface intersects
  the globe (where *k*=1.0).

- **Azimuth of the centre line** (for oblique projections) – The
  orientation of the projection’s central line relative to north.

- **The rectifying rotation of the map grid** (for oblique projections)
  – A rotation applied to align the y-axis with true north or another
  desired direction.

- **Overall scaling factor** – Applied (often at the central meridian)
  to balance distortion between the centre and edges of the projection.

## Coordinate Reference Systems

In Sect. 4, we established that a Coordinate Reference System (CRS)
consists of two main components: the datum and the coordinate system. In
Sect. 4.4, we introduced the idea that for users to determine
coordinates within a specific CRS, the system must be realized in
practice. This requires a set of physical points whose coordinates (and
possibly velocities) are known in that CRS. This set of points is known
as the reference frame.

*In this section, when we refer to a CRS, we mean the functional
combination of the reference system and its realization (the frame).*

Many thousands of CRSs have been defined for describing positions on or
near the Earth’s surface. Broadly, they fall into five categories:
Geographic CRSs (or geodetic), Geocentric CRSs (or Earth-Centered
Earth-Fixed), Projected CRSs (or planar/grid), Vertical CRSs, and
Engineering CRSs (or local/custom). In this section, we introduce the
first four types and provide representative examples. In practice,
multiple CRSs are often combined to describe a point’s position
fully—for example, pairing a geographic CRS for horizontal coordinates
with a vertical CRS for height. Such combinations are known as
*Compound* CRSs, although we do not treat them separately here. We also
do not discuss *Spatio-temporal* CRSs, which are compound systems where
one constituent is spatial and the other is temporal.

**To prepare the descriptions of the examples presented in this section,
we drew on the Dutch documentation available at the National Spatial
Data Infrastructure website.**

### Geographic Coordinate Reference Systems

A Geographic CRS describes positions on the curved surface of the Earth.
It is defined by a geodetic datum and an ellipsoidal coordinate system.
Coordinates are expressed as angular values: geographic (or geodetic)
latitude (*φ*), longitude (λ), and often include ellipsoidal height
(*h*).

**Usage:** Geographic CRSs are standard in global navigation, aviation,
and marine positioning. Because they follow the curvature of the Earth,
they are suitable for mapping very large regions or the entire globe.
However, since the coordinates are angular, calculating distances or
areas directly requires specialized formulas rather than simple plane
geometry.

**Key Examples:**

- **WGS 84 (World Geodetic System 1984):** WGS 84 is the reference
  system used by the Global Positioning System (GPS). It is maintained
  by the U.S. National Geospatial-Intelligence Agency (NGA) and realized
  through the coordinates of GPS ground stations and the orbital
  parameters of GPS satellites. Users can typically determine positions
  in WGS 84 with meter-level accuracy. Periodically, new realizations of
  WGS 84 are aligned with the most recent realization of the
  International Terrestrial Reference System.

- **Geographic ITRS (International Terrestrial Reference System):** The
  ITRS is the most accurate global scientific coordinate system and is
  recognized by the United Nations as the official Global Geodetic
  Reference Frame. It is defined by the International Association of
  Geodesy (IAG) and the International Earth Rotation and Reference
  Systems Service (IERS), and realized using the coordinates of GNSS
  stations in the International GNSS Service (IGS) network and other
  satellite geodesy systems. *Because ITRS maintains the average motion
  of all tectonic plates, its coordinates are time-dependent.* Thus,
  every coordinate must include a realization and an epoch, and
  preferably also a velocity. For points on the stable part of a
  tectonic plate, specifying the epoch and the plate identifier (e.g.,
  EURA for the Eurasian Plate) is usually sufficient for horizontal
  coordinates. New measurements lead to new realizations, known as
  International Terrestrial Reference Frames (ITRF). Recent realizations
  include ITRF2014 and ITRF2020.

- **Geographic ETRS89 (European Terrestrial Reference System 1989):**
  ETRS89 is the official 3D coordinate system of the Netherlands and of
  most other European states. It is defined by the EUREF sub-commission
  of the IAG as a transformation of ITRS. *The transformation accounts
  for the motion of the stable part of the Eurasian tectonic plate,
  making horizontal coordinates effectively time-independent for most
  applications.* National coordinate systems across Europe are tied to
  ETRS89. New realizations of ITRS lead to corresponding new
  realizations of ETRS89. In the Netherlands, the adopted realization is
  ETRF2000, following EUREF recommendations. *Geographic
  coordinates—latitude and longitude in degrees, with height in meters
  above the ellipsoid—are used for data storage, data exchange, and
  geospatial computations.*

### Geocentric Coordinate Reference Systems

A Geocentric CRS is a 3D Earth-Centered, Earth-Fixed (ECEF) system. Like
the Geographic CRS, it uses a geodetic datum, but it employs a 3D
Cartesian coordinate system. The origin coincides with the Earth's
centre of mass, the Z-axis aligns with the Earth's rotation axis, and
the X and Y axes define the equatorial plane. Positions are expressed in
triplets of X,Y,Z (in meters).

**Usage:** Geocentric CRSs are essential for satellite geodesy. GNSS
satellites orbit in geocentric space, and position calculations are
performed in this system before being converted to geographic or
projected coordinates for use on the ground. Although not intuitive for
human navigation, geocentric coordinates form the computational
foundation for modern positioning.

**Key Examples:**

- **Geocentric ITRS**: XYZ coordinates in meters relative to the Earth’s
  centre of mass are used in standard GNSS exchange formats such as
  RINEX. Except at the poles and the equator, the axes intersect the
  Earth’s surface at oblique angles.

- **Geocentric ETRS89**: XYZ coordinates in meters relative to the
  Earth’s centre of mass are also used in RINEX and other GNSS exchange
  formats. As with geocentric ITRS, the axes meet the Earth’s surface
  obliquely except at special locations such as the North Pole.

### Projected Coordinate Reference Systems

A Projected CRS is created by applying a map projection to a Geographic
CRS. The projection maps the curved ellipsoidal surface onto a flat,
two-dimensional plane. The result is a Cartesian coordinate system with
positions expressed as Easting (E) and Northing (N), or x and y, in
meters.

**Usage:** Projected CRSs are indispensable for engineering, cadastral
surveying, and large-scale mapping. On a flat plane, distances, angles,
and areas can be computed easily using standard Euclidean geometry.
However, all map projections introduce distortion, so projected CRSs are
typically designed for specific regions or zones where distortion can be
kept within acceptable limits.

**Key Examples:**

- **WGS84 UTM (Universal Transverse Mercator):** The UTM system uses a
  transverse Mercator projection applied to the WGS 84 ellipsoid. The
  Earth is divided into 60 zones, each spanning 6 degrees of longitude.
  Each zone has its own central meridian and its own planar coordinate
  system. The scale factor at the central meridian is typically 0.9996,
  limiting distortion within the zone. UTM coordinates are widely used
  for topographic mapping and general location referencing.

- **Dutch Triangulation System (Rijksdriehoeksstelsel, RD):** The RD
  system provides projected x-y coordinates in meters and is
  traditionally used on land, inland waters, and the coastal zone of the
  Netherlands, and increasingly also in the Dutch Exclusive Economic
  Zone (EEZ). RD is defined by the Dutch Cadastre (Kadaster) as a
  transformation of ETRS89 using RDNAPTRANS™. Distortions in the RD
  system—up to about 0.25 m from noise propagation in historical
  triangulation measurements—are modelled using a correction grid. The
  underlying stereographic projection preserves angles, and scale
  distortions are small: within the traditional Dutch land area,
  distortions are less than 0.15 m per km, and within the Dutch EEZ,
  less than 1.01 m per km.

### Vertical Coordinate Reference Systems

A Vertical CRS is a one-dimensional reference system used for
gravity-related heights. Its datum defines the origin, the orientation
of the vertical axis, and the scale (Sect. 4.2) and is typically related
to a mean water level such as mean sea level.

**Usage:** Vertical CRSs are essential in water management, hydrography,
and infrastructure design and maintenance.

**Key Examples:**

- **NAP (Normaal Amsterdams Peil):** NAP is the Dutch reference surface
  for precise physical heights, used on land, inland waters, and in the
  coastal zone. At sea, NAP is represented by the quasi-geoid. NAP
  originates from the Amsterdams Peil (AP), defined as the mean high
  water level on the IJ in 1683–1684. Today, NAP is maintained by
  Rijkswaterstaat using stable underground benchmarks, with the
  benchmark in Amsterdam serving as the fundamental point. Heights of
  NAP benchmarks are determined using precise leveling. Transforming an
  ETRS89 height with RDNAPTRANS™ provides an accurate approximation of
  NAP height.

- **EVRS (European Vertical Reference System):** EVRS is the unified
  European system for precise physical heights. The first realization,
  EVRF2000, used a single datum point in Amsterdam, aligning the EVRS
  reference surface with NAP. Later realizations use multiple datum
  points while preserving the mean level defined in EVRF2000. New
  leveling campaigns can lead to new realizations with regionally
  significant updates. The most recent realization is EVRF2019. EVRS is
  defined by the EUREF sub-commission of the IAG as a leveling-based
  height system. Transformations from national height systems provide
  accurate approximations. A direct transformation between ETRS89
  heights and EVRS heights is still under development.

- **International Height Reference System (IHRS)**: IHRS is the emerging
  international system for precise physical heights. A formal
  realization has not yet been published by the International
  Association of Geodesy (IAG).

## Coordinate Transformations

In Sect. 2, we introduced the relationships between Cartesian
coordinates and their spherical and geographic counterparts. These
relationships allow us to convert coordinates from one coordinate system
to another. They are exact and do not involve any change of datum. The
same is true for map projections. Both types of operations fall under
the category of coordinate conversions.

In addition to coordinate conversions, we also distinguish coordinate
transformations, which are operations that change the datum. Because the
parameters used in such transformations ultimately depend on
observations, datum transformations are not exact—observations
themselves are never exact. Furthermore, depending on the transformation
applied, datum transformations are not necessarily reversible.

In this section, we first outline a general strategy that enables the
application of datum transformations without requiring a whole set of
methods. We then present the 3D similarity transformation followed by
coordinate operations for vertical CRSs.

### Overview of Transformations

Starting from the five different types of CRSs introduced in Sect. 6, a
wide range of different transformations can be envisaged. For example,
transformations from one geographic CRS to another, but also
transformations from an engineering CRS to a geocentric CRS. It is
possible to transform directly between two CRSs of the same type. Within
the scope of these lecture notes, however, it is not feasible to treat
all the methods required for this. We therefore resort to *indirect*
transformation methods. Essentially, these consist of first converting
the coordinates to a geocentric CRS, then transforming them to the
target geodetic datum, and finally converting the coordinates to the
desired coordinate system. From an educational point of view, this means
that we only need to introduce a single transformation method. This is
the commonly applied *7-parameter similarity transformation* (or
*14-parameter* in the case that time dependency is included). The
strategy is outlined in {numref}`refsys14`.

````{figure} ../figures/refsys_14.png
---
name: refsys14
width: 40%
align: center
---
Coordinate conversions and datum transformations. The horizontal operations represent coordinate conversions, while the vertical operations show datum transformations from system A to system B. Although direct transformations between different projected and geographic CRSs are possible, our strategy relies on indirect methods. These consist of converting the coordinates to a geocentric CRS, applying the datum transformation to the target geodetic datum, and then converting the transformed coordinates to the desired coordinate system. Figure is taken and adapted from Tiberius et al. (2022, Fig. 31.1).
````

### 3D Similarity Transformations

3D similarity transformations, also referred to as Helmert
transformations, are transformations that preserve shape (lengths of
lines and the position of points may change). The transformation
accounts for a translation of the origin of the 3D Cartesian coordinate
system (3 parameters), a rotation about each of the three axes (3
parameters), and a change in the scale (1 parameter). It is written as:

$$\left( \begin{array}{r}
X \\
Y \\
Z
\end{array} \right)_{Target} = \lambda R\left( \Omega_{X},\Omega_{Y},\Omega_{Z} \right)\left( \begin{array}{r}
X \\
Y \\
Z
\end{array} \right)_{Source} + \left( \begin{array}{r}
\Delta X \\
\Delta Y \\
\Delta Z
\end{array} \right),$$

where *λ = 1+μ* is the scale factor between the two systems, *μ* the
differential scale factor (sometimes expressed in parts-per-million
(ppm), with 1 ppm = 10<sup>−6</sup>), and **R** is the rotation matrix
defined as:

*R*(*Ω*<sub>*X*</sub>, *Ω*<sub>*Y*</sub>, *Ω*<sub>*Z*</sub>) = *R*<sub>*Z*</sub>(*Ω*<sub>*Z*</sub>)*R*<sub>*Y*</sub>(*Ω*<sub>*Y*</sub>)*R*<sub>*X*</sub>(*Ω*<sub>*X*</sub>),

with

$$R_{X}\left( \Omega_{X} \right) = \begin{bmatrix}
1 & 0 & 0 \\
0 & \cos\Omega\ {X} & \sin\Omega_{X} \\
0 & - \sin\Omega_{X} & \cos\Omega_{X}
\end{bmatrix},R_{Y}\left( \Omega_{Y} \right) = \begin{bmatrix}
\cos\Omega_{Y} & 0 & - \sin\Omega_{Y} \\
0 & 1 & 0 \\
\sin\Omega_{Y} & 0 & \cos\Omega_{Y}
\end{bmatrix},R_{Z}\left( \Omega_{Z} \right) = \begin{bmatrix}
\cos\Omega_{Z} & \sin\Omega_{Z} & 0 \\
 - \sin\Omega_{Z} & \cos\Omega_{Z} & 0 \\
0 & 0 & 1
\end{bmatrix}.$$

The composed rotation is gained by the rotation of
*Ω*<sub>*X*</sub>about the x-axis, followed by *Ω*<sub>*Y*</sub>around
the y-axis (already subject to the first rotation) and finally
*Ω*<sub>*Z*</sub>about the z-axis (again subject to the previous two
rotations).

If the rotation angles are small (i.e., less than 10"), **R** is given
by:

$$R\left( \Omega_{X},\Omega_{Y},\Omega_{Z} \right) = \begin{pmatrix}
1 & \Omega_{Z} & - \Omega_{Y} \\
 - \Omega_{Z} & 1 & \Omega_{X} \\
\Omega_{Y} & - \Omega_{X} & 1
\end{pmatrix},$$

and the transformation is simplified (products *μ* Ω<sub>𝑖</sub> can be
safely neglected) to:

$$\left( \begin{array}{r}
X \\
Y \\
Z
\end{array} \right)_{Target} = \left( \begin{array}{r}
X \\
Y \\
Z
\end{array} \right)_{Source} + \begin{pmatrix}
\mu & \Omega_{Z} & - \Omega_{Y} \\
 - \Omega_{Z} & \mu & \Omega_{X} \\
\Omega_{Y} & - \Omega_{X} & \mu
\end{pmatrix}\left( \begin{array}{r}
X \\
Y \\
Z
\end{array} \right)_{Source} + \left( \begin{array}{r}
\Delta X \\
\Delta Y \\
\Delta Z
\end{array} \right).$$

**Be aware that different conventions are used for the sign of the
rotation parameters.** In both conventions a positive rotation occurs in
an anti-clockwise direction, when looking along the positive axis
towards the origin. However, the IERS convention (also called the
position vector convention) deems the rotations to be of the points
relative to the axes while the ‘*coordinate frame rotation convention*’
that is used here deems the rotations to be of the axes relative to the
points.

The values of the transformation parameters must be estimated. In many
cases, however, this does not need to be done by the user, as published
parameter values are available. For example, transformations between the
ITRF and ETRF can be performed using parameter sets published by EUREF.
In particular when working with engineering CRSs, it may be necessary to
derive the parameters oneself. In that case, a set of points is required
for which coordinate values are known in both CRSs between which the
transformation is to be applied. Since a three-dimensional similarity
transformation involves seven parameters, the theoretical minimum number
of points is three. To ensure reliability and redundancy, however, a
larger number of well-distributed points is typically used. The
transformation parameters are then estimated using least-squares
adjustment, which seeks to minimize the sum of squared residuals between
the transformed coordinates and the known target coordinates. The
quality of the resulting transformation can be assessed by comparing
transformed coordinates with independently known coordinates at points
that were not included in the estimation.

### Coordinate Operations for Vertical CRSs

Two main operations are: i) the transformation between ellipsoidal
heights and gravity-related heights and ii) the transformation between
gravity-related heights referring to different vertical datums. The
first is required when converting GNSS-derived ellipsoidal heights into
gravity-related heights. The second is required, for example, in case
your area of interest covers multiple countries – each having their own
national vertical CRS.

The relation between orthometric height 𝐻 and ellipsoidal height ℎ is
without any significant loss of accuracy given by ℎ=𝑁+𝐻, where *N* is
the height of the geoid above the ellipsoid. For the relation between
the normal height *H<sup>N</sup>* and ellipsoidal height ℎ, we need to
replace *N* by the height of the quasi-geoid (*ζ*). The values of the
(quasi-)geoid height are typically to be obtained from gridded
(quasi-)geoid models. Such models are computed from various types of
gravity data acquired both in-situ as well as from moving platforms
(e.g., airplanes, ships, and satellites) and may cover a particular
country, region or even the entire globe. In the Netherlands, the
official model to be used in order to convert GNSS-derived ellipsoidal
heights into NAP heights is the NLGEO2018 quasi-geoid model (see {numref}`refsys15`).

````{figure} ../figures/refsys_15.png
---
name: refsys15
width: 40%
align: center
---
The Dutch NLGEO2018 quasi-geoid model that needs to be used to convert GNSS-derived ellipsoidal heights into NAP heights.
````

The transformation between vertical CRSs referring to different vertical
datums is one that can be written as (Iliffe and Lott, 2008):

$$H_{Target} = \left\lbrack \left( H_{Source} + \Delta H \right)U_{Source} \right\rbrack\frac{m}{U_{Target}},$$

with *Δ**H*being an offset, *m* is a unit direction multiplier (*m* = 1
if both systems are height or both are depth and *m* = -1 if one system
is height and the other system is depth), and *U*<sub>Source</sub> and
*U*<sub>Target</sub> are unit conversion ratios to metres for the source
and target systems and the offset value respectively. *Δ**H*may be: i) a
constant that is valid for an entire region, ii) a spatially varying
offset to be obtained by means of interpolation from a gridded dataset,
or iii) is given by a mathematical model. One example of the latter that
has been used in the past to describe the transformation between the
national vertical CRSs and the European Vertical Reference Frame is the
model of a tilted plane that includes a constant offset as well as a
slope in longitude and latitude direction.

### Practical Implementation

Software for map projections, coordinate conversions and datum
transformations is provided for instance by the open source PROJ package
(<https://proj.org/>) used by several Geographic Information System
(GIS) packages (e.g. the open source QGIS package). PROJ started purely
as a cartography application, but over the years support for datum
shifts and more precise coordinate transformations were added to PROJ.
In their own words: “*Today PROJ supports more than a hundred different
map projections and can transform coordinates between datums using all
but the most obscure geodetic techniques*”.

## **References**

Baker, D. W., & Haynes, W. (2020). *Engineering Statics: Open and
Interactive*. <https://engineeringstatics.org/>.

Drewes, H. (2009). Reference Systems, Reference Frames, and the Geodetic
Datum. In: Sideris, M.G. (eds) Observing our Changing Earth.
International Association of Geodesy Symposia, vol 133. Springer,
Berlin, Heidelberg. <https://doi.org/10.1007/978-3-540-85426-5_1>.

Featherstone, W. E., & Kuhn, M. (2006). Height systems and vertical
datums: A review in the Australian context. *Journal of Spatial
Science*, *51*(1), 21–41.
<https://doi.org/10.1080/14498596.2006.9635062>.

Foroughi, I. & Tenzer, R. (2017). *Comparison of different methods for
estimating the geoid-to-quasi-geoid separation*, Geophysical Journal
International, Volume 210, Issue 2, Pages 1001–1020,
<https://doi.org/10.1093/gji/ggx221>.

Hofmann-Wellenhof, B. & Moritz, H. (2006). *Physical Geodesy* (2nd ed.).
Springer, Vienna. <https://doi.org/10.1007/978-3-211-33545-1>.

Iliffe, J., & Lott, R. (2008). *Datums and map projections for remote
sensing, GIS, and surveying* (Second edition). Whittles Publishing.
<http://www.dawsonera.com/depp/reader/protected/external/AbstractView/S9781904445968>

ISO (International Organization for Standardization). (2019). Geographic
information – Spatial referencing by coordinates (ISO Standard No.
19111:2019). Geneva, Switzerland.

McCarthy, G. and Petit, G. (2003) ‘IERS Conventions’, IERS Technical
Note No. 32. Available at: [http://www.iers.org](http://www.iers.org/)

Meyer, Thomas H.; Roman, Daniel R.; and Zilkoski, David B. (2006). What
Does Height Really Mean? Part III: Height Systems. Department of Natural
Resources and the Environment Articles. Paper 2.
<http://digitalcommons.uconn.edu/nrme_articles/2>.

Neutsch, W. (2011). *Coordinates*. Walter de Gruyter.

Tiberius, C., van der Marel, H., Reudink, R., & van Leijen, F. (2022).
*Surveying and Mapping*. TU Delft OPEN Publishing.
<https://doi.org/10.5074/T.2021.007>

## Backup material

https://www.google.nl/books/edition/Coordinates/qaYbi3ugRDIC?hl=nl&gbpv=1&dq=Coordinates&pg=PA1329&printsec=frontcover

https://tudelft.on.worldcat.org/oclc/609533634

https://engineeringstatics.org/cartesian-coords-2d.html

The directions of the axes

<https://mathworld.wolfram.com/OrthogonalCoordinateSystem.html>

<https://phys.libretexts.org/Bookshelves/Classical_Mechanics/Variational_Principles_in_Classical_Mechanics_(Cline)/19%3A_Mathematical_Methods_for_Classical_Mechanics/19.04%3A_Appendix_-_Orthogonal_Coordinate_Systems>

<https://books.google.nl/books?hl=en&lr=&id=XVJwDrkZA1wC&oi=fnd&pg=PA8&dq=definition+coordinate+system+&ots=M7gaFRbUiI&sig=oJk43EcXJiMzO3e7W6qhkrUNx7Q#v=onepage&q=definition%20coordinate%20system&f=false>

https://www.usu.edu/geospatial/tutorials/core-concepts/coordinate-systems

<https://docs.ogc.org/per/22-036r1.html#toc16>

-International Organization for Standardization. (2019). Geographic
information – Spatial referencing by coordinates (ISO Standard No.
19111:2019). Geneva, Switzerland.

<https://www.ngs.noaa.gov/research/geopotential-datums/geopotential-surface.shtml>

<https://docs.geotools.org/stable/userguide/library/api/cs.html>

https://docs.ogc.org/as/18-005r4/18-005r4.html#34

The rotations in the 7-parameter similarity transformation described
above are about the origin of the source system. If the area over which
points used in the transformation derivation is small, the angle
subtended by this area at the rotation point is small and the problem is
ill-conditioned. If the problem is ill-conditioned, a rotation around
the origin is very similar to a translation, and a large additional
shift may be needed to compensate for this. There is a high degree of
correlation between the transformation parameters. As such the solution
is not solving for the seven parameters. Therefore, it is better to
apply the rotation around an arbitrary point
(𝑋<sub>0</sub>,𝑌<sub>0</sub>,𝑍<sub>0</sub>) somewhere in the centre of
the network. For this type of transformation three additional
parameters, the coordinates of the rotation point, are required to
describe the transformation. These additional parameters can be chosen
freely, or by convention, and do not have the same role in the
derivation of parameter values for the other 7-parameter. The
transformation essentially remains a 7-parameter transformation, with 7
degrees of freedom, although an extra 3 parameters are needed in the
specification. The transformation formula is:

$$\left( \begin{array}{r}
X \\
Y \\
Z
\end{array} \right)_{Target} = \lambda R\left( \Omega'_{X},\Omega'_{Y},\Omega'_{Z} \right)\left( \begin{array}{r}
X - X_{0} \\
Y - Y_{0} \\
Z - Z_{0}
\end{array} \right)_{Source} + \left( \begin{array}{r}
\Delta X' \\
\Delta Y' \\
\Delta Z'
\end{array} \right) + \left( \begin{array}{r}
X_{0} \\
Y_{0} \\
Z_{0}
\end{array} \right),$$
