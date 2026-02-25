# Measuring and Mapping the Earth

The ability to acquire data, particularly through observation and measurement, is a core skill for engineers and scientists in Earth, Climate and Technology (EC&amp;T). Although, among other things, the quantities you wish to measure, the area of interest, and the instrumentation and methods employed may vary widely, designing and executing an observation campaign is a central component of many projects.

This chapter provides a first, general introduction to the topic. Rather than concentrating on the acquisition of specific types of observations, we adopt a more general and conceptual perspective. Ultimately, the aim is to develop a framework for describing the process of acquiring observations—one that helps structure workflows, evaluate data quality, and determine whether results are fit for purpose.

We begin by defining the terminology needed for this framework. This includes distinguishing between measurements, observations, and data; clarifying concepts such as the measurand (the specific quantity being measured); and explaining the distinction between direct and indirect measurements. We also present a vocabulary for describing uncertainty in measurements.

Next, we reflect on the role of observations in science and engineering. Why is the ability to collect them considered so important? From a philosophical perspective, we will see that observing and measuring are less objective than they might initially appear. At the same time, adopting this critical perspective highlights professional skills that are essential in practice: documenting work clearly, assessing data critically, and ensuring that observations are robust and fit for their intended purpose.

We then turn to the practical side. First, we outline the principal stages in designing an observation campaign. What does this process involve, and which decisions must be made? While each campaign is unique in terms of data type and measurement conditions, certain decisions are almost always required:

- Which properties or quantities should be observed?

- Which instruments are most appropriate?

- How and where should the observations be conducted (procedures and survey design)?

- Who will carry out the observations?

Second, we focus on the execution of the observation campaign. Here, we identify generic components and illustrate how these can influence the quality of the data obtained. 

## Terminology

Clear and consistent terminology is essential to avoid misinterpretation and miscommunication. This section introduces key terms that will be used throughout the learning line. Sect. "Measurements, Observations, and Data" defines terminology used in connection with measurement and observation and explains how measurements, observations, and data are distinguished. Sect. "Uncertainty" introduces the concept of uncertainty, with an emphasis on measurement uncertainty. Here we explain why all measurements are inherently uncertain and define the main terms used to quantify and analyse uncertainty.

It is important to note that terminology is not always used uniformly—neither across the various disciplines within EC&amp;T, nor even within one. While we adopt specific definitions for the purposes of this course, you should remain aware that others may use slightly different ones. To ensure a reliable foundation, we rely on established references such as the International Vocabulary of Metrology – Basic and General Concepts and Associated Terms (VIM) (JCGM 200, 2012), as well as standards provided by the Open Geospatial Consortium (OGC, https://www.ogc.org/).

### Measurements, Observations, and Data

So far, we have used the terms data, observations, and measurements without defining them precisely. In this section, we clarify how they relate to one another by presenting them as a hierarchy: from measurements to observations to data, with each level encompassing a broader scope. Every measurement is an observation, and every measurement and observation is a form of data. The reverse does not necessarily hold: not all observations are measurements, and not all data originate from observations. We therefore begin with the most specific level—measurements—and proceed step by step to the broader categories of observations and data. 

#### Measurements

According to the VIM, measurement is the “process of experimentally obtaining one or more quantity values that can reasonably be attributed to a quantity”. A quantity, in turn, is defined as a “property of a phenomenon, body, or substance, where the property has a magnitude that can be expressed as a number and a reference”.

The following notes apply to the definition of measurement. First, measurement applies only to properties that can be expressed quantitatively—not to nominal properties such as colour names or categories. Second, measurement always involves either comparing quantities or counting entities. And third, measurement presupposes a clear description of the quantity, an agreed measurement procedure, and a calibrated system that operates under specified conditions.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Scales of Measurement}$

Scales of measurement refers to how data values are defined, categorised, and interpreted. The framework most used derives from psychologist Stanley Stevens, who distinguished four scales: nominal, ordinal, interval, and ratio. These scales determine not only how quantities are represented as data, but also which descriptive and inferential statistical methods are valid. Table 1 provides an overview. 
</p>
</div>

Table 1: Definition of measurement scales.

| Scale | Definition | Example |
| :---: | :---: | :---: |
| Nominal | Distinct classes or categories; no inherent order. | Land cover types: forest, grassland, urban, water|
| Ordinal | Categories with meaningful ranking, but unequal differences between ranks. | Soil erosion risk levels: very low, low, moderate, high, very high |
| Interval | Differences between values are meaningful and consistent, but zero is arbitrary. | Temperature in °C or °F|
| Ratio | All mathematical operations are valid; zero means “none of the quantity”. | Temperature in K; precipitation amount in mm; ice sheet mass in gigatonnes|

Let’s explore this further by starting with the concept of quantity. A quantity is a property of something—physical, chemical, or biological—that can be expressed as a number together with a reference. The reference may be a unit of measurement, a procedure, a reference material, or a combination of these. 

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Reference}$

