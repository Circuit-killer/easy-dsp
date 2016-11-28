# Intro

This part explains how to get the audio streams in python code and how to send results to the webapp, so it can display them in live.

## How it works

It is important to understand that the code written in the editor in the webapp will be inserted in the file `base-program.py`, at the line `#####INSERT: Here insert code`.
So pre-existing functions and variables will be accessible, whereas you will not see them in the editor.

## Reading the configuration

Four variables contain the configuration:

* `rate`: the rate in bits/second;
* `channels`: the number of channels;
* `buffer_frames`: the number of audio frames contained in one buffer;
* `volume`: the volume between 0 and 100.

These are read-only, and you must not change them!

## Receiving the audio streams

A function `handleData(buffer)` must be defined in your code.
It will be called each time a new audio buffer is received.

The parameter `buffer` will contain an array of size `buffer_frames` containing arrays of size `channels` containing integers between -32 767 and +32 767.

An example with 5 frames per buffer and 2 channels:

```python
[
  [100, 300],
  [80, 240],
  [130, 0],
  [-800, 123],
  [-400, 0]
]
```

## Using the data handlers

After you performed some algorithms on the audio streams, you may want to display some outputs, like charts, histograms or new audio streams.
What you have to do is to send the data you want to display to a **data handler** of the webapp.
You have two simple steps to do:

1. You create a new data handler using the function `addHandler(name, type, parameters)` which returns an object representing this new instance;
2. You send data to this instance using its method `sendData(data)`.

Once you call the function `addHandler`, a new tab will be created in the webapp, with the name `name` you specified, and the chart/plot/audio player will appear inside.
You can use the part [Data Handlers](data-handlers.md) to see which *types* of data handlers exist, which parameters are supported, and which structure the `data` you send must follow.