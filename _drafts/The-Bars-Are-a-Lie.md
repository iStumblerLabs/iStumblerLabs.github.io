---
layout: post
title: The Bars are a Lie
---

# The Bars are a Lie


## Intro

Signal strength bars are a lie.

Or at least a misnomer. The three little radial slices of pie on the top of your screen don't relate to the signal your devices radio or radios are receiving. 


## Math is Fun!

Here's how you convert from a dBm (deci-Bell-milliwatt) value to a percentage, 
where 100% is the theoretical maximum, and 0% the minimum according to our 
understanding of electromagnetism.

```
typedef CGFloat RSRadioDB; // Deci-bells, a ratio
typedef CGFloat RSRadioDBm; // Deci-bell-milliwats, an absolute power
typedef CGFloat RSRadioHertz; // how many times per second (Cycles if you were a radio op in WWII)
typedef CGFloat RSRadioWatts; // EIRP absolute power

/*
  Converting a dBm value to a percentage: 

    boltzmann-constant + 10 log(channel-width-in-hz)

  http://en.wikipedia.org/wiki/Thermal_noise

  noise floors for common channel widths:
  
  1MHz      = -114;	// bluetooth channel
  2MHz      = -111; // bluetoth LE channel
  20MHz     = -101; // 802.11a/b/g channel
  40Mhz     = -98;  // 802.11n 40 mhz channel
  80Mhz     = -95;  // 802.11ac 80 mhz channel
  160Mhz    = -92;  // 802.11ac 160 mhz channel
*/
static CGFloat const BoltzmannConstantAt300K  = -174;

RSRadioDBm RSComputeNoiseFloor(RSRadioHertz channelWidth) {
	return BoltzmannConstantAt300K + log10f(channelWidth);
}

CGFloat RSSignalDBmAsPercentage(RSRadioDBm signal, RSRadioHertz channelWidth) {
	CGFloat floor = RSComputeNoiseFloor(channelWidth);
	return (100 - (((CGFloat)signal / floor) * 100));
}

RSRadioWatts RSWattsFromdBm(CGFloat dBm) {
	return (pow(10, (dBm / 10)) / 1000);
}
```


