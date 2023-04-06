# Building Studywide Statistics in MNE with Confi

A significant amount of documentation in the MNE universe centers around computing statistics on single subjects. Researchers however are most often interested in effects across groups, conditions, or entire populations. **MNE-Confi** seeks to provide convient user facing functionality for study-wide ERP statistics.

## Development Stages

1. Data structure creation and specifications
2. Study design ingestetion
3. Data loading procedures
4. 1x1 comparisons
5. 1x2, 2x1, and 2x2 comparisons
6. ERSP and time frequency comparisons
7. More!

## Sample User Workflow

1. Initialize your data
2. Clean your data with whatever method you like
  - ICA, manual review, etc
3. Epoch your data based on your paradigm
  - Make sure your events are labeled, i.e. go vs no-go
4. Save your epoched data
5. Specify the study design to MNE-Confi
  - Which type of comparison?
    - ERP or ERSP?
  - Study-wide sampling?
  - File paths
6. Validate procedure before running
  - Make sure you have selected the correct settings
  - Confirm file paths
  - Decide if intermediate files or figures need saving
  - etc
7. Run MNE-Confi
8. View results!

## Rough Calculation Workflow

Based on previous Confi plugin from [Face13 Publication](https://jov.arvojournals.org/article.aspx?articleid=2121634)

1. Build data structure of across all channels, all epochs, all subjects, and all conditions
 - Order here is subject to change
2. Compute the standard deviation across all channels 
  - This represents the Global Field Power (GFP)
  - Standard deviation is used such that average rereferencing does not produce a flat signal
3. Construct a "trial set" of potential epochs to sample from for bootstrapping
  - Trial set can be either within individual OR entire group 
  - Entire group produces grey bar figure from Face13 original publication
    - Within indivudual requires you to average at the end to produce one wave and reproduces the black bar figure from Face13 original publication
4. Sample with replacement from trial set to make single ERP based on condition
  - For any given time point `t_a`, randomly sample from all amplitude values in the trial set at `t_a`
5. Repeat step 4 for each condition at `t_a`
6. Compute difference waves for each comparison at `t_a`
7. Repeat steps 4, 5, and 6, `N` times
  - Typically `N = 1,000`
  - We now have `N` ERPs based on random sampling from trials for each condition
  - We also now have `N` difference waves per comparison

## Figure Representations

Assuming a 1x1 analysis of a go vs no-go task you would compute and display the following:

A. Compare the evoked responses with confidence intervals as well as the mean signals on the same axis
  - Envelope represents the confidence interval at every time point
  - Points where the confidence intervals do not overlap are significantly different
B. Plot the difference wave on its own with its respective confidence interval
  - Anywhere the confidence interval does not touch zero is significant
  - Compute Z-Score to determine effect size
    - Represents distance from zero; how many confidence intervals away?

## Further Considerations

A rough list of considerations or future directions:

- Needs to consider differences of differences
- Be able to export all variables so that you can do external relations based on individual differences
- Saving of intermediate stages