Imagine my American colleague and I each measure the height of our desks at home. I might report a magnitude of 0.9, while my colleague reports 3. To compare these results, we need two additional pieces of information: (1) the unit used (metres versus feet) and (2) how the height was measured. For a fair comparison, both of us should have measured the perpendicular distance from the tabletop to the floor.
</p>
</div>

According to the VIM, quantity is a generic concept that can be made more specific. In the International System of Units (SI), seven base quantities are defined: length (m), mass (kg), time (s), electric current (ampere), thermodynamic temperature (kelvin), amount of substance (mole), and luminous intensity (candela). More specific examples of the length-type quantity include diameter, circumference, or wavelength. From these base quantities, countless derived quantities can be constructed. 

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Examples of Derived Quantities}$

Density (mass/volume [itself the third power of length]), velocity (length / time), and pressure (force applied perpendicularly to a surface per unit area, derived from mass, length, and time).
</p>
</div>

With these foundations, we return to the definition of measurement itself. A measurement is the process of experimentally obtaining one or more values of the measurand—the specific quantity intended to be measured. The outcome is the measurement result, consisting of the measured value(s) together with essential information such as the associated measurement uncertainty. These measured values are often referred to simply as measurements.

#### Direct and Indirect Measurements

Measurements can be classified as either direct or indirect (Crowder et al., 2020). A direct measurement is one in which the measurand’s value is read directly from the instrument. Conceptually, this can be represented as:

y = Actual (i.e., true value) + Bias + εA + εB.

In this expression, the measured value (y) of the measurand is equal to the actual value plus a potential constant bias term, plus εA and εB, the Type A and Type B random error terms, respectively. Note that even a direct measurement becomes indirect once corrections are made for environmental or instrumental effects. In practice, very few measurements remain purely direct.

An indirect measurement is one in which the value of the measurand is obtained by measuring other quantities that are functionally related to it. Most real-world measurements fall into this category. An indirect measurement model may be expressed as:

Y = f(X1, X2, . . . , XN),

where Y is the measurand and Xi refers to the input quantities needed to obtain the result. These may include measured values, corrections, or influence quantities. Each has its own uncertainty, which propagates into the uncertainty of Y. The function f may rest on established physical laws or be determined experimentally, but in either case all significant sources of variation must be incorporated for the result to be meaningful. 


<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Measuring distance}$

Using a ruler or tape measure gives a direct measurement: the length is read directly from the instrument’s scale. Yet even this simple case becomes indirect once corrections are applied (e.g., for thermal expansion of the ruler). In that case, the measurand is no longer obtained solely by reading the scale, but through a measurement model that combines the observed length with a correction factor.

By contrast, a total station measures distance indirectly. It records the travel time of a laser pulse or the phase shift of a modulated electromagnetic signal. Combined with other input quantities—such as the speed of light and corrections for environmental factors like temperature, humidity, and atmospheric pressure—the distance is inferred from the measurement model.

````{figure} ../figures/part-a_mapping_1.jpg
---
name: mapping1
width: 60%
align: center
---
Image obtained from Christiaan Tiberius.
````
</p>
</div>

#### Observations

The term observation is broader than measurement. Rinne et al. (2023) define observation as “an act carried out by an observer to determine the value of an observable property of an object (feature of interest) by using a procedure, with the value provided as the result”. The result of an observation may be quantitative (a number) or qualitative (a category or description).

The feature of interest does not only refer to physical objects; it may also be a phenomenon. Put simply, it is the ‘thing’ under study. For example, the feature of interest might be the atmosphere, with the observable property being its temperature. Or it might be a rock outcrop, with the property of interest being the rock type.

In this view, a measurement is a particular type of observation—one that yields a numerical result. Observations in general, however, may be either quantitative or qualitative.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Observation versus Measurement}$

Recording that the weather was cloudy on 29 August 2025 at 10:00 UTC is an observation but not a measurement. In contrast, reporting that the air temperature was −5.2 °C at the same time is both an observation and a measurement.
</p>
</div>


#### Data

In general, data is a broader term than measurements and observations. It refers to any collection of symbols, numbers, or information—not necessarily originating from an instrument. For example, a spreadsheet with survey results, the output of a climate model, or even text documents can all be considered data.

In Earth Sciences, however, the term is often used in a narrower sense, especially when linked to a specific measurement technique (e.g., GNSS data or LiDAR data). In such cases, data may refer to raw measurements, to the complete set of information acquired with the measurement system, or to processed and derived products (e.g., GNSS-derived positions or LiDAR-derived digital elevation models).

### Uncertainty

#### A Multifaceted Concept

Uncertainty, an inherent component of any dataset (including observations and measurements), is a multifaceted concept comprising many aspects. To illustrate this, consider MacEachren et al.’s (2005) still incomplete typology of geospatial information uncertainty:

````{figure} ../figures/part-a_mapping2.png
---
name: mapping2
width: 60%
align: center
---
````

