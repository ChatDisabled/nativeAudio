
### To begin with we are going to create a `.awc` container which will hold all the audio files.

1. Gather all the sounds you want to use. This is obviously personal preference and this can be done though https://www.youtube.com/ or whatever. Preferably these sounds should be in the `Waveform Audio File Format | .wav for short`. But these are hard to come by. Which is no problem as we can do this ourselves.

2. Once you got everything you want, you will need to convert these sounds to `.wav` files. This can be done however you want but I personally use Sony Vegas as that is what I am comfortable with. As long if you do what is written below there should be no problem whatever software you use.
    - Simply drag & drop one of the sounds in your software of choice, and render it back into a `.wav` with a sample rate (Hz) of 32.000, bit depth of 8 or 16 and it has to be in mono, not stereo. The format will be `PCM` or `ADPCM`. Do this for every sound you have[^1][^4][^5].

3. Now put all of these sound files in a folder. For the sake of this tutorial call this folder `custom_sounds`.

4. Using the template file included that is called `custom_sounds.awc.xml`, I want you to edit this file in whatever IDE you use. I already included 2 example sounds in the template.
    - Firstly change both the `<Name>` and `<FileName>` entries. `<FileName>` is going to be the filename of your converted sound files which you put in the folder `custom_sounds`. `<Name>` however can be anything you want but it is simply easier to keep this the same or rather similar.
    - `<Codec>` will be `PCM` since we converted the sounds into this format.
    - `<SampleRate>` will be `<SampleRate value="32000" />` because we used the 32kHz sample rate. The `<Samples>` value however needs to be calculated by you by doing `audio duration * sample rate`. If you don't know the exact duration I would highly advise you use [Audacity](https://www.audacityteam.org/) for this part. Once Audacity is installed simply drag the sound into it, double click to select the whole clip. The samples value will be displayed below[^2]. Fill this in inside the `.xml` file.

        - Now I'm no audio head, but there are other entries included which you can play with to prepare your sounds before use. But I would keep `<LoopPoint>` at minus 1 because otherwise your sound will keep looping if this is set at 0 for example. Have fun and play around with these entries.

5. Once you have added all of your sound entries you can go ahead and open CodeWalker[^3]. Make sure both your folder containing the sounds and the `.xml` file you just edited are on the same level so that wherever you put them you can see them both. Enable edit mode and right click to Import XML. Find your XML file and press done. Now you should have a working `.awc` container with all the sounds included. Upon importing, if you get `"Object reference not set to an instance of an object"`, it can be for a multitude of reasons such as:
  - Incorrect folder/file structure
  - .awc.xml file name does not match folder name
  - Soundname cannot be found in folder (either missing or typo in either filename or awc file entry)
  - The sound is stero (>=2 channels) instead of Mono
  - The sound is not PCM or ADPCM
  - Invalid XML entry (e.g. missing information, such as samples, name etc.)


### Now onto making the corresponding `.dat54` file

1. Using the included template `audioexample_sounds.dat54.rel.xml`. We are going to make 2 `SimpleSounds` which will be usable through a `soundset`. You can however include as many simple sounds as you want of course.

2. Editing a `.dat54.rel.xml` file

    - First we have the `<Name>` entry. This name will be used later on in the file and can be named however you want. But again for simplicity just name it the same way you did your sound name. Rockstar however uses some internal naming scheme depending on which type of sound you are adding. `MultitrackSound` for example end with `_mt`.
    
    - `<Header>`. Here you can change a lot of attributes of the sound. Most flags have already been discovered and I would highly suggest you look at this [GitHub repository](https://github.com/Monkeypolice188/Monkys-Audio-Research/blob/main/sounds.dat54/Dat54Sound%20Header) to get an idea of which flags are available. In the template I am using `0x00008004`. This can be broken down to `0x00000004` for Volume and `0x00008000` to change the category (Category is very important if we want to use a sound in a `soundset`!!!. Please keep this at scripted)

    - And finally the `<ContainerName>` and `<FileName>`. These two are to locate the actual sound inside of your `.awc` container. `<ContainerName>` will start from wherever your resource that is streaming the sounds is located. Following the example below as structure with the resource named `resourceAudio`. The entry in `<ContainerName>` should be `audiodirectory/custom_sounds`. `<FileName>` should be the name you gave the sound in your `.awc.xml` file (The `<Name>` entry not `<FileName>`!).
        ```bash
        resourceAudio
        │
        ├── audiodirectory
        │   └── custom_sounds.awc
        ├── data
        │   └── audioexample_sounds.dat54.rel
        ├── fxmanifest.lua
        ├── client.lua    
        ```

    - Once you have created all of your SimpleSounds you want. You will need to insert them all into a `SoundSet` to actually use them in game. The 2 example sounds are already inside of the template. You simply need to add your sounds. The `<Name>` entry here can be whatever you want. You can add more sounds inside of the `<SoundSets>` entry. `<ScriptName>` will be the name of the sound that you call inside of scripts. `<ChildSound>` will be what you named your `SimpleSound` from before in the same file.

3. Now you are once again ready to simply Import XML inside of CodeWalker and you should have a valid `.dat54.rel` file.

Following the same folder structure as mentioned above and a simple code snippet, you should now have working "native" sounds 😊. Thanks to everyone making this possible and spreading information on this topic. And I highly suggest you use [this repo](https://github.com/Monkeypolice188/Monkys-Audio-Research) and join the [CodeWalker discord](https://discord.gg/codewalker) to find more information about the topic

[^1]: https://media.discordapp.net/attachments/844240881283366962/1136305015754076210/V3R14LYUIVgpZw.png

[^2]: https://cdn.discordapp.com/attachments/803679370156965920/1136335474986860696/6knzX5lqLcjX4B.png

[^3]: As of writing, I used `CodeWalker30_dev44`

[^4]: A sample rate of 32kHz mostly gets used for simple sound effects. 44.1 and 48kHz gets used for songs. And 24kHz gets used for speech interactions.

[^5]: There seems to be some kind of limit on the size of the `.wav` and even the `.awc`. Limit is unknown(?) but keep it under ~1.5MB. Knowing that the base game files exceed this there *should* be a way to counteract this "limit".
