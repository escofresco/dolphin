A civil engineer is looking build a multistory facility. The water will be sourced from a tower that must have a height greater than the facility's in order to sustain a minimum water pressure. For that reason, the engineer would like to identify the largest section of land that will not exceed a height *h* after being leveled. Surveyors have gone ahead and collected data representing the relative heights for contiguous units of land. For instance, here's the data for a 10-unit section of land for a sum that cannot exceed 184:

$$\begin{array}{}421&-25&629&\underbrace{\begin{array}{}332 & -24 & 555 & -934\end{array}}_{sum \leq 184}625&157&-80\end{array}$$


Given an array *A*, design a Python algorithm to determine the longest subarray of sum less than or equal to *h*. The runtime must be linear on average.