Although formulated to describe the uncertainty of geospatial information, many of these aspects—if not all—apply equally to the data that served as the source of the information. Awareness of each is required to draw meaningful and actionable insights from a dataset. To appreciate why such awareness matters, consider a few concrete examples:

- Completeness: A geological survey may only cover part of a region. Maps derived from it are therefore incomplete, and extrapolation into unsampled areas introduces additional uncertainty that must be accounted for when making decisions about resource exploration or hazard assessment.

- Currency: Land-cover maps created from remote sensing data acquired two decades ago may be an unreliable basis for present-day studies of sustainable biomass.

- Credibility: Crowd-sourced environmental reports (e.g. species sightings or air-quality observations) may contain valuable information, but their reliability depends heavily on the training, expertise, and motivation of contributors.

- Subjectivity: Rock classifications in the field may vary between geologists, depending on training or interpretation of borderline cases. Recognising this subjectivity is essential when integrating multiple observers’ records.

In the remainder of this section, we focus on uncertainty in measurements. 

#### An Unavoidable Fact

Every measurement carries uncertainty. Awareness of this associated uncertainty is essential for making informed decisions. Teunissen (2003) identifies four reasons why measurements will always remain uncertain to some degree, regardless of efforts to improve instruments, train observers, or better control measurement conditions:

1. Mathematical certainty relates to abstractions, not to physical, technical, or social reality. Mathematical models may describe phenomena and relationships drawn from experience, but there will always be a fundamental difference between a model and the real world.

2. Measurement conditions can be controlled to some extent in the laboratory, but in nature they are uncontrollable and only partially describable.

3. Even with improved methods and instruments, uncertainties remain because of the issues outlined in (1) and (2)—only their level may change.

4. Measurements are made with a purpose. Depending on that purpose, some uncertainty may be perfectly acceptable. Since better instruments and methods usually cost more, one must always ask whether the reduction in uncertainty is worth the extra expense.

In short, it is both fundamentally and practically impossible to achieve absolute certainty in measurement. At the same time, such certainty is rarely required. Measurements are performed to obtain quantitative information that is sufficiently accurate and affordable for a given purpose.

#### Basic Terminology

To analyse measurements and their uncertainty, consistent terminology is required. The VIM provides precise definitions of many terms that we also use in our field. The VIM uses what it calls the ‘Uncertainty Approach’ to measurement terminology. The ‘Error Approach’ was the historical norm prior to publication of the VIM and was used to estimate a value as close as possible to a single true value. The Uncertainty Approach does not attempt to determine a single true value; instead, it assumes that information from the measurement permits an interval of reasonable values. The uncertainty approach is the preferred terminology for use by metrology organizations. Below are simplified definitions of some commonly used terms, based on the VIM (JCGM 200, 2012) and Crowder et al. (2020). 

Measurement Accuracy – Accuracy describes how close a measurement result is to the (unknown) true value. Because the true value can never be known exactly, accuracy cannot be determined quantitatively.

Measurement Precision – Precision describes the degree of agreement among repeated measurements of the same quantity. High precision means the measurements cluster closely together; low precision means they are more dispersed. Precision does not imply correctness—repeated measurements may be very consistent yet still biased.

Resolution (Instrument) – Resolution represents the smallest change at which the measured value can be read or recorded. For example, a tide gauge might report sea level to the nearest millimetre, while a digital thermometer might display to the nearest 0.1 °C. Resolution almost never indicates overall accuracy or total uncertainty, but can be a contributor.

Measurement Repeatability – Repeatability refers to the agreement between repeated measurements taken under nearly identical conditions: same operator, same instrument, same procedure, and within short time intervals (hours to days).

Measurement Reproducibility – Reproducibility refers to the agreement between measurements taken under different conditions: different operators, instruments, and/or procedures. It is often assessed over longer time intervals. In Earth Sciences this could mean, for example, comparing sea surface temperature from different satellites, or groundwater level measurements from independent surveys.

##### The Error Approach (Discouraged)

Although widely used, the terminology associated with the Error Approach is discouraged in contemporary metrology.

Measurement Error – The difference between a measured value and the true value. Since the true value is never known exactly, the actual error is also unknown. For this reason, metrology prefers to speak in terms of uncertainty rather than error.

Systematic (Measurement) Error – Predictable, repeatable effects that shift measurements in one direction (e.g. a temperature sensor that consistently reads 0.2 °C too high). If known, these systematic errors can be corrected. Again, since the true value can never be known, use of the term ‘systematic error’ is discouraged unless referring to a quantitative, known offset that can be corrected.

Random (Measurement) Error – Unpredictable variation between individual measurements, reflecting the inherent variability of the measurement process or system (caused by, e.g., sensor noise or atmospheric turbulence). Random errors cannot be corrected but can be characterised statistically.

##### The Uncertainty Approach (Preferred)

The Uncertainty Approach assigns a range of likely values that could be attributed to the measurand based on the finite amount of knowledge of the measurement equipment and process.

