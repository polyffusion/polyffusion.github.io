---
layout: home
---
<head>
    <link rel="stylesheet" href="styles.css">
</head>

\| <a href="https://arxiv.org/abs/2307.10304">Paper</a> \| <a href="https://github.com/aik2mlj/polyffusion">Code Repository</a> \|

<!-- <hr color="#E8E8E8"> -->
<!-- <br> -->
We propose ***Polyffusion***, a **diffusion model** that generates polyphonic music scores by regarding music as image-like piano roll representations. The model is capable of controllable music generation with two paradigms: *internal control* and *external control*. Internal control refers to the process in which users pre-define a part of the music and then let the model infill the rest. External control conditions the model with external yet related information, such as chord, texture, or other features, via the cross-attention mechanism. We show that by using internal and external controls, Polyffusion unifies a wide range of music creation tasks, including melody generation given accompaniment, accompaniment generation given melody, arbitrary music segment inpainting, and music arrangement given chords or textures.

In each MIDI visualization block, <font color="#2B7ADB">blue</font> notes denote the generated results. Except for the iterative inpainting demo, all the demos are 8-bar long (16s).
<br>
<br>

## Unconditional Generation

<section class="center-stuff alone">
    <midi-player src="/media/uncond_pop909wm_1.mid" sound-font visualizer="#Vis_uncond"> </midi-player>
    <midi-player src="/media/uncond_pop909_1.mid" sound-font visualizer="#Vis_uncond"> </midi-player>
    <midi-player src="/media/uncond_pop909wm_0.mid" sound-font visualizer="#Vis_uncond"> </midi-player>
    <midi-player src="/media/uncond_pop909_3.mid" sound-font visualizer="#Vis_uncond"> </midi-player>
    <midi-visualizer type="piano-roll" id="Vis_uncond"> </midi-visualizer>
</section>
<br>

## Melody generation given accompaniment

With the pre-defined accompaniment as follows,
<div class="center-stuff">
<section class="vis inp">
    <midi-player src="/media/uncond_inp_above_acc.mid" sound-font visualizer="#Vis_inp_above_acc">
    </midi-player>
    <midi-visualizer src="/media/uncond_inp_above_acc.mid" type="piano-roll" id="Vis_inp_above_acc">
    </midi-visualizer>
</section>
</div>

the model inpaints the upper melody via masked generation:
<section class="center-stuff alone inp">
    <midi-player src="/media/uncond_inp_above_0_split.mid" sound-font visualizer="#Vis_inp_above"> </midi-player>
    <midi-player src="/media/uncond_inp_above_1_split.mid" sound-font visualizer="#Vis_inp_above"> </midi-player>
    <midi-visualizer type="piano-roll" id="Vis_inp_above"> </midi-visualizer>
</section>
<br>


## Accompaniment generation given melody

With the pre-defined melody as follows,
<div class="center-stuff">
<section class="vis inp">
    <midi-player src="/media/uncond_inp_below_ode_mld.mid" sound-font visualizer="#Vis_inp_below_mld_1"> </midi-player>
    <midi-visualizer src="/media/uncond_inp_below_ode_mld.mid" type="piano-roll" id="Vis_inp_below_mld_1">
    </midi-visualizer>
</section>
</div>

the model inpaints the lower accompaniment via masked generation:
<section class="center-stuff alone inp">
    <midi-player src="/media/uncond_inp_below_ode_0_split.mid" sound-font visualizer="#Vis_inp_below_1"> </midi-player>
    <midi-player src="/media/uncond_inp_below_ode_1_split.mid" sound-font visualizer="#Vis_inp_below_1"> </midi-player>
    <midi-visualizer type="piano-roll" id="Vis_inp_below_1"> </midi-visualizer>
</section>

Here is another example. Given the melody as follows,
<div class="center-stuff">
<section class="vis inp">
    <midi-player src="/media/uncond_inp_below_canon_mld.mid" sound-font visualizer="#Vis_inp_below_mld"> </midi-player>
    <midi-visualizer src="/media/uncond_inp_below_canon_mld.mid" type="piano-roll" id="Vis_inp_below_mld">
    </midi-visualizer>
</section>
</div>

the model inpaints the lower accompaniment:
<section class="center-stuff alone inp">
    <midi-player src="/media/uncond_inp_below_canon_0_split.mid" sound-font visualizer="#Vis_inp_below"> </midi-player>
    <midi-player src="/media/uncond_inp_below_canon_1_split.mid" sound-font visualizer="#Vis_inp_below"> </midi-player>
    <midi-visualizer type="piano-roll" id="Vis_inp_below"> </midi-visualizer>
</section>
<br>

## Arbitrary segment inpainting

With the pre-defined segment as follows,
<div class="center-stuff">
<section class="vis inp">
    <midi-player src="/media/uncond_inp_bars_orig.mid" sound-font visualizer="#Vis_inp_bars_orig"> </midi-player>
    <midi-visualizer src="/media/uncond_inp_bars_orig.mid" type="piano-roll" id="Vis_inp_bars_orig"> </midi-visualizer>
</section>
</div>

