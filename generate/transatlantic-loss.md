
# Empty transatlantic cable
## Background
A U.S. company is auctioning off use of their new transatlantic cable. The transatlantic cable consists of smaller dedicated tubes that will be leased to Internet Service Providers (ISPs). The transatlantic cable company would like to determine how much to charge each ISP according to the cross-sectional area that their tube occupies. 

To reiterate, the transatlantic cable itself is purely intended to insulate a bundle of *n* inner cables. These sell for 10¢/µm. The transatlantic cable cross-section is arranged into an Appolonian gasket<sup>1</sup> of tubes. The signed curvature of each tube's cross-section changes according to Descarte's theorem<sup>2</sup>,

$$k = \pm \frac 1 r\\\ \text{where, }k = k_1+k_2+k_3 + 2(k_1k_2 + k_1k_3 + k_2k_3)\.$$

For a 1"-thick, 2,500 miles long transatlantic cable, compute the revenue lost by offering to sell *n* = 5 instead of *n* = 7.

## Expectations
* Use Python 3 to implement a function ƒ that answers the question for any *k*.
* Use Python 3 to supply  ƒ(*7*)-ƒ(*5*).
* Produce the answer in dollars.
* Use the following to reconcile differing units:
$$1\text{ nautical mile} = 1.15078\text{ miles,}\\\ 1 \text{ mile}= 1.60934\text{ kilometers,}\\\ 1 \text{ kilometer} = 10^5 \text{ centimeters,}\\\1 \text{ meter} = 10^6 \text{micrometers,}\\\ 1 \text{ dollar}=100\text{ cents.}$$
* Infer the rate of return when ∆*k* = 1.

---
<sup>1</sup>[Apollonian gasket](https://en.wikipedia.org/w/index.php?title=Apollonian_gasket&oldid=1214842476), (last visited Mar. 22, 2024).
<sup>2</sup>[Descarte's theorem](https://en.wikipedia.org/wiki/Descartes%27_theorem), (last visited Mar. 22, 2024)