Measurement Uncertainty – A non-negative parameter that characterizes the dispersion of the quantity values being attributed to a measurand, based on the information used (JCGM 200, 2012). Put simply, uncertainty describes the range within which the true value of the measurand is believed to lie, given all the available information. It includes contributions from the instruments and standards used to make the measurement, the measurement process, the measurement model, and definitional uncertainty. Measurement uncertainty always includes Type A and Type B evaluations of measurement uncertainty:

- Type A uncertainty evaluation: Based on statistical analysis of repeated observations taken under the same conditions (e.g. the spread of repeated temperature readings).

- Type B uncertainty evaluation: Based on information other than immediate repeated measurements. Sources include historical data, calibration certificates, manufacturer specifications, and reference data (e.g., from handbooks). Type B captures sources of variation not evident in short-term experiments, such as long-term sensor drift or systematic bias. 

Both Type A and Type B evaluations may involve statistical methods, but the key distinction is the source of information: Type A uses current, repeated measurements; Type B relies on external or prior information. Care must be taken to avoid ‘double counting’ uncertainties when combining the two.

Total Measurement Uncertainty – The total measurement uncertainty combines both Type A and Type B evaluations. Since the true value is unknown, it may lie anywhere within the reported uncertainty interval—or even outside it, depending on the chosen level of confidence (i.e., the probability that the constructed uncertainty interval will contain the true value).

````{figure} ../figures/part-a_mapping3.jpg
---
name: mapping3
width: 60%
align: center
---
Illustration summarizing terms for the preferred Uncertainty Approach to measurement terminology. The measured value will fall within the total uncertainty above or (not shown) below the true value. Taken from: Crowder et al. (2020).
````

Definitional Uncertainty – Component of measurement uncertainty resulting from the finite level of detail in the definition of a measurand. In other words, it is the minimum uncertainty you can have in any measurement of a given quantity, regardless of instrument precision. Any change in the descriptive detail of what you&apos;re measuring will lead to a different definitional uncertainty. Note, sometimes this is referred to as ‘idealization accuracy’. 


<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Example}$

The Length of a River – Suppose you are asked to measure the length of a river. The result will always contain some uncertainty because the definition ‘a river’ is not perfectly specific. Where exactly does the river begin and end? Do you follow every meander, or measure a straight line from source to mouth? This ambiguity in the definition itself creates uncertainty, even before you start measuring. 
</p>
</div>

````{figure} ../figures/part-a_mapping4.jpg
---
name: mapping4
width: 60%
align: center
---
Photo by Sindre Fs: https://www.pexels.com/photo/aerial-photography-of-water-beside-forest-during-golden-hour-1144176/
````

## To Measure Is to Know...!?

Sayings such as “to measure is to know”, “if you cannot measure it, you cannot improve it”, and “what gets measured gets done” underscore the crucial role of observations in everyday life. Observations underpin much of our knowledge and guide decision-making across nearly all areas of modern society. 

The same applies in the EC&amp;T domain. Examples can be found in Mulhern (2020), Kimball (2024), Hijma et al. (2025), Pearson (2025), ter Voorde (2025), and Zheng et al. (2025). At a higher level, within EC&amp;T we rely on observations to describe and characterise natural systems, monitor changes, forecast future states, develop and validate models, inform design and interventions, and support resource management, risk assessment, and policy. Yet, while their importance is evident, the nature of observations is far from straightforward. This section reflects on how observations are shaped by theories, instruments, and social values—and what that implies for the knowledge we derive from them.

### Beyond “Neutral Facts”: What Philosophy of Science Teaches Us

These familiar sayings suggest that observations are pure, objective snapshots of reality—a neutral basis for judging theories. In practice, however, the relationships among observation, fact, and theory are more complex.

An observation is akin to a photograph: not reality itself, but a representation of it. The photographer decides what to frame, where to focus, when to press the shutter, and which lens to use; afterwards, the image may be cropped, color-corrected, or sharpened.

Similarly, (scientific) observations are shaped by the observer’s background, the instruments used, and the processing applied to the data. To make meaningful use of them, we must not only know how to collect observations but also how to interrogate their provenance, context, and limitations. Inspired by Boyd and Bogen (2025), this section introduces ten considerations—grouped into three themes—that clarify the nature and value of observations. 

#### The Observer Is Never Neutral

Our minds are not empty buckets we fill with facts. They come equipped with theories, values, and expectations that act as filters. These filters are useful—they help us make sense of what we see, allowing us to recognize patterns instead of noise. A geologist, for example, looking at a rock outcrop does not just see ‘rock’, but evidence of tectonic forces (theory-ladenness). An environmental agency deciding to monitor nitrogen dioxide in cities but not in rural areas is makes a choice informed by public health priorities (value-ladenness).

Theory- ladenness and value- ladenness are two of the four considerations under this theme. All four are listed below with brief explanations:

