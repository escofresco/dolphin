## Positively missing
### Scenario
A school district is allocating the annual budget and this year they have decided to change the way that age demographics are factored in. This year, a bonus will be allotted in diminishing value for a collection of age brackets such that
$$budget_{\text{age}}\propto \frac{1}{age}$$
To help every school maximize how much money they get, the district would like to write a web app that would identify the age group with the fewest students below the minimum required to receive a bonus so as to be the easiest to fulfill. The user would provide a list of student ages and the program would determine the target age group, if one exists. 

### Example
$$A = \{8, 8, 12, 8}$$

### Requirements
Running as a serverless function on a web service that bills for compute time, the program must minimize total cost. It should accept the following as input:
* Mutable list of ages, *A*
* 
