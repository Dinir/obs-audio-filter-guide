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

| Problem  | Voice is sometimes too loud, sometimes too quiet. |
| -------- | ---------------- |
| Function | Compress loud signals to make the overall signal constant. |

> **How to set**
> 1. Check the range of your talking. Try talking in various ways and see where the peak meter stays.
> 2. Decide where you want your range to be in the peak meter.
> 3. Squeeze the range so it has the same length of the range you want.
> 4. Drag up the range to the range you want.

This should be the most complex filter among the filters introduced here. But when you make enough audio test to get the current range of your voice and set the target range you want your voice to stay in, setting the compressor to your environment will be clear.

After figuring out which range you want your voice to stay in, you can first *squeeze* the signal, then make up for the volume loss caused by the squeezing.

- Any signal that goes over **Threshold** will be squeezed by the **Ratio**.
- The squeezed signals can be amplified back up by **Output Gain**. It will be added to the signal by the fixed amount.

There's a setting for Attack/Release Time.

- When the signal reaches the Threshold, the squeezing will start gradually growing up to the Ratio, over **Attack Time**.
- When the signal goes under the Threshold, the squeezing will start gradually wearing off over **Release Time**.

Here's an *example case* of setting up the compressor to make your voice constant and loud enough. The specific numbers can be various due to many reasons: how close your mouth is to your mic, how sensitive your mic is, how loud your desktop audio usually goes, and many others...

When you tried talking in various ways, sometimes the peak goes between -5 and -15, -15 and -25, and -30 and -35.
You want to make your voice range to be between -10 and -20.

![Compressor Explanationary Picture][Compressor Steps]

Your original voice range could be therefore between -5 and -35. You don't need to be precise when define the range. Just check the most biggest peak and most smallest peak when you were talking.

Let's say game audio is usually going around -20 and -30. Most of the cases you want your voice to be louder than game audio and other desktop sounds, so let's set the target range to -10 and -20.

First you want to squeeze the signals. Original range is 30dB wide (-5 ~ -35), and target range is 10dB wide (-10 ~ -20). Squeeze the original range by Ratio of 3:1 so it becomes 10dB wide.

With this change, the overall voice should be much quieter now. The changed range is between -25 and -35 now. You need to make up the volume loss, so let's add Output Gain of 15dB. The range will be now -10 and -20, which is the target range.

Now most of the time you speak to the mic, your voice will be in between -10 and -20. Unless you shout right into the mic, which will result going way over -10, because Compressor is not functionally 'limiting' the volume. 

In that case, we could use Limiter.

> By the way you can apply Compressor to Desktop Audio and other various capture device audio outputs to make them stay in a range most of the time!  
  Compressor for Desktop Audio could be set in a bit different way: you can set Threshold as 'I hope the game usually doesn't go louder than this' and then set Ratio to control the peak of maximum expected volume.
>
> ![Compressor for Desktop Audio][Compressor Input-Output Graph]
>
> If you want to make a hard limit for the desktop audio, Limiter can be helpful.

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
[Compressor Steps]: ./image/compressor-steps.png "Step by step process to set up Compressor"
[Compressor Input-Output Graph]: ./image/compressor-io-graph.png "Compressor Concept in an Input-Output Graph"
[Window: Gain]: ./image/en/g-window.png "window of Gain"
[Window: Limiter]: ./image/en/l-window.png "window of Limiter"
