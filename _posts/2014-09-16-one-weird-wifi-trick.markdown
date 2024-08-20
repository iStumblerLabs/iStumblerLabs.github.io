
# This One Weird Trick to Improve Your Wi-Fi Reception

Recently on MacGeek Gab, I was asked about the ‘correct’ antenna orientation for Wi-Fi routers. Off the cuff I replied: “one up, one down,” which is how I habitually orient antennas in the familiar two-monopole configuration.

![Think Perpendicular for Antenna Placement](/images/2014/OWIT-01-antenna-placement.webp)

My rationale, based on my rudimentary knowledge of antenna and RF design was that the two different orientations would produce two separately polarized antenna patterns, one horizontal and one vertical. Devices vary in their antenna polarization, and mobile devices tend to change theirs frequently, so my thinking was to provide for both modes of operation by creating the appropriate corresponding antenna patterns.

In discussing the issue after the episode aired, and doing some research I learned some things about antennas and diversity that I didn’t know before and found very interesting. Besides polarization, aligning the antennas at right angles has two other benefits, both paid for with marginal range loss:

## POLARIZING THE DISCUSSION

The first questions came up about polarization, what is it exactly and why is it better to have more than one polarity?

Polarization is a property of light, and has to do with the orientation of the wave to the axis along which you observe it. Polarizing sunglasses really cut down on glare because the light reflected off shiny surfaces is composed of many different polarities, the shades only allow some of those through, cutting down the total brightness.

Wi-Fi operates at much lower frequencies than visual light, but the principals are the same: if the transmitting and receiving antennas are aligned physically, the signal comes through clearer. So having both vertical and horizontal antennas gives devices a better chance of seeing one or the other.

One fine point that came out of the discussion: antennas themselves are not polarized, strictly speaking they create a polarized field. Also, many panel antennas have multiple emitting elements, each with separate polarization, to provide better coverage.

## MIMO AND PATH DIVERSITY

I formed my opinion on this way back when .11g routers where common, and two antenna systems were typically using a simple antenna diversity system to improve signal strength. Wi-Fi in the mean time added 11n which includes MIMO (Multiple-In Multiple-Out) radio systems. Suddenly, there are routers with three antennas, and each antenna is driven by a separate radio-chain or radio-subsystem in order to exploit what’s called: spatial diversity.

Spatial diversity is the kind of technology that’s really hard to explain without understanding general relativity. Fundamentally, it relies on the fact that the speed of light being constant, and microwave signals which tend to bounce around, will take slightly less time to reach you via some paths than others. The signal processing systems in your Wi-Fi card can measure this, and use it to compress more data into a given channel.

The effect of MIMO is asymmetric so that a 3x3–which is to say three radio and three antenna–access point can deliver more data and better range, even to 1x1 clients. When orienting a three antenna array, the best solution is a ‘peacock fan’ with a vertical central antenna, and the other two about 60° from vertical (one can be horizontal).

## DE-CORRELATING THE ANTENNAS

The final benefit is that by adjusting the antennas away from the same orientation, you are de-correlating them. Since the radios which drive the antennas are operating on the same frequencies, the output of each is received by the others during transmit. This is factored into the MIMO system but by adding polarization diversity you can increase the efficiency of antenna system by reducing this cross-talk between antennas.

## THERE IS NO FREE LUNCH

Now, nothing in the universe comes for free, there are always tradeoffs. The principal one in this case is absolute range of the system. If all the emitters in an antenna system are oriented identically, operating in lockstep, they can achieve better range than a diverse array of antennas especially for a client that is similarly aligned. Some adaptive antenna systems do this dynamically at the cost of compute power, to achieve better range for clients at various orientations.

## SIGN-OFF

All of this to say that a simple twist of the antennas in your access point can make your Wi-Fi perform a little bit better for you.
