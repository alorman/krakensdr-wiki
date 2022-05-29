<img src="https://user-images.githubusercontent.com/78108016/170180118-7be4ca09-2436-480c-b5d4-c599492271f3.png" align="right" width="500" />

For standard direction finding you will need five identical omni-directional antennas. You can compromise and use fewer antennas, but for best performance we recommend using all five antennas. These are typically magnet mount whip antennas, or dipoles. We recommend always using a Uniform Circular Array (UCA) antenna arrangement as it can determine bearings from all directions. Linear arrays are restrictive in that they do not know the difference between a signal coming from in front, or behind the array,

Note, when mounting antennas, the convention is to mount them in a clockwise direction when seen from a top-down perspective. So, antenna zero is the first antenna pointing towards zero degrees, antenna one is to the coordinate to the right of antenna one, and so on.

The explanations below provide more detail to the math behind the antenna spacing. However, in practice, you only need to decide what type of array you want to use, and then use an [Excel sheet calculator](https://docs.google.com/spreadsheets/d/1w_LoJka7n38-F0a3vgaTVcSXxjXvH2Td/edit?usp=sharing&ouid=113401145893186461043&rtpof=true&sd=true) to calculate the spacing and placement coordinates required. 

# Antenna Arrangements

## Uniform Circular Array (UCA)

If you wish to determine radio sources from 360 degrees around the array, then the antennas should be arranged in a uniform circular array (UCA). The interelement spacing (the distance between the tip of each neighbouring antenna element in the array) needs to be set specifically for a range of interested frequencies.

You must design your array such that the interelement spacing I_e is less than half a wavelength λ of your highest frequency of interest
I_e=sλ

where s is the wavelength spacing multiplier that must be <= 0.5 and λ is the wavelength in meters.

An array with an interelement spacing larger than this will experience what’s called ‘ambiguity’. Put simply, this means that the system may see the signal source coming in from more than one direction, and we have no way to know which is the true direction. This is obviously not ideal, so always keep the multiplier below 0.5.

Using a spacing multiplier less than 0.5 can also allow you to design a smaller array size, at the expense of some accuracy. Generally, down to s=0.2 is acceptable, and we typically set our arrays to s=0.33. It’s important to note that the accuracy of the direction-finding result diminishes with smaller spacing multipliers, and for 5-elements the accuracy starts to become unacceptable below around s=0.2.

As the interelement calculation depends on wavelength, you can conclude that lower frequencies require larger antenna array sizes. This shows that this type of radio direction finding method can be impractical for frequencies with large wavelengths as the arrays will take up a lot of space. For HF and the smaller VHF frequencies with large wavelengths, other radio direction methods like TDoA, Watson-Watt and manual Yagi based methods may be more appropriate.

It may be useful to set up a UCA array by measuring the radius, rather than by measuring interelement spacing. The formula for calculating radius for a given spacing multiplier and wavelength is given by:

r=  sλ/√(2 (1-cos⁡(360/n))

where s = spacing multiplier, λ = wavelength in meters and n = number of antenna elements

## Uniform Linear Array (ULA)

The other way to set up an array is to use a uniform linear array (ULA), which is just the antennas lined up in a straight line. The disadvantage to this arrangement is the array is only valid for 180 degrees, and there is no way of knowing if the signal is coming from in front, or behind the array.

The advantage of ULA is greater accuracy resolution due to a larger possible aperture. But this greater accuracy only applies to signals that arrive at angles near to orthogonal to the array. The effective aperture will appear to be much smaller near the 0- and 180-degree edges of the array. 

The interelement spacing calculation is the same formula as for UCA.

I_e=sλ

# Antenna and Coax Precision

The KrakenSDR will not compensate for phase distortion in the external antenna system.
Therefore, you must use identical antennas, and lay out your antenna array as precisely as possible. You can use one of our layout templates on krakenrf.com to help with placement. A tip is to measure the interelement spacing between elements after placement and confirm that all measurements are identical.

All the coax cables connecting the antennas to KrakenSDR must be identical lengths to a tolerance within a centimeter or less. If cables have different lengths, then direction finding will not be possible.

The higher your frequency of interest, the more precise you need to be with your antenna position layout and coax length tolerances.
For example, at 800 MHz a 1 cm difference between coax cable lengths in the array could result in a phase distortion between elements of up to 14 degrees. At 400 MHz the same 1 cm difference results in 7 degrees distortion. Note that this distortion is between elements and does not translate directly to a bearing distortion which is often less. Nevertheless, be aware cable length precision is an important consideration.

# Antenna Array Positioning

On a vehicle you will want to have the antennas on the roof of the car. Ideally objects that could block the antennas like roof racks will be removed too. 

For a fixed site, you want the array to be placed up as high as possible, away from obstructions. Nearby obstructions like other antennas, poles, roofing can cause multipath and other refractive type effects that can distort the angle that the signal arrives at, resulting in poor results.
In both cases, ensure that the coax cables are neat, and ideally all run in the same direction, and are bundled together with cable ties. Being neat like this ensures that any phase distortions caused by bends in the cable happen identically to all cables.

Note that some fixed site antenna arrays like the array produced by the company Arrow Antennas may have holes drilled for elements that can be placed at different radii. It’s important to note that you can only use ONE set of elements at a time. If other unused elements are placed on the same array at the same time, those elements will block, reflect and refract the incoming signal causing massive distortion to the angle if the signal arrive direction that the system detects.

If you need to run multiple antenna arrays, you will need to either spread multiple arrays out a good amount of horizontal distance apart, or spread them out vertically in height. An idea might be to stack the smaller array on top of the larger array.

# External RF Components
Be aware any external components placed in the RF chain such as switches, LNAs and filters may be distorting the phase of the antennas which will result in poor results. You may need to perform lab tests to confirm if your components cause non-negligible phase distortion or not. Typically we find that most simple filters will cause negligible distortion and LNAs will only cause mild distortion as long as they are all identical, and all identical adapters are used.

# Antenna Choice
As mentioned, you will most likely want to use either magnetic whip antennas, or dipole antennas. Magnetic whip antennas are well suited to motor vehicles. If you are choosing antennas, make sure that they have a direct or capacitive ground plane connection for best performance. Many cheaper magnetic whip bases have very poor, or even no ground connection.

As mentioned above you will also want to examine closely the cable length tolerances if the cable is fixed to the antenna base.

# KrakenSDR Direction Finding Antenna Set

If you ordered our 5x KrakenSDR antenna set, you will need to assemble them. This is a simple process:

* Simply screw the SMA tee part into the base, 
* then screw the telescopic whip onto the tee; and 
* then you can connect the provided coax cables.

You will then want to adjust the telescopic whip for the length that is best covered by your frequency of interest. Under normal circumstances, you will want the length to be a quarter of the wavelength of the frequency of interest for best reception.

Obviously if you are running the antennas on a vehicle, you do not want the antennas to be extended too long for safety. Using shorter than optimal antenna lengths will generally be acceptable in most cases.

# Theory of Resolving Resolution

If the resolving resolution is 10 degrees, we can say that the actual bearing is somewhere within a 10-degree arc.
Here we briefly explain the background theory behind what sort of accuracy resolution we can expect from a 5-element array system. With a 5-element circular array spaced at 0.5 λ, we might roughly expect a resolution of about 8 degrees. With a 5-element linear array we could roughly expect about 3.4 degrees. This is the best-case resolution, not considering external distortions like multipath. (This may appear inaccurate, but in practice when multiple readings are taken from many locations the inaccuracies simply average out and become negligible.)

To estimate the error, we used the Rayleigh resolution calculation from wave physics. The Rayleigh formula states that resolving resolution is given by θ=1.22λ/D, where D is the aperture of the antenna array. For a circular array the aperture is equivalent to the diameter, and for a linear array it’s equal to the total length. For a linear array however, it must be taken into account that the effective aperture will appear to be much smaller when seen from the sides.

So, using the formula given further above for array radius, then multiplying by two to get diameter, for an n=5 element circular antenna array with s=0.5 spacing we get an aperture of D=0.85λ . Therefore, the Rayleigh equation reduces to θ=1.22/0.85 = 1.44 rad = 83 degrees. 

For a 5-element linear array its aperture is given by the total array length which is given by D = (n-1) * s λ. If we have n=5 elements and s=0.5 spacing, then θ=1.22/2 = 0.61 rad = 34 degrees.

Because we use ‘super-resolution’ algorithms like MUSIC, we can improve on the Rayleigh resolution by a very approximate factor of 10. So, we end up with a resolution of 83/10 = 8.3 degrees for the circular array, and 34/10 = 3.4 degrees for the linear array.