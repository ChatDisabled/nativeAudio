
# What is this?
This is a collection of examples on how to make *"custom native audio"*. This will allow you to benefit from the audio engine in GTA without the use of NUI. I would highly suggest you take a look at this [GitHub repository](https://github.com/Monkeypolice188/Monkys-Audio-Research) to see what is possible (a LOT).

And a big thank you to everyone talking about it in the [CodeWalker discord](https://discord.gg/codewalker) and especially everyone I had personal contact with that led me to the small thing that I was missing to make this work

### Contributors ✨
<table>
  <tr>
    <td align="center"><a href="https://github.com/Ehbw"><img src="https://avatars.githubusercontent.com/u/106408826?v=4" width="100px;" alt=""/><br /><sub><b>Ehbw</b></sub></td>
    <td align="center"><a href="https://github.com/masonschafercodes"><img src="https://avatars.githubusercontent.com/u/57614646?v=4" width="100px;" alt=""/><br /><sub><b>Qwade</b></sub></a><br /></td>
  </tr>
</table>

## [SimpleSound](SimpleSound)
Simple sound entries as the name implies, are used for simple sounds. However it is broadly used as this is the beginning of every sound entry. Before a `.wav` sound is ready to be used, it needs to be registered first as a `SimpleSound`. Luckely for us it only takes one extra step to use these sounds and that is adding the sounds to a `SoundSet`. This is the perfect alternative for people using simple sound effects from resources like [Interact-Sound](https://github.com/plunkettscott/interact-sound) and [xSound](https://github.com/Xogy/xsound).

## [Weapon audio](weaponAudio)
Using the `WeaponAudioItem` entry inside of a `dat151` file, we can modify the `PlayerFire` entry. This will be streamed to every client thus everyone hears the same sound. This way we don't have to rely on the client downloading the appropiate files to modify their sounds. Furthermore we can finally adapt the sounds of addon weapons instead of relying on existing WeaponAudioItems.