1. Theory-Ladenness of Observation – Observations are never theory-free. What we look for, how we classify it, and even what we notice depend on the theoretical and conceptual frameworks we already hold. For example, an oceanographer viewing a satellite map of sea surface temperatures does not merely see random patches of warm and cold water. They see features like the Gulf Stream or an El Niño event because their knowledge of ocean circulation theory allows them to recognise such patterns. A layperson would simply perceive colours on a map.

2. Value-Ladenness of Science – Choices about what, when, and how to measure are influenced by social, political, and/or ethical values. For instance, a government agency with limited resources for monitoring PFAS (i.e, a ‘forever chemical’) contamination might decide to test groundwater near industrial parks (an economic value), in affluent suburbs (a political value), or in low-income communities known to be disproportionately affected (an environmental justice value). The decision where to measure is guided by societal values.

3. Bias and Selectivity – Observers may unconsciously bias their data by seeing what they expect to see or by ignoring inconvenient signals. For instance, a researcher counting sediment layers (varves) in a lake core to reconstruct past rainfall might have a hypothesis predicting a drought 500 years ago. When faced with thin or ambiguous layers in the part of the core corresponding to that period, they may be more inclined to classify them as ‘missing’ or ‘compressed’, thereby reinforcing their expectation of a dry period. Such risks can be mitigated through replication, independent cross-checks, pre-specified procedures, and automation.

4. Semantic Ambiguity – Observational terms may vary in meaning across communities or contexts. Words such as ‘heat’, ‘pollution’, or ‘sea level’ can carry different interpretations. It is therefore essential to define terms operationally and document them clearly. For example, ‘sea level’ may refer to the instantaneous height, a daily average, or a 30-year climate mean. Without a clear operational definition, the term becomes unfit for rigorous analysis.

Note: the danger is not in having a framework, but in being unaware of it. Good science requires constant reflection: Why am I measuring this? Am I seeing what is really there, or what I expect to see?

#### The Journey of Data

A measurement is not a direct copy of reality; it is the result of a long chain of events. A satellite altimeter, for example, does not measure sea level directly. It records the reflected power of a radar pulse as a function of time, producing a waveform. This waveform is used to estimate the pulse’s travel time, which is converted into a range. Corrections are then applied for instrumental effects and atmospheric propagation delays—often themselves model-based. The corrected range is finally transformed into an estimate of sea level. From raw signal to a value in a dataset, the journey is long indeed.

This does not render the data unreliable, but it makes provenance—the record of where the data came from and how it was treated—critical. Metadata are therefore the most critical component of any dataset. Without it, data become just numbers that can be misinterpreted or misused. The following considerations apply:

5. Instrument and Context Dependence – Instruments deliver signals conditioned by calibration, assumptions, and embedded theories. Context (site, operator, conditions) also matters. Measuring wind speed with a handheld anemometer on the rooftop of a tall building yields data fundamentally different from that obtained with a research-grade sonic anemometer mounted on a 10-metre mast in open, flat terrain. Instrument and context are inseparable from the measurement.

6. Incomplete or Misplaced Observation – Observations are inevitably partial—they are made at specific times, places, and scales. Poor sampling strategies distort understanding. For example, measuring a river&apos;s discharge once on a dry summer day paints a very different picture than hourly measurements during a rainy week.

7. Processing and Mediation of Data – Data are rarely ‘raw’. They undergo conversion, correction, interpolation, and other processing. Each step may add insight but can also introduce potential distortion. Satellite imagery, for example, is corrected for geometric distortions caused by satellite motion, scanning methods, and atmospheric effects. Thus, the images used for analysis are the outcome of significant processing and mediation.

8. Reuse and Provenance – Data are often repurposed. Without comprehensive metadata (documenting methods, location, calibration, uncertainty, etc.), reused data can mislead. For example, a student downloading a historical dataset of air temperatures in a particular city to study the urban heat island effect might be unaware that the weather station was moved in 1950 from a leafy park to the concrete surroundings of a nearby airport. The apparent ‘warming trend’ they detect is partly explained by this undocumented change of location.

#### How Observations Build Knowledge

A single observation is not sufficient to prove a theory. Observations act more like clues in a detective story: they constrain possibilities, strengthen some hypotheses, and challenge others. A discordant result may point to an instrument fault, an invalid auxiliary assumption, or perhaps a genuinely new phenomenon. The relationship between observation and theory is therefore one of negotiation, not a simple true/false test.

Objectivity in science is not a perfectly detached ‘view from nowhere’. Rather, it is a collective achievement, emerging when scientists with different perspectives independently test, replicate, and critique one another’s work and eventually reach a consensus. Knowledge is robust not because it rests on a single flawless observation, but because it survives collective, critical scrutiny. The following considerations apply:

9. The Epistemic Status of Observations – Observations do not automatically prove or disprove a theory; they serve as evidence that constrains theories, always in conjunction with other assumptions. Suppose an ice core reveals a sudden, anomalous spike in methane 1,000 years ago. This single anomaly would not immediately overturn our understanding of the global carbon cycle. Instead, scientists would interrogate the observation: Was it contaminated? Could there have been an instrument error? Might it reflect a local event, such as a subglacial gas release, rather than a global signal? In such cases, an observation functions as a clue that demands further investigation, not as a standalone fact that topples a theory.

