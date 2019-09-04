So you decided to use your mic on your stream! Which would be very helpful toward making the stream more interactive, as generally it's more fun and joyful watching someone playing games when you can hear what they think via their voice!

But one thing, your viewers are supposed to hear your voice and **all kind of other noises**, and it's hard to stay in your stream if the noises are too interrupting to watch your stream.

There are 4 audio filters I will explain, that will drastically improve your overall audio, and if you are done setting your basic configuration for them, it will be easier to make change when someone tells you there's an issue with your audio.

Before going into the explanation, I want to tell you that all these filters can also be applied to any of your audio sources, including Desktop Audio. And the filters can improve these audio sources in the same way they can improve your voice.

# Table of Contents

- Quick look at [the Peak Meter and the Filter Window](#about-the-interface).
- Is there static noise around you?  
  Try [Noise Suppression](#noise-suppression) and [Noise Gate](#noise-gate).
- Your voice is too quiet even at maximum volume?  
  Try [Gain](#gain).
- Your voice is sometimes too loud, and sometimes too quite?  
  Try [Compressor](#compressor).
- Worried about your voice maxing out and distorting when you scream?  
  Try [Limiter](#limiter).

- - -

# About the Interface

## Peak Meter

![Peak Meter][OBS Peak Meter]

Here each channel will show the peak of the signal they receive in real time. All active filters affect these meters. Here I set it to be vertical, but default view is horizontal. There could be more than just two channels if you have more audio devices connected to the computer!

Right click or click the gear icon to access filters and other options.

Detailed info about how to read this meter is available at [the official wiki][Reading the Volume Meter].

## Filter Window

![Filter Window][OBS Filter Window]

When you access the filters from the peak meter, you will see all the filters set for the corresponding channel.

1. Eyes show if filters are active. If you feel like you have to keep a filter while not going to use it right now, you can click the eye to toggle the filter to be on and off, instead of just deleting it.
2. These icons will let you add, remove, and adjust the order of the filters. Signals of an audio channel will go through them from top to bottom.

Remember that **only the first filter in the order will receive the raw audio input**. All the other filters will receive the altered signal from a filter right above it.

[OBS Peak Meter]: ./image/peak-meter.png
[Reading the Volume Meter]: https://github.com/obsproject/obs-studio/wiki/Understanding-The-Mixer#reading-the-volume-meter
[OBS Filter Window]: ./image/filter-window.png

- - -

# Noise Suppression

![Noise Suppression window][Window: Noise Suppression]

| Problem  | There's a background noise. |
| -------- | ---------------- |
| Function | Reduce the audio by the level. |

> **How to set up** Keep yourself silent, and start from 0dB and slowly decrease the slider until you see no peak meter movement. Try talking to see if it keeps your voice.

This filter has a very simple interface, one slider named 'Suppression Level' and that's it! It will reduce the associated audio by the amount set by the slider.

Noise Suppression is good at cutting mild noises like an electric fan in your room.

Since it will reduce the volume of the channel, it's good to set up a Gain filter to compensate the volume loss.

# Gain

![Gain Window][Window: Gain]

| Problem  | Voice is too quiet but it can't be increased anymore. |
| -------- | ---------------- |
| Function | Boost the audio by the level. |

> **How to set up** Set the slider to the value you want to add to the signal.

This filter has a very simple interface too, and this time the change is clearly visible: Let's say you set the slider to 5dB, you'll see the peak meter increase by 5dB for the same signal.

When you applied a filter and as a result the channel signal became quieter, you can apply this filter to compensate for the loss.

This filter has another use than just 'boosting up' the signal: Compressor can make a better adjustment for signal that's loud in overall.

# Noise Gate

![Noise Gate Window][Window: Noise Gate]

| Problem  | I want the mic to be completely silent when I am not talking. <br>Noise Suppression is not enough to cut out the background noise. |
| -------- | ---------------- |
| Function | Turns off the channel when it goes silent. |

> **How to set up**  
> 1. Set two thresholds all the way to the left.  
  Slowly drag Close Threshold to right until you see no peak meter movement. It should show a movement when you talk.
> 2. Try talking to see where the peak stays after you finished talking.  
  Move Open Threshold to a value around the peak value you saw.  
  Try talking to see if the peak meter goes silent after talking.  
  Keep adjusting the threshold until you find a value where the channel effectively goes silent after your voice.

Basically what it does is muting and unmuting at set conditions.

- Signal goes quieter than **Close Threshold**, the channel is muted.
- Signal goes louder than **Open Threshold**, the channel is unmuted.

It comes handy when you want to ensure complete silence on the mic channel or more strong control on the background noise.

You might not need to touch Attack/Hold/Release Time, but if you hear your first syllable getting cut when you start talking, then you would want to try setting at least Attack Time.

- When the signal goes over Open Threshold, the channel will be gradually opened over **Attack Time**, like a fade-in.
- Even the signal quickly goes back under Close Threshold, the channel will be kept open at least for **Hold Time**.
- When the signal goes under Close Threshold and after Hold Time is passed, the channel will be gradually closed over **Release Time**, like a fade-out.

# Compressor

![Compressor Window][Window: Compressor]

| Problem  |   |
| -------- | ---------------- |
| Function |   |

# Limiter

![Limiter Window][Window: Limiter]

| Problem  |   |
| -------- | ---------------- |
| Function |   |

# Troubleshooting

Okay, so you're all set up with audio configuration! It should be good for now, but as time goes there should be always someone who's gonna point out an issue with your audio setting. It could be a viewer, or you yourself!

I'll list some case

[Window: Noise Suppression]: ./image/en/ns-window.png "window of Noise Suppression"
[Window: Noise Gate]: ./image/en/ng-window.png "window of Noise Gate"
[Window: Compressor]: ./image/en/c-window.png "window of Compressor"
[Window: Gain]: ./image/en/g-window.png "window of Gain"
[Window: Limiter]: ./image/en/l-window.png "window of Limiter"
