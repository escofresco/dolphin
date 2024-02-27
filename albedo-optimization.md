### Reflective short roads
#### Scenario
A federal task team has been chartered to help the highway interstate system build sustainable roads by changing the way they allocate their annual budget. The new highway budget will ensure new highways increase surface reflectivity, known as albedo<sup>1</sup>, and reduce metric-tons of CO<sub>2</sub> of the system. New roads connecting two cities must maximize albedo while minimizing vehicle emissions<sup>2</sup>. The team needs a program that selects the ten most eco-friendly highways from the thousands of annual applications.

<br/>

#### Inputs:


* ##### Albedo
This refers to the percentage of diffusively reflected sunlight on a road. It is a dimensionless number.


* ##### Metric tons of CO<sub>2</sub> 
This quantity is calculated from the product of highway distance , *D<sub>i </sub>km*, and average tons of gas emitted per kilometer. Given an average number of cars, *C<sub>j</sub>*, with average tailpipe emissions of 250 grams of CO<sub>2</sub> per kilometer, the total interstate emissions is solved for *n* highways where every highway connects two cities *X* and *Y*.

$${V {\_{\text{tons}}} = }\{\sum_\{i=0}^n}{{\sum_\{j=0}^\{|C_i|}}}{\cfrac{C_i\times D_i \times 250{\frac{\text{g}}{\text{car}{\cdotp}\text{km}}} }{1000\frac{\text{kg}}{\text{ton}}}}$$


* ##### 

<br/>


#### Instructions
Write a Python function that accepts a list of potential highways  and returns ten highways that, when considered individually, would most reduce the albedo-metric-tons of CO<sub>2</sub> for the entire system.

Each candidate consists of
* `city_a` location,
* `city_b` location,
* kilometers `distance` between `city_a` and `city_b`,
* `albedo` ratio



---
<font size=1> 1. [Albedo](https://en.wikipedia.org/w/index.php?title=Albedo&oldid=1209156247) (last visited Feb. 27, 2024).</font>
<font size=1> 2. [Countering Climate Change](https://news.mit.edu/2021/countering-climate-change-cool-pavements-0822).</font>
<font size=1> 3. [Greenhouse Gas Emissions from a Typical Passenger Vehicle](https://www.epa.gov/greenvehicles/greenhouse-gas-emissions-typical-passenger-vehicle#:~:text=2%20per%20mile.-,What%20is%20the%20average%20annual%20carbon%20dioxide%20(CO2)%20emissions,around%2011%2C500%20miles%20per%20year) (last visited Feb 27, 2024).