10. Inter-Subjectivity and Objectivity – Observations gain strength through independent reproduction and convergence across methods, teams, and contexts. Objectivity arises from communal checks and balances. The scientific consensus on global warming is considered objective not because it comes from one perfect thermometer, but because thousands of independent research teams, using different instruments (satellites, ocean buoys, weather stations), different analytical methods, and different models, all converge on the same basic conclusion. Objectivity is achieved through this communal verification and cross-checking.

## Acquiring Measurements

### From a Problem Statement to a Measurement Plan

From here, we shift to a more practical perspective. How do we decide what to observe (i.e., the measurand[s]), which instrument to use, and how to design the measurement campaign? What does a typical workflow look like, from a user’s problem to the point where we can begin collecting data?

There is no universal recipe, but a useful framework comes from the structured way in which space agencies such as ESA and NASA design satellite missions. Their process provides a logical path from a high-level goal to a detailed technical plan. We can adapt its four main steps:

1. Defining User Requirements – What does the user need to know?

2. Translating to Observation Requirements – What specific data will answer the user’s question?

3. Defining System Requirements – How will we collect those data?

4. Formulating a Calibration and Validation (Cal/Val) Plan – How will we prove our data are reliable?

Although most EC&amp;T projects are less formal, following these steps helps ensure that the final data are fit for purpose. It is crucial to recognize that while these steps are presented sequentially, the process is often iterative in practice. For instance, you might discover in Step 3 that the ideal measurement system is prohibitively expensive. This would force a return to Step 2 to relax the observation requirements, possibly after renegotiating the original user requirements from Step 1. This back-and-forth is a core part of engineering, balancing what is desired with what is feasible. 

In the following, we will elaborate on each step. To make it tangible, we will follow a hypothetical but realistic scenario through all four steps: assessing the flood risk for the coastal community of &apos;Seaside Town&apos;.

#### Step 1 – Defining User Requirements

This first step is about understanding the core problem from the user&apos;s perspective. What do they want to know? What problem do they need to solve? A key insight here is that user requirements are almost never formulated in terms of ‘measurable quantities’. Instead, users are interested in concepts such as risk, safety, impact, or suitability—things we cannot measure directly with an instrument. 

Key questions to ask at this stage include: What does the user want to know? Why do they need it? Who will use the information? When is it needed, and how often? Answering these precisely lays the essential foundation for the project.

A side note: users are not always known in advance. Observations acquired for one purpose may later prove valuable for entirely different ones.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Assessing flood risk in Seaside Town }$

In our scenario, the ‘user’ is the Seaside Town city council. The council wants to update its flood defence plan. Specifically, they need to know which residential areas are at risk during a 1-in-100-year storm surge event. The purpose is to prioritise infrastructure upgrades.
</p>
</div>

#### Step 2 – Translating to Observation Requirements

The next step is to translate the abstract user need (‘risk’) into concrete, observation requirements. This involves identifying the quantities that, when measured, will allow us to answer the user’s question, together with the required spatial coverage, spatial resolution, temporal coverage, and data quality.

(The theory allowing us to determine the required resolution will be covered in the second year of the program, but the key point is that we must define how good our data needs to be to be useful.)

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Assessing flood risk in Seaside Town }$

Determining flood risk requires knowing two primary things: the height of the land and the height of the water level during a 1-in-100-years storm surge event. This translates to:

Measurands:
- Ground surface elevation (topography)

- Predicted peak water level during a 1-in-100-year storm surge

Specifications:
- Spatial coverage: Entire municipal area of Seaside Town

- Spatial resolution: Sufficient to identify houses and streets (around 1 m)

- Temporal coverage: Elevation data should be recent, as construction can alter the landscape

- Accuracy: The vertical accuracy of the elevation data is critical. If we need to know whether a 50 cm high barrier will protect a neighbourhood, the ground elevation must be known with an accuracy significantly better than that, for example, to within ±10 cm
</p>
</div>


#### Step 3 – Defining System Requirements

With the observation requirements in place, we can now define how to obtain the data. This involves selecting or designing the measurement system, defining the measurement process, and developing a measurement plan, all while considering practical constraints.

One key decision is whether to collect the data in situ—for example, because of the required accuracy or temporal resolution—or whether remote sensing techniques will suffice, where measurements are taken without direct contact with the object of study. In-situ methods raise questions of access: is the location reachable, and are we permitted to install instruments there? For long-term monitoring, we must also decide how to retrieve the data—periodically on site, or via real-time transmission.

If remote sensing is chosen, the next question is which platform to use. Satellites offer broad coverage but are constrained by limits on spatial resolution. Aircraft and UAV campaigns present other challenges: gaining permission to fly, determining the appropriate altitude to achieve the required accuracy and resolution, and correcting for platform movement, among others.

