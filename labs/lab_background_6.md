# Maintainable Chef

## Linting 

### Foodcritic

Foodcritic is part of the standard set of utilities included with the Chef Development Kit.

Foodcritic is a command-line application that analyzes cookbooks to verify that they adhere to a set of conventions.

Foodcritic is executed against a specified path. The path provided is the path to a specific cookbook.

```
foodcritic PATH
```

The [foodcritic website](http://www.foodcritic.io/) describes each of the violations. Given a rule number the website provides additional details about the rule, the categories where the rule belongs, the reasoning behind it, example code that violates the rule and example code that provides a remedy to the rule.

Example:

[FC033](http://www.foodcritic.io/#FC033) is a _correctness_ check. If informs an individual that an _erb_ template can't be found to match the use of a _template_ resource within a recipe.

### Rubocop

Rubocop is part of the standard set of utilities included with the Chef Development Kit.

Rubocop is a command-line application that analyzes source code to verify the ruby syntax and structure of our cookbooks.

The results start with a summary describing the number of ruby files that were found and examined. Next it displays the results of each of those files as a series of symbols or letters.

```
. means that the file contains no issues
C means an issue with convention
W means a warning
E means an error
F means a fatal error
```



