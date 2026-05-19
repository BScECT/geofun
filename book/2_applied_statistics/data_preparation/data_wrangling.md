# Data wrangling and cleaning

## What are tidy data?

Data formatting and cleaning is often the most time consuming step in a statistical or data analysis project. The concept of tidy data was developed to limit the effort spent cleaning data to get it ready for analysis ([Wickham, 2014](https://doi.org/10.18637/jss.v059.i10)). In tidy data:
  1. Each variable forms a column.
  1. Each observation forms a row.
  1. Each type of observational unit forms a table.

In contrast, in messy data:
  * Column headers are values, not variable names.
  * Multiple variables are stored in one column.
  * Variables are stored in both rows and columns.
  * Multiple types of observational units are stored in the same table.
  * A single observational unit is stored in multiple tables.

But tidy datasets are just a part of what constitute a robust digital culture: you also need all the infrastructure to store and be able to use them. This is codified by the [FAIR principle](https://www.go-fair.org/fair-principles), which are guidelines to make data (from [libereurope.eu](https://libereurope.eu/wp-content/uploads/2020/09/LIBER-FAIR-Data.pdf)):
  * Findable
    > Data and supplementary materials have sufficiently rich metadata and a unique and persistent identifier.
  * Accessible
    > Metadata and data are understandable to humans and machines. Data is deposited in a trusted repository.
  * Interoperable
    > Metadata use a formal, accessible, shared, and broadly applicable language for knowledge representation.
  * Reusable
    > Data and collections have a clear usage licenses and provide accurate information on provenance.

## How to tidy data?

In most cases, tidying a dataset requires reshaping the data and splitting multiple observations encoded into a single column. Many datasets are stored in a wide format (i.e., with many columns), because it limits the duplication of information and it is easier to read by humans, like in this tabular dataset showing the top ten solar-producing countries in Europe (data from [CBS](https://www.cbs.nl/en-gb/news/2023/24/46-percent-more-solar-energy-production-in-2022)):

| Land | 2022 (energy production (bn kWh)) | 2021 (energy production (bn kWh)) | 2020 (energy production (bn kWh)) | 2019 (energy production (bn kWh)) |
| :---------- | :--: | :--: | :--: | :--: |
| Germany     | 61.3 | 51.2 | 50.1 | 44.9 |
| Spain       | 31.9 | 25.6 | 19.7 | 14.3 |
| Italy       | 27.6 | 25.1 | 25.6 | 24.3 |
| France      | 19.0 | 14.8 | 13.4 | 11.0 |
| Netherlands | 17.7 | 11.5 |  8.8 |  5.3 |
| Turkey      | 15.0 | 13.4 | 11.3 |  9.4 |
| Poland      |  8.0 |  3.8 |  2.0 |  0.7 |
| Greece      |  7.0 |  5.1 |  4.4 |  4.0 |
| Belgium     |  6.8 |  5.6 |  4.9 |  3.5 |
| Hungary     |  4.6 |  3.8 |  2.4 |  1.4 |

But this format makes it more difficult to manipulate the data for analysis, modeling, and visualization, especially in an automated way. A long format (i.e., few columns but many rows) is then much more appropriate and matches the definition of a tidy dataset:

```{raw} html
<div style="width: 400px; height: 500px; overflow-y: auto; margin-bottom: 1em;">
```
| Land        | Year | Energy production (bn kWh) |
| :---------- | :--: | :----------: |
| Germany     | 2019 | 44.9 |
| Germany     | 2020 | 50.1 |
| Germany     | 2021 | 51.2 |
| Germany     | 2022 | 61.3 |
| Spain       | 2019 | 14.3 |
| Spain       | 2020 | 19.7 |
| Spain       | 2021 | 25.6 |
| Spain       | 2022 | 31.9 |
| Italy       | 2019 | 24.3 |
| Italy       | 2020 | 25.6 |
| Italy       | 2021 | 25.1 |
| Italy       | 2022 | 27.6 |
| France      | 2019 | 11.0 |
| France      | 2020 | 13.4 |
| France      | 2021 | 14.8 |
| France      | 2022 | 19.0 |
| Netherlands | 2019 |  5.3 |
| Netherlands | 2020 |  8.8 |
| Netherlands | 2021 | 11.5 |
| Netherlands | 2022 | 17.7 |
| Turkey      | 2019 |  9.4 |
| Turkey      | 2020 | 11.3 |
| Turkey      | 2021 | 13.4 |
| Turkey      | 2022 | 15.0 |
| Poland      | 2019 |  0.7 |
| Poland      | 2020 |  2.0 |
| Poland      | 2021 |  3.8 |
| Poland      | 2022 |  8.0 |
| Greece      | 2019 |  4.0 |
| Greece      | 2020 |  4.4 |
| Greece      | 2021 |  5.1 |
| Greece      | 2022 |  7.0 |
| Belgium     | 2019 |  3.5 |
| Belgium     | 2020 |  4.9 |
| Belgium     | 2021 |  5.6 |
| Belgium     | 2022 |  6.8 |
| Hungary     | 2019 |  1.4 |
| Hungary     | 2020 |  2.4 |
| Hungary     | 2021 |  3.8 |
| Hungary     | 2022 |  4.6 |
```{raw} html
</div>
```

Converting a dataset like the one above, where the variable *year* is originally encoded as columns, to a wide format is called melting. You will find more examples of messy datasets and of their tidy counterparts in the [original paper describing tidy data](https://doi.org/10.18637/jss.v059.i10).

## What is data wrangling?

Data wrangling, also called data preparation or data munging, is the overall process of cleaning, structuring, and transforming raw, sometimes messy, data into a format more appropriate and valuable for downstream tasks, may they be analysis, modeling, visualization, or communication. Tidying a dataset is then often the first step of this process, along with storing that dataset in an appropriate format. But more steps are usually required.

Data wrangling often happens during exploratory data analysis, because this is when issues with the dataset structure and with the data themselves become visible. So data wrangling benefits greatly from data visualization.

## How to clean and transform data?

(2:data_wrangling:missing_data)=
### Missing data

Missing data occur when no value is stored for a variable in an observation. The easiest way to encode missing data in a file is to leave a blank space. But this is not a standard practice, and people have developed many different ways of encoding them: none, null, -99, -999, -9999 (etc.), 0, -1, \*, \*\*\*, and many more. That missing data are sometimes encoded as numbers can lead to huge issues in analysis, so always make sure to check the metadata to see the proper encoding. If there are no metadata or nothing is mentioned, plot the data and check for any nonphysical values (e.g., a negative concentration).

(2:data_wrangling:outliers)=
### Outliers

An outlier is a datum that deviates clearly from the rest of the data. They can come from:
  * A device malfunction.
  * A transcription error.
  * A sample contamination.
  * A too small sample size.
  * A rare event.
  * A change in system behavior.
  * etc.

So from measurement errors, lack of measurements, or because the variables of interest have heavy-tailed distributions.

Some statistical estimators are sensitive to outliers (e.g., the mean), so they can perturb analyses and many approaches have been developed to identify them. The most famous is Tukey's fences, which define outliers as values outside of the range:

$$
    [Q_1 - k(Q_3 - Q_1), Q_3 + k(Q_3 - Q_1)]
$$

Where $Q_1$ is the lower quartile, and $Q_3$ the upper quartile, and $k$ a non-negative constant. This is the approach used to highlight outliers in [box plots](1:descriptive_statistics:box_plot), often with $k = 1.5$.

But should you remove outliers identified with such approaches (and even remove outliers in general)? If they are related to an experimental error you can, but it is always better to correct the value when possible (e.g., by running the experiment again). Removing an outlier just because it is an outlier is highly controversial, because they can still highlight some characteristic of the population. It is better to turn to more robust estimators (e.g., using the median instead of the mean).

### Transformations

Transformations turn the original data into more useful inputs for statistical modeling. This mainly means turning some variables into numerical values or making sure the data fulfill the assumptions of some statistical method.

For this subsection, let's assume that we have a sample of $n$ observed values $\{x_1, x_2, ..., x_n\}$ of a variable $X$.

(2:data_wrangling:standardization)=
#### Standardization

Standardization transforms a numerical variable $X$ into a variable $Z$ with a mean of 0 (i.e., it is centered) and a standard deviation of 1 (i.e., it is reduced):

$$
    z_i = \frac{x_i - \overline{x}}{s_X} \qquad \forall i \in [1, n]
$$

Where $\overline{x}$ is the mean of the sample and $s_X$ its standard deviation. It is mainly used on continuous variables to make variables with different units comparable. Otherwise, variables with larger values could have a disproportionate effect in some statistical analyses.

(2:data_wrangling:log_transformation)=
#### Log transformation

Logarithm transformation transforms a numerical variable $X$ into a variable $Y$ using a logarithm, sometimes of base 10 but often of base $e$:

$$
    y_i = \ln(x_i) = \log_e(x_i) \qquad \forall i \in [1, n]
$$

And its inverse transformation is then:

$$
    x_i = e^{y_i} \qquad \forall i \in [1, n]
$$

It is mainly used on continuous variables with a right-skewed distribution to make them more symmetric. This often turns non-linear relationships into linear ones. A constant $b$ can also be added to the data if they contain 0 or negative numbers:

$$
    y_i = \log_e(b + x_i) \qquad \forall i \in [1, n]
$$

Where $b = 1$ when some data are equal to 0. More generally, any mathematical function can be used to transform some data as long as it is invertible.

#### Ordinal encoding

Ordinal encoding transforms a categorical variable into a discrete one by attributing a number to each category (data from the [Decatur project](https://co2datashare.org/dataset/illinois-basin-decatur-project-dataset)):

```{raw} html
<div style="width: 400px;">
```
| Depth | Lithology | Encoded |
| :---- | :-------: | :-----: |
| 4900  | shale     | 3       |
| 4925  | shale     | 3       |
| 4950  | sandstone | 1       |
| 4975  | sandstone | 1       |
| 5000  | sandstone | 1       |
| 5025  | sandstone | 1       |
| 5050  | carbonate | 2       |
| 5075  | carbonate | 2       |
| 5100  | carbonate | 2       |
| 5125  | carbonate | 2       |
| 5150  | carbonate | 2       |
```{raw} html
</div>
```

This is mainly used with ordinal variables. When used with nominal variables, it is best to define some meaningful order: for instance in the dataset above, the categories are encoded from most to least permeable.

#### One-hot encoding

Ordinal encoding transforms a categorical variable $X$ into a set of discrete ones called indicator variables, one per category: each indicator variable $I$ is equal to 1 when an observation belongs to a given category, false otherwise. So in the dataset from the previous subsection we would have three indicator variables:

$$
\begin{align}
    i_{\text{sandstone},i} = & \begin{cases}
        1 \text{ if } x_i = \text{sandstone} \\
        0 \text{ otherwise} \\
    \end{cases} \\
    i_{\text{carbonate},i} = & \begin{cases}
        1 \text{ if } x_i = \text{carbonate} \\
        0 \text{ otherwise} \\
    \end{cases} \\
    i_{\text{shale},i} = & \begin{cases}
        1 \text{ if } x_i = \text{shale} \\
        0 \text{ otherwise} \\
    \end{cases} \\
\end{align}
$$

Which would lead to the following dataset (data from the [Decatur project](https://co2datashare.org/dataset/illinois-basin-decatur-project-dataset)):

| Depth | Lithology | Shale | Sandstone | Carbonate |
| :---- | :-------: | :---: | :-------: | :-------: |
| 4900  | shale     | 1     | 0         | 0         |
| 4925  | shale     | 1     | 0         | 0         |
| 4950  | sandstone | 0     | 1         | 0         |
| 4975  | sandstone | 0     | 1         | 0         |
| 5000  | sandstone | 0     | 1         | 0         |
| 5025  | sandstone | 0     | 1         | 0         |
| 5050  | carbonate | 0     | 0         | 1         |
| 5075  | carbonate | 0     | 0         | 1         |
| 5100  | carbonate | 0     | 0         | 1         |
| 5125  | carbonate | 0     | 0         | 1         |
| 5150  | carbonate | 0     | 0         | 1         |
