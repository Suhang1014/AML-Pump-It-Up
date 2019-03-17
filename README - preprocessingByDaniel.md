# Preprocessing: Daniel part
## Based on Su's document, using lowercase to select the values from features: funder, installer, scheme_management

### 1, only using the lowercase to select the target values and maintain the Top5 features.

### 2, using the lowercase and using regularization to categories the features: funder, installer

a, We categories the values into "government", "community", "individual" and "other"



b, Turn the 'nan' and '0' to be unknown 



c, Keep the feature values that counts>500.

### overall, we categories 15 feature values for funder, 12 features for installer