This stage is ultimately about making informed choices and managing trade-offs. The ‘perfect’ measurement system may be too costly, too slow, or may not exist at all. In any case we must demonstrate—at least in theory—that the proposed system can meet the observation requirements.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Assessing flood risk in Seaside Town }$

How can we measure ground elevation with 1-meter resolution and ±10 cm vertical accuracy over the whole town?

System Requirements (not complete):
- Instrument &amp; Method: We chose to extract the elevation model using an airborne LiDAR (Light Detection and Ranging) system. An Airborne LiDAR system (ALS) integrates a laser scanner, a Global Navigation Satellite System (GNSS), and an Inertial Navigation System (INS). It is a commonly used method for this application. The distance between the scanner and the target is calculated based on the time interval between the laser pulse being transmitted and its reflection being received. By combining this with the position and attitude of the laser scanner as observed by the GNSS and the inertial measurement unit (IMU, module of the INS), the 3D spatial coordinates of the target are calculated.

- Procedure: Depending on the characteristics of the laser scanner, we need to fly at a certain altitude. Together with the swath width covered by the laser scanner, this is key input to design the flight plan.

- Constraints &amp; Trade-offs: Airborne LiDAR surveys are expensive. Budget limitations may force compromises, such as lower resolution or reliance on older datasets. This illustrates the classic engineering trade-off between cost, quality, and time.
</p>
</div>

#### Step 4 – Calibration and Validation (Cal/Val) Plan

Finally, having a system is not enough—we must prove that it works. The Cal/Val plan addresses this by asking: How will we demonstrate that our system and data meet the required accuracy? This may also be an ongoing task. For example, if we conduct a monitoring over a long time span, it is not sufficient to proof at the start that the system performs. Indeed, instrument performance can degrade over time. 

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Assessing flood risk in Seaside Town }$

Our system requirement is to deliver an elevation map with ±10 cm vertical accuracy. How do we prove we achieved this?

Cal/Val Plan (not complete):
Calibration: A primary source of systematic error is angular misalignment between the mounting axes of the laser scanner and the IMU, known as boresight misalignment. This can be compared to a poorly adjusted sight (the IMU) on a rifle (the laser scanner): no matter how carefully you aim, the result will always be systematically off target. Another common source is the physical offset between the laser scanner and the GNSS antenna, referred to as lever-arm offsets. To address these, calibration is required. Several methods are available—for example, the approach described by Tian et al. (2022).

Validation: After the survey, ground-truth measurements are collected using GNSS at 30–50 easily identifiable points in Seaside Town (e.g. road intersections). Validation is performed by comparing these elevations with the ALS-derived values.
</p>
</div>

### The Observation Campaign

As noted in the introduction, this chapter does not focus on the acquisition of specific types of observations. Nor do we review the full range of observational campaigns carried out across the broad field of Earth, Climate and Technology (EC&amp;T). That is somewhat regrettable, as each campaign tells its own story. Many of us have been taken to remarkable places through such work—from nearby sites to the polar regions. Each time, things unfolded differently. Plans had to be adapted. Carefully designed measurement setups sometimes proved impractical in the field. Sites turned out to be inaccessible. Instruments that had worked perfectly in the office failed while being in the field. The list could go on. Ultimately, the experience of conducting an observational campaign is easier to live through than to describe.

In this section, therefore, we identify the components that are common to most observational campaigns (if not all) conducted in the EC&amp;T domain. Our focus is on how these components influence the quality of the data obtained. We distinguish the following:

1) The Observer(s) – The individual(s) conducting the measurements and in-field quality control. This component highlights the human element and the importance of in-field documentation. The observer is not a passive recorder but an active participant, capable of introducing errors or performing crucial quality control. Operator skill determines the extent of human error (blunders) and the consistency with which procedures are followed. Technical knowledge of the instruments can be decisive for the success of a campaign: for instance, an observer familiar with their instrument may be able to adjust settings or even perform emergency repairs.

2) Measuring System – The complete set of instruments and associated devices that produce the measurements (see JCGM 200 [2012], section 2.9). Wherever possible, instruments should be tested prior to deployment. Yet even then, failures may occur—during transport, installation, or operation—potentially affecting performance. Environmental conditions such as terrain, humidity, or temperature can also influence how well an instrument functions.

3) Measurement Procedure – The documented sequence of actions to be followed by the operator to ensure consistency and repeatability (e.g., an ISO standard or a project-specific protocol). Procedures cannot eliminate all sources of variability, and poorly designed protocols may themselves introduce uncertainty. A particular challenge arises when operators deviate—consciously or unconsciously—from the prescribed procedure, for example due to deteriorating weather or time pressure. However legitimate the reason, such deviations can invalidate the measurements.

