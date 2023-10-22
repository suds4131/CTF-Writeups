### Syncopated Beat

We are given a zip file with 2 wav files, they are `mysterious_music.wav` and `Syncopated-Beat-2023.wav`, the second one contains music with some distorted voice in the middle.

From description of the challenge, something about `EVIL` in songs is mentioned. There is a huge conspiracy theory that reversing some songs spits out recordings of the devil lol.

So we reverse the distorted part and we see it is instructing us to use an audio steganography tool used in Mr. Robot with name of new CTO of Evil Corp(all caps, no spaces) as password. I finished watching Mr. Robot recently so I know it has to be Deep Sound, or you can even google for Mr. Robot audio steganography.
Audacity Reverse: Select all -> Effect -> Pitch and Tempo -> Reverse

I have uploaded the reversed version here, so you can listen to it if you want to.[Reversed Audio](https://github.com/suds4131/CTF-Writeups/blob/main/DEADFACE_CTF_2023/Steganography/Syncopated-Beat-2023-convo-reversed.wav)

<details>
  <summary>Password is a series spoiler. Warning.</summary>
  TYRELLWELLICK
</details>

Opening `mysterious_music.wav` in Deep Sound and using the password, we can extract a hidden file named `ozzy-mandias.jpeg` which has the final flag.

![Opening the file in Deep Sound.](https://raw.githubusercontent.com/suds4131/CTF-Writeups/main/DEADFACE_CTF_2023/Steganography/deep_sound_mysterious_music.png)

### Flag

`flag{Lookout_COVID_BATZ!!!}`
