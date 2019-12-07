# Open source offline speech recognition for Android using Mozilla's DeepSpeech in Termux

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
```
#!/data/data/com.termux/files/usr/bin/bash
WORDS="$(speech2text | tail -1)"

echo "Recognized: $WORDS"
if [[ "$WORDS" =~ "light" ]]; then
    if [[ $WORDS =~ "on" ]]; then
        termux-tts-speak "Turning flashlight on"
        termux-torch on
    elif [[ $WORDS =~ "of" ]]; then
        termux-tts-speak "Turning flashlight off"
        termux-torch off
    fi  
    echo ""
elif [[ "$WORDS" =~ "heating" ]] || [[ "$WORDS" =~ "temperature" ]]; then
    termux-tts-speak "Your thermostat has been updated."
else
    termux-tts-speak "You said: $WORDS"
    sleep 3
fi
```

If you install the Termux:Widgets app and save the above script under "$HOME/.shortcuts/tasks/" and make it executable for example like this: `chmod "$HOME/.shortcuts/tasks/speech-command"` (speech-command is the name of the script).
You can then then create a widget that triggers the script. Or using the app HomeBot (open source) you can remap long-pressing the home button which usually triggers the Google voice assistent to run your speech-command script.


## Warning

This is a very new script that has barely been tested. You might also have to isntall a TTS Engine (Flite TTS Engine is a good open source one) because I'm using text-to-speech commands a few times.