4) Measurement Platform – The vehicle or structure that carries the system (e.g., satellite, aircraft, drone, vessel, tripod, or even a person). Platform stability and positioning accuracy directly affect the geometrical quality and spatial reliability of the measurements. For example, if a survey vessel lacks a calibrated motion sensor while conducting a multibeam echosounder survey, the inability to correct for roll and pitch will produce significant artefacts in the resulting seafloor map.

5) Survey Design – Specifies where (area of interest and sampling strategy: transect lines, grid points, random samples) and when (time of day, duration, frequency) the measurements are taken. In practice, many factors can lead to deviations from the original design: sites may prove inaccessible, unsuitable for instrument deployment, or unsafe; flight paths may need to change due to wind; individual measurements may take longer than expected. Such adjustments can compromise the intended sampling strategy, reducing the representativeness and completeness of the dataset.

6) Data &amp; Metadata Management – The logging, storage, back-up, and documentation of both data and metadata. This includes field logs detailing, for example, antenna height, start and end times, and any problems encountered. Such documentation is essential for traceability and post-processing; without it, errors may become impossible to correct.

7) Measurement Environment – The external conditions (e.g., weather, temperature, water column properties, terrain characteristics) that can influence the measurement system, the platform, or even the phenomenon being measured. These factors are often the hardest to control. The environment is a primary source of both random and systematic disturbances: it may degrade instrument performance or alter the very property under observation, thereby affecting the validity of the data. For example, acquiring high-resolution aerial imagery on a day with scattered clouds will inevitably reduce image quality.

8) Logistics &amp; Safety - The supporting activities that make data acquisition possible. Although not part of the measurement chain itself, shortcomings here can compromise or even halt an entire campaign. Inadequate logistics or unsafe conditions can result in data gaps, incomplete surveys, or rushed measurements prone to error.

## References

Boyd, Nora Mills and James Bogen, &quot;Theory and Observation in Science&quot;, The Stanford Encyclopedia of Philosophy (Spring 2025 Edition), Edward N. Zalta &amp; Uri Nodelman (eds.), URL = &lt;https://plato.stanford.edu/archives/spr2025/entries/science-theory-observation/&gt;. 

Crowder, S., Delker, C., Forrest, E., &amp; Martin, N. (2020). Introduction to statistics in metrology. Springer International Publishing. https://doi.org/10.1007/978-3-030-53329-8.

Hijma, M.P., Bradley, S.L., Cohen, K.M. et al. Global sea-level rise in the early Holocene revealed from North Sea peats. Nature 639, 652–657 (2025). https://doi.org/10.1038/s41586-025-08769-7

Kimball, R. (2024, December 11). Satellite Science: How Earth Observation Data Furthers Our Understanding of the World. Planet. https://www.planet.com/pulse/satellite-science-how-earth-observation-data-furthers-our-understanding-of-the-world/

MacEachren, A. M., Robinson, A., Hopper, S., Gardner, S., Murray, R., Gahegan, M., &amp; Hetzler, E. (2005). Visualizing Geospatial Information Uncertainty: What We Know and What We Need to Know. Cartography and Geographic Information Science, 32(3), 139–160. https://doi.org/10.1559/1523040054738936

Mulhern, O. (2020, November 20). How Satellites Help Tackle Climate Change. Earth.org. https://earth.org/data_visualization/how-satellites-help-tackle-climate-change/

Pearson, J. (2025, August 11). Dateline survey lights up hot spot at US rare earths project. Business News. https://www.businessnews.com.au/article/Dateline-survey-lights-up-hot-spot-at-US-rare-earths-project

Rinne, I., Schleidt, K., van den Brink, L., Grellet, S., Portele, C., &amp; van Der Schaaf, H. (2023). OGC Abstract Specification Topic 20: Observations, measurements and samples (OGC 20-082r4). Open Geospatial Consortium. http://www.opengis.net/doc/as/om/3.0

ter Voorde, M. (2025, April 28). Satellieten lokaliseren nu ook kortdurende methaanuitstoot. De Ingenieur. https://deingenieur.nl/artikelen/satellieten-lokaliseren-nu-ook-kortdurende-methaanuitstoot

Teunissen, P.J.G. (2003). Adjustment theory. DUP Blueprint.

Tian, Yu, Zhao, Yibo, Lei, Shaogang, Ji, Chuning, Duan, Lei, Sedlák, Vladimír, Automatic Calibration Method for Airborne LiDAR Systems Based on Approximate Corresponding Points Model, Journal of Sensors, 2022, 4853419, 13 pages, 2022. https://doi.org/10.1155/2022/4853419 

Zheng, L., Shang, X., van den Broeke, M.R. et al. Rapid increases in satellite-observed ice sheet surface meltwater production. Nat. Clim. Chang. 15, 769–774 (2025). https://doi.org/10.1038/s41558-025-02364-4 JCGM 200: International Vocabulary of Metrology – basic and general concepts and terms (VIM), 3rd Edition, 2008 Version with Minor Corrections (2012) available at https://www.bipm.org/en/doi/10.59161/jcgm200-2012.