the model re-generates the 3rd, 4th, 5th, and 7th bars via masked generation:
<section class="center-stuff alone inp">
    <midi-player src="/media/uncond_inp_bars_0.mid" sound-font visualizer="#Vis_inp_bars"> </midi-player>
    <midi-player src="/media/uncond_inp_bars_1.mid" sound-font visualizer="#Vis_inp_bars"> </midi-player>
    <midi-visualizer type="piano-roll" id="Vis_inp_bars"> </midi-visualizer>
</section>
<br>

## Iterative inpainting for long-term generation

Polyffusion can generate long-term music by iteratively inpainting the future given the past. Here is a 64-bar generation:
<section class="vis">
    <midi-player src="/media/uncond_autoreg_0.mid" sound-font visualizer="#Vis_inp_autoreg"> </midi-player>
    <midi-visualizer src="/media/uncond_autoreg_0.mid" type="piano-roll" id="Vis_inp_autoreg"> </midi-visualizer>
</section>
<br>

## Generation with chord conditioning

By feeding the following chord progression as the condition of the generation (chords are first encoded by <a href="https://arxiv.org/abs/2008.07122">a pre-trained VAE</a>),
<div class="center-stuff">
<section class="vis inp">
    <midi-player src="/media/chd_v_chd.mid" sound-font visualizer="#Vis_chd_v_chd"> </midi-player>
    <midi-visualizer src="/media/chd_v_chd.mid" type="piano-roll" id="Vis_chd_v_chd"> </midi-visualizer>
</section>
</div>

the model can generate music scores that follow the given chord progression:
<section class="center-stuff alone">
    <midi-player src="/media/chd_v_0.mid" sound-font visualizer="#Vis_chd_v_nog"> </midi-player>
    <!-- <midi-player src="/media/chd_v_1.mid" sound-font visualizer="#Vis_chd_v"> </midi-player> -->
    <midi-player src="/media/chd_v_2.mid" sound-font visualizer="#Vis_chd_v_nog"> </midi-player>
    <midi-visualizer type="piano-roll" id="Vis_chd_v_nog"> </midi-visualizer>
</section>

Moreover, by setting the guidance scale as 5 with *Classifier-free Guidance*, the generation involves more in-chord tones:
<section class="center-stuff alone">
    <midi-player src="/media/chd_gs_5.mid" sound-font visualizer="#Vis_chd_v_g"> </midi-player>
    <midi-visualizer type="piano-roll" id="Vis_chd_v_g"> </midi-visualizer>
</section>

<!-- <section id="inp"> -->
<!--     Chord progression (condition): -->
<!--     <midi-player src="/media/chd_gs_chd.mid" sound-font visualizer="#Vis_chd_gs_chd"> </midi-player> -->
<!--     <midi-visualizer src="/media/chd_gs_chd.mid" type="piano-roll" id="Vis_chd_gs_chd"> </midi-visualizer> -->
<!-- </section> -->

<!-- Generation (same seed with different guidance scales): -->
<!-- <br> -->
<!-- guidance scale = 1 -->
<!-- <midi-player src="/media/chd_gs_1.mid" sound-font visualizer="#Vis_chd_gs"> </midi-player> -->
<!-- guidance scale = 3 -->
<!-- <midi-player src="/media/chd_gs_3.mid" sound-font visualizer="#Vis_chd_gs"> </midi-player> -->
<!-- guidance scale = 5 -->
<!-- <midi-player src="/media/chd_gs_5.mid" sound-font visualizer="#Vis_chd_gs"> </midi-player> -->
<!-- guidance scale = 10 -->
<!-- <midi-player src="/media/chd_gs_10.mid" sound-font visualizer="#Vis_chd_gs"> </midi-player> -->
<!-- <midi-visualizer type="piano-roll" id="Vis_chd_gs"> </midi-visualizer> -->
<br>

## Generation with texture conditioning

By feeding the following music texture as the condition of the generation (the texture is encoded by <a href="https://arxiv.org/abs/2008.07122">a pre-trained VAE</a>),
<div class="center-stuff">
<section class="vis inp">
    <midi-player src="/media/txt_v_txt.mid" sound-font visualizer="#Vis_txt_v_txt"> </midi-player>
    <midi-visualizer src="/media/txt_v_txt.mid" type="piano-roll" id="Vis_txt_v_txt"> </midi-visualizer>
</section>
</div>

the model can generate music scores that inherit the given music texture:
<section class="center-stuff alone">
    <midi-player src="/media/txt_v_0.mid" sound-font visualizer="#Vis_txt_v_nog"> </midi-player>
    <midi-player src="/media/txt_v_1.mid" sound-font visualizer="#Vis_txt_v_nog"> </midi-player>
    <!-- <midi-player src="/media/txt_v_2.mid" sound-font visualizer="#Vis_txt_v_nog"> </midi-player> -->
    <midi-visualizer type="piano-roll" id="Vis_txt_v_nog"> </midi-visualizer>
</section>

