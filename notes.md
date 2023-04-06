# Building Studywide Statistics in MNE with Confi

Study time!

## User Docs

1. Clean your data with whatever method you like
2. Epoch your data based on your paradigm
  - go vs no-go
  - Can be segmented however you want
3. Math!

## Calculation Steps

1. Need all epoched trials in all conditions across all subjects available in some datastructure
2. Stdev across all channels
  - could technically be subset
  - stdev by time of epochs
3. Sample with replacement from trial set to make ERP based on condition
  - Trial set can be either within individual OR entire group
  - Entire group produces grey bar figure from Face13 original publication
  - Within indivudual requires you to average at the end to produce one wave and reproduces the black bar figure from Face13 original publication
4. Repeat above N times (like 1000)
  - We now have 1000 ERPs based on random sampling from trials within a condition
  - We also now have 1000 difference waves
5. Build step 4's ERPs into a confidence interval plot

every time you finish a step 3, subtract across the conditions, to make a difference wave.
  - you end up with 1000 difference waves
  - plotting the difference waves WITH their confidence interval will show where significant
  - anytime that something is not zero wrapping zero

convert final difference wave, into z-score
  - represents the effect size
  - distrance of the wave form from zero in units of the confidence interval
  - how many confidence intervals away from zero is this wave form

needs to consider differences of differences

be able to export all variables so that you can do external relations based on individual differences
