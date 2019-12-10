# Open source offline speech recognition for Android using Mozilla's DeepSpeech in Termux

## Requirements
- ~3GB of disk space during installation; afterwards only ~2GB
- [Termux](https://f-droid.org/app/com.termux)
- [Termux:API](https://f-droid.org/app/com.termux.api)

## Installation

- Install the following (open source) apps: Termux, Termux:API
- Open Termux and run
    `pkg i -y git && git clone https://github.com/T-vK/Termux-DeepSpeech.git && cd ./Termux-DeepSpeech && ./speech2text`

This will take a while beacuse it needs to download a pre-trained DeepSpeech model and a DeepSpeech release. It will probably also ask for microphone permissions (which are required for obvious reasons).

## Usage
If the installation was successful, you should now be able to use command `speech2text`.
`speech2text` will listen to your microphone for (by default) 2 seconds and then print the words that were recognized.

## Advanced usage
You could create bash scripts like this:
``` bash
#!/data/data/com.termux/files/usr/bin/bash

WORDS="$(speech2text)"                            # This will listen to the microphone for (by default) 2 seoncds and the write what you said in the variable WORDS

echo "Recognized: $WORDS"                         # Show what you just said

if [[ "$WORDS" =~ "light" ]]; then                # If what you said contained the word "light"
    if [[ $WORDS =~ "on" ]]; then                 # If what you said contained the word "on"
        termux-tts-speak "Turning flashlight on"  # Let a robot voice say "Turning flashlight on"
        termux-torch on                           # Turn the flashlight on
    elif [[ $WORDS =~ "of" ]]; then               # If what you said contained the word "of"
        termux-tts-speak "Turning flashlight off" # Let a robot voice say "Turning flashlight off"
        termux-torch off                          # Turn the flashlight off
    fi
elif [[ "$WORDS" =~ "heating" ]] || [[ "$WORDS" =~ "temperature" ]]; then   # If what you said contained the word "heating" or "temerature"
    # Do whatever here...
    echo "Hello"
else
    termux-tts-speak "You said: $WORDS"           # Let a robot voice repeat what it thought you said...
fi
```

If you install the [Termux:Widget](https://f-droid.org/app/com.termux.widget) app and save the above script under "$HOME/.shortcuts/tasks/" and make it executable for example like this: `chmod +x "$HOME/.shortcuts/tasks/speech-command"` (speech-command is the name of the script).
You can then then create a widget that triggers the script. Or using the app [HomeBot](https://f-droid.org/app/com.abast.homebot) (open source) you can remap long-pressing the home button which usually triggers the Google voice assistent to run your speech-command script.


## Warning

This is a very new script that has barely been tested. You might also have to install a TTS Engine ([Flite TTS Engine](https://f-droid.org/app/edu.cmu.cs.speech.tts.flite) is a good open source one) because I'm using text-to-speech commands a few times in the `Advanced usage` example.
