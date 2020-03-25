# Checklist

## 1. Before Starting -- Answering the Question

- [ ] Did you specify the type of data analytic question (e.g. exploration, association causality) before touching the data?
- [ ] Did you define the metric for success before beginning?
- [ ] Did you understand the context for the question and the scientific or business application?
- [ ] Did you record the experimental design?
- [ ] Did you consider whether the question could be answered with the available data?
- [ ] What is the end deliverable going to look like (e.g., jupyter notebook, slides, deployable code)?

##  2. Checking the Data

- [ ] Did you plot univariate and multivariate summaries of the data?
- [ ] Did you check for outliers?
- [ ] Did you identify the missing data code? 
	- To visualize where the data missing data are: [the Missingno Library](https://www.geeksforgeeks.org/python-visualize-missing-values-nan-values-using-missingno-library/)
- [ ] How many observations are there in total, and of each important class? Are the data imbalanced?
- [ ] What data types are the data stored in? E.g., are dates, numbers stored as strings?

### Helpful functions:
```python
# Pandas functions
df.value_counts()
df.value_counts(normalize=True) # gets the percentage of different value counts
df.sample(50) # generates a random sample of 50 rows. Useful for checking your own intuition about data
```

## 3. Cleaning the Data

- [ ] Is each variable one column?
- [ ] Is each observation one row?
- [ ] Are there repeated observations?
- [ ] Are the data types in the right format now?
- [ ] Did you record the recipe for moving from raw to tidy data?
- [ ] Did you record all parameters, units, and functions applied to the data?

### Helpful functions:
```python
# check for duplicates & drop them
print('Number of duplicated rows:', sum(df.duplicated()))
df.drop_duplicates(inplace = True)

# Convert numbers in strings to integers. Entries that can't be converted will be null now. Need to fill those in or drop. 
df['column'] = pd.to_numeric(df['column'],errors='coerce',downcast='integer')

# Use assert statements to check whether there are any nulls left in specified columns:
for colname in df.columns:
	assert df.loc[df[colname].isnull()].shape[0]==0, 'Error! Nulls in {}'.format(colname)
```

## 4. Exploratory Data Analysis

- [ ] Did you identify missing values? How are you going to deal with them (imputation, dropping rows, etc.)?
- [ ] Did you make univariate plots (histograms, density plots, boxplots)?
	- These plots can be useful to identify outliers, so is df.describe()
- [ ] Did you consider correlations between variables (scatterplots)?
- [ ] Did you check the units of all data points to make sure they are in the right range?
- [ ] Did you try to identify any errors or miscoding of variables?
- [ ] Did you consider plotting on a log scale?
- [ ] Would a different type of plot (scatter maybe) be more informative?

### Helpful functions and packages:
[Pandas profiling](https://github.com/pandas-profiling/pandas-profiling) shows the distribution or proportion of every column, correlation across every column, missing values, duplicate rows, and other important statistics
```python
profile = ProfileReport(df, title='Pandas Profiling Report')
```

## 5. Inference

- [ ] Did you identify what large population you are trying to describe?
- [ ] Did you clearly identify the quantities of interest in your model?
- [ ] Did you consider potential confounders?
- [ ] Did you identify and model potential sources of correlation such as measurements over time or space?
- [ ] Did you calculate a measure of uncertainty for each estimate on the scientific scale?

## 6. Prediction

- [ ] Did you identify in advance your error measure?
- [ ] Did you immediately split your data into training and validation?
- [ ] Did you use cross validation, resampling, or bootstrapping only on the training data?
- [ ] Did you create features using only the training data?
- [ ] Did you estimate parameters only on the training data?
- [ ] Did you fix all features, parameters, and models before applying to the validation data?
- [ ] Did you apply only one final model to the validation data and report the error rate?

## 7. Causality

- [ ] Did you identify whether your study was randomized?
- [ ] Did you identify potential reasons that causality may not be appropriate such as confounders, missing data, non-ignorable dropout, or unblinded experiments?
- [ ] If not, did you avoid using language that would imply cause and effect?

## 8. Figures

- [ ] Does each figure communicate an important piece of information or address a question of interest?
- [ ] Do all your figures include plain language axis labels?
- [ ] Is the font size large enough to read?
	- sns.set(font_scale = 1.5)
- [ ] Does every figure have a detailed caption that explains all axes, legends, and trends in the figure?

### Helpful functions and packages:
This produces a more stylistically pleasing plot
```python
from matplotlib import cycler
colors = cycler('color',
                ['#EE6666', '#3388BB', '#9988DD',
                 '#EECC55', '#88BB44', '#FFBBBB'])
plt.rc('axes', facecolor='#E6E6E6', edgecolor='none',
       axisbelow=True, grid=True, prop_cycle=colors)
plt.rc('grid', color='w', linestyle='solid')
plt.rc('xtick', direction='out', color='gray')
plt.rc('ytick', direction='out', color='gray')
plt.rc('patch', edgecolor='#E6E6E6')
plt.rc('lines', linewidth=2)
```

## 9. Written analyses -- if required

- [ ] Did you describe the question of interest?
- [ ] Did you describe the data set, experimental design, and question you are answering?
- [ ] Did you specify the type of data analytic question you are answering?
- [ ] Did you specify in clear notation the exact model you are fitting?
- [ ] Did you explain on the scale of interest what each estimate and measure of uncertainty means?
- [ ] Did you report a measure of uncertainty for each estimate on the scientific scale?

## 10. Presentations -- if required

- [ ] Did you lead with a brief, understandable to everyone statement of your problem?
- [ ] Did you explain the data, measurement technology, and experimental design before you explained your model?
- [ ] Did you explain the features you will use to model data before you explain the model?
- [ ] Did you make sure all legends and axes were legible from the back of the room?
