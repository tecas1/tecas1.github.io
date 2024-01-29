# MethaneSAT

I was excited to read about [MethaneSAT](https://www.methanesat.org/satellite/) today, a satellite that can measure methane leak rates at high speed and resolution.

![MethaneSAT example](https://www.methanesat.org/images/uploads/2023/09/Artboard-1.png)

[Methane](https://en.wikipedia.org/wiki/Methane) (CH<sub>4</sub>, the main component of natural gas) is an especially potent greenhouse gas; while it is the atmosphere it has a [global warming potential](https://en.wikipedia.org/wiki/Global_warming_potential) of about 150. The tricky "while in the atmosphere" qualifier is because atmospheric methane constantly breaks down to [carbon dioxide](https://en.wikipedia.org/wiki/Carbon_dioxide) (CO<sub>2</sub>). The half-life for atmospheric methane is about [10 years](https://climate.nasa.gov/vital-signs/methane). The half-life of atmospheric carbon dioxide seems to be [very long](https://www.nature.com/articles/climate.2008.122).

> Methane molecules react with hydroxyl radicals (OH)—the "major chemical scavenger in the troposphere" that "controls the atmospheric lifetime of most gases in the troposphere".[60] Through this CH<sub>4</sub> oxidation process, atmospheric methane is destroyed and water vapor and carbon dioxide are produced.
>
> [Wikipedia](https://en.wikipedia.org/wiki/Atmospheric_methane)

If we assume a constant hazard rate for atmospheric methane then the survival function will exhibit [exponential decay](https://en.wikipedia.org/wiki/Exponential_decay). If the half-life of atmospheric carbon dioxide were equal to the half-life of atmospheric methane then the survival rate for carbon dioxide would be a [gamma distribution](https://en.wikipedia.org/wiki/Gamma_distribution) with shape factor 2 and a scale factor based on the common half-life. But because the half-life values are different we end up with a more complicated expression to capture the interplay between the creation and sequestration processes. 

![methane by time](https://docs.google.com/spreadsheets/d/e/2PACX-1vRa5SQrQyMQD2-eKc7PcwHhx5X5oUdNZFJ0EyqvLrPxoWi7FaZti-XYk7bYdfDEU0y5BkVuHYjUYgi6/pubchart?oid=69845364&format=image)

| Description  | Equation |
| :-: | :-: |
| survival function for atmospheric methane | $$S_{CH_{4}} (t)=e^{-k_{CH_{4}}\cdot t}$$ |
| survival function for atmospheric carbon dioxide | $$S_{CO_{2}} (t)=e^{-k_{CO_{2}}\cdot t}$$ |
| methane is subject to constant hazard rate; break-down rate is proportional to amount of atmospheric methane | $$\frac {d[CH_{4}]}{dt}=-k_{CH_{4}}\cdot S_{CH_{4}} (t)=-k_{CH_{4}}\cdot e^{-k_{CH_{4}}\cdot t}$$ |
| carbon dioxide formation rate is equal to methane break-down rate | $$f_{CO_{2}} (t)=-\frac {d[CH_{4}]}{dt} $$|
| amount of carbon dioxide created at time τ and surviving to time t | $$[CO_{2}] (τ,t)= f_{CO_{2}} (τ)\cdot S_{CO_{2}} (t-τ)=k_{CH_{4}}\cdot e^{-k_{CH_{4}}\cdot\tau}\cdot e^{-k_{CO_{2}}\cdot (t-\tau)}$$ |
| amount of carbon dioxide | $$[CO_{2}] (t) = \int_{0}^{t} [CO_{2}] (τ,t) d\tau = (k_{CO_{2}} * S_{CO_{2}}) (t)=\int_{0}^{t} k_{CO_{2}}\cdot e^{-k_{CO_{2}}\cdot\tau}\cdot e^{-k_{CO_{2}}\cdot (t-\tau)}d\tau$$ |

![GWP by time](https://docs.google.com/spreadsheets/d/e/2PACX-1vRa5SQrQyMQD2-eKc7PcwHhx5X5oUdNZFJ0EyqvLrPxoWi7FaZti-XYk7bYdfDEU0y5BkVuHYjUYgi6/pubchart?oid=103035834&format=image)

This global warming potential plot shows that a release of methane initially causes quite a lot more warming than a similar size release of carbon dioxide. But over time the gap narrows as the atmospheric methane breaks down to carbon dioxide. Over a long enough amount of time the harm would seem to be about the same. 

So if we can prevent releases of methane now we get large emissions savings now.

| Methane years in atmosphere | Cumulative warming relative to carbon dioxide |
| :-: | :-: |
| 1  | 145x |
| 5 | 125x |
| 10 | 110x |
| 20 | 80x |
| 50 | 45x |
| 100 | 20x |

Please feel free to check out my calculations [here](https://docs.google.com/spreadsheets/d/1Xl0Zh1OKOf-eD1j0mvif0L7oHBUzZrp23TLmq4K22jY/edit?usp=sharing).

Hopefully leaks can be detected with the satellite then fixed: the emissions savings could be huge and perhaps hundreds of times less expensive than any course of action available to individuals wanting to act on their own.

> The MethaneSAT project has an ambitious policy goal: reduce global methane emissions from oil and gas facilities by 45 percent by 2025 and 70 percent by 2030. If achieved, it would have a similar impact on the climate over 20 years as closing one-third of the world’s coal plants, EDF said.
> ....
> Hamburg and Wofsy said they’re optimistic that corporations will respond relatively quickly because the fixes aren’t technically difficult, involving things such as tightening pipelines and improving wasteful processes. In addition, the methane saved can be sold as natural gas, so any remediation will at least partly pay for itself.
>
> [Harvard](https://news.harvard.edu/gazette/story/2023/03/methane-tracking-satellite-may-be-fastest-way-to-slow-climate-change/)

