# Overview
This is dataset contains the synthesized soundscapes and crowdsourced audio annotations that accompany the paper, 

> M. Cartwright, A. Seals, J. Salamon, A. Williams, S. Mikloska, D. MacConnell, E. Law, J. Bello, and O. Nov. "Seeing sound: Investigating the effects of visualizations and complexity on crowdsourced audio annotations." In *Proceedings of the ACM on Human-Computer Interaction*, 1(1), 2017.

This paper investigated the effects of soundscape complexity and sound visualizations on the quality and speed of annotations of sound events (i.e. start time, end time, sound class, and proximity). In this dataset, we varied the soundscape complexity along two dimensions: maximum polyphony (3 levels) and Gini polyphony (2 levels). Maximum polyphony is the maximum number of sound events that occurred simultaneously in the soundscape. Gini polyphony is a measure of the concentration of sound events. For each of the 6 (3 x 2) combinations of complexity levels, we synthesized 10 soundscapes (using Scaper <LINK>), each of which was 10 seconds long, for a total of 60 soundscapes. Each soundscape was annotated by 90 participants from Amazon's Mechanical Turk—30 of which were aided by waveform visualization, 30 of which were aided by a spectrogram visualization, and 30 of which did not have any visualization aid. For more details on how this data was collected, please refer to the paper.

# Contents

There are 60 soundscape audio and annotation files.

## Audio files
The audio files are in WAV format and are named as follows: `soundscape-<soundscape_id>_m<max_polyphony_level>_g<gini_polyphony_level>.<wav>`, e.g. `soundscape-0-m0-g0.wav`

## Annotation files
The anotation files are in JAMS format and are named as follows: `soundscape-<soundscape_id>_m<max_polyphony_level>_g<gini_polyphony_level>.<jams>`, e.g. `soundscape-0-m0-g0.jams`, the annotation file for the soundscape in `soundscape-0-m0-g0.wav`

JAMS is a JSON-based audio annotation format. For details about this format and JAMS-specific reading and writing tools, refer to http://pythonhosted.org/jams/

To load a JAMS annotation file using Python (requires [Scaper](https://github.com/justinsalamon/scaper) for `sound_event` namespace defined in `scaper`):

```python
  import scaper
  jams_filename = 'soundscape0-m0-g0.jams'
  jam = scaper.jams.load(jams_filename)
```

There is one JAMS file for each soundscape. Each JAMS file includes both the ground-truth annotations as generated by the soundscape synthesizer, [Scaper](https://github.com/justinsalamon/scaper), and also each of the soundscape's 90 crowdsourced annotations.

### Ground-truth annotations
The first annotation is the ground-truth annotation (i.e. `jam.annotations[0]`) generated by [Scaper](https://github.com/justinsalamon/scaper) Each sound event within the ground truth annotation is described by its time (`jam.annotations[0].time`), duration (`jam.annotations[0].duration`), and value (`jam.annotations[0].value`), which contains additional attributes such as sound class (e.g. `jam.annotations[0].value[0]['label']`), signal-to-noise ratio (the [LUFS](https://tech.ebu.ch/docs/r/r128.pdf) ratio between the sound event and the noise floor—e.g. `jam.annotations[0].value[0]['snr']`), and the signal-to-mix-minus-one ratio (the LUFS ratio between the sound event and the other sound sources in the mix—e.g. `jam.annotations[0].values[0]['smm1r']`).

In addition, the sandbox of the ground-truth annotation (i.e. `jam.annotations[0].sandbox.scaper`) describes all of the Scaper parameters used to generate the soundscape.

### Crowdsourced annotations
The crowdsourced annotations are the remaining annotations starting at index 1, i.e. `jam.annotations[1:]`. Each sound event within a crowdsourced annotation is described by its perceived start time (e.g. `jam.annotations[1].time`), perceived duration (e.g. `jam.annotations[1].duration`), and value (e.g. `jam.annotations[1].value`), which contains additional attributes such as the perceived sound class (e.g. `jam.annotations[1].value[0]['label']`) and the perceived proximity (how close the participant perceived the event—*near*, *far*, or *not sure*).

The annotation metadata of each crowdsourced annotation contains additional information about the annotatation including attributes of the annotator (e.g. `jam.annotations[1].annotator_metadata.annotator`). These include:
* **participant_id** - a unique ID assigned to each participant
* **age** - the participant's self-reported age
* **gender** - the participant's self-reported gender identification
* **musical instrument experience** - the participant's response to: *Approximate your level of the following: - Experience playing a musical instrument* on a scale from 1 ("no experience") to 7 ("expert")
* **audio technology experience** - the participant's response to: *Approximate your level of the following: - Experience using audio recording and/or sound editing technology* on a scale from 1 ("no experience") to 7 ("expert")
* **sound labeling experience** - the participant's response to: *Approximate your level of the following: - Experience labeling sound recordings* on a scale from 1 ("no experience") to 7 ("expert")

In addition, the sandbox of the crowdsourced annotations (e.g. `jam.annotations[1].sandbox`) contains additional variables from our experiment such as the visualization, the gini polyphony level, the max polyphony level, the class label options, the annotation task index (order index in which the soundscape was presented to the participant), the task length.


# Cite
When referencing this paper and dataset, please use the following Bibtex citation:

```
  @article{Cartwright:SeeingSound:CSCW:17,
    Author = {Cartwright, M. and Seals, A. and Salamon, J. and Williams, A. and Mikloska, S. and MacConnell, D. and Law, E. and Bello, J.P. and Nov, O.},
    Journal = {Proceedings of the ACM on Human-Computer Interaction},
    Number = {1},
    Title = {Seeing Sound: Investigating the Effects of Visualizations and Complexity on Crowdsourced Audio Annotations},
    Volume = {1},
    Year = {2017}}
```

# Tools used to create this dataset
* [Audio-Annotator](https://github.com/CrowdCurio/audio-annotator)
* [Scaper](https://github.com/justinsalamon/scaper)
* [HearingScreening.js](https://github.com/mcartwright/hearing-screening.js)
* [CrowdCurio](https://www.crowdcurio.com)
* [Amazon's Mechanical Turk](https://www.mturk.com)

# Classes of sound events
The soundscapes in this dataset contain the following classes of sound events:

* *car horn honking*
* *dog barking*
* *engine idling*
* *gun shooting*
* *jackhammer drilling*
* *music playing*
* *people shouting*
* *people talking*
* *siren wailing*