<!-- Generation (guidance scale = 5): -->
<!-- <section class="center-stuff alone"> -->
<!--     <midi-player src="/media/txt_gs_5.mid" sound-font visualizer="#Vis_txt_v_g"> </midi-player> -->
<!--     <midi-visualizer type="piano-roll" id="Vis_txt_v_g"> </midi-visualizer> -->
<!-- </section> -->

<!-- <section id="inp"> -->
<!--     Texture MIDI (condition): -->
<!--     <midi-player src="/media/txt_gs_txt.mid" sound-font visualizer="#Vis_txt_gs_txt"> </midi-player> -->
<!--     <midi-visualizer src="/media/txt_gs_txt.mid" type="piano-roll" id="Vis_txt_gs_txt"> </midi-visualizer> -->
<!-- </section> -->

<!-- Generation (same seed with different guidance scales): -->
<!-- <br> -->
<!-- guidance scale = 1 -->
<!-- <midi-player src="/media/txt_gs_1.mid" sound-font visualizer="#Vis_txt_gs"> </midi-player> -->
<!-- guidance scale = 3 -->
<!-- <midi-player src="/media/txt_gs_3.mid" sound-font visualizer="#Vis_txt_gs"> </midi-player> -->
<!-- guidance scale = 5 -->
<!-- <midi-player src="/media/txt_gs_5.mid" sound-font visualizer="#Vis_txt_gs"> </midi-player> -->
<!-- guidance scale = 10 -->
<!-- <midi-player src="/media/txt_gs_10.mid" sound-font visualizer="#Vis_txt_gs"> </midi-player> -->
<!-- <midi-visualizer type="piano-roll" id="Vis_txt_gs"> </midi-visualizer> -->
<br>

## Chord-specified accompaniment generation given melody

This is a hybrid control case where we want to generate the corresponding accompaniment for a melody, while further specifying its chord progression. The melody is given as follows:
<div class="center-stuff">
<section class="vis inp">
    <midi-player src="/media/uncond_inp_below_canon_mld.mid" sound-font visualizer="#Vis_chd_inp_below_mld">
    </midi-player>
    <midi-visualizer src="/media/uncond_inp_below_canon_mld.mid" type="piano-roll" id="Vis_chd_inp_below_mld">
    </midi-visualizer>
</section>
</div>

And the chord progression we want the generated accompaniment to comply with is as follows:
<div class="center-stuff">
<section class="vis inp">
    <midi-player src="/media/chd_v_chd.mid" sound-font visualizer="#Vis_chd_inp_below_chd"> </midi-player>
    <midi-visualizer src="/media/chd_v_chd.mid" type="piano-roll" id="Vis_chd_inp_below_chd"> </midi-visualizer>
</section>
</div>

The model takes both the controls and inpaint the accompaniment:
<section class="center-stuff alone inp">
    <midi-player src="/media/chd_inp_below_canon_0_split.mid" sound-font visualizer="#Vis_chd_inp_below"> </midi-player>
    <midi-player src="/media/chd_inp_below_canon_1_split.mid" sound-font visualizer="#Vis_chd_inp_below"> </midi-player>
    <midi-visualizer type="piano-roll" id="Vis_chd_inp_below"> </midi-visualizer>
</section>
<br>

## Texture-specified melody generation given accompaniment

This is a hybrid control case where we want to generate the corresponding melody for a accompaniment, while further specifying its music texture. The accompaniment is given as follows:
<div class="center-stuff">
<section class="vis inp">
    <midi-player src="/media/txt_inp_above_acc.mid" sound-font visualizer="#Vis_txt_inp_above_acc"> </midi-player>
    <midi-visualizer src="/media/txt_inp_above_acc.mid" type="piano-roll" id="Vis_txt_inp_above_acc">
    </midi-visualizer>
</section>
</div>

And the music texture we want the generated melody to inherit is as follows:
<div class="center-stuff">
<section class="vis inp">
    <midi-player src="/media/txt_inp_above_txt.mid" sound-font visualizer="#Vis_txt_inp_above_txt"> </midi-player>
    <midi-visualizer src="/media/txt_inp_above_txt.mid" type="piano-roll" id="Vis_txt_inp_above_txt"> </midi-visualizer>
</section>
</div>

The model takes both the controls and inpaint the melody:
<section class="center-stuff alone inp">
    <midi-player src="/media/txt_inp_above_0.mid" sound-font visualizer="#Vis_txt_inp_above"> </midi-player>
    <midi-player src="/media/txt_inp_above_1.mid" sound-font visualizer="#Vis_txt_inp_above"> </midi-player>
    <midi-visualizer type="piano-roll" id="Vis_txt_inp_above"> </midi-visualizer>
</section>
<br>


<script
    src="https://cdn.jsdelivr.net/combine/npm/tone@14.7.58,npm/@magenta/music@1.23.1/es6/core.js,npm/focus-visible@5,npm/html-midi-player@1.5.0"></script>
<script>
    pianorolls = document.querySelectorAll("midi-visualizer");
    for (let i = 0; i < pianorolls.length; i++) {
        pianorolls[i].config = {
            noteHeight: 5
        };
    }
</script>

Thanks <a href="https://cifkao.github.io/html-midi-player/">html-midi-player</a> for the excellent MIDI visualization.
