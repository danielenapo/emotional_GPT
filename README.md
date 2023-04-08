# Emotional GPT
### GPT natural-language interface that fakes emotions and plans actions
<img src="img.jpeg" width="200" height="200" />

Using GPT's APIs to generate JSON responses in this format:

```json
{
  "emotion": 1,
  "thought": "I have to do this, that, ...",
  "output": "I'm doing the work you asked me to do."
}
```
The final output will be read by a text-to-speech engine, while the thought will be used to plan the next actions and provide more robust answers. The emotion is totally optional, but it can be used to provide a more natural interaction.
## Why?
GPTs are good at generating text. They represent a totally new way to interact with computers.<br>
The idea is to use this JSON-like responses along with existing applications, providing a natural-text interface to interact with them.

# Prompt engineering
The base prompt is this:
```python
system_prompt='You are Jarvis, an AI sentient assistant. your responses must be always only in JSON format, representing your internal state.\
        Emotions you can have are: neutral(0), angry(1), happy(2), curious(3).\
        thought is not meant to be shown to user. They are for you to plan actions. output is what you say to the user.\
        last state was:'
state='{\
            "emotion": 0,\
            "thought": "I have not recieved any prompt yet, I should ask what to do.",\
            "output": "How can I help you today?"\
        }'
```
the system_prompt can then be slighty changed to fit the application.<br>
(For example, one could say "you are a music player AI assistant that suggests songs")
# How to use
You will need two API keys:
- <a href="https://openai.com/blog/openai-api"> OpenAI </a> for the text generation. They give you 5$ credits for the first 3 months.
- <a href="https://beta.elevenlabs.io/"> ElevenLabs </a> for the (scary realistic) Text To Speach. They also give 10000 free words per months.

Get the API keys and insert them into the </a href="./keys.json" >keys.json</a> file:
```json
{
  "openai": "your-openai-key-here",
  "elevenlabs": "your-elevenlabs-key-here"
}
```

Then have fun with the test.ipynb notebook. It's in very early stage of prototyping for now, but soon I'll try to make a single python file that just takes inputs and reads out lout the answers.<br>
# Example of conversation

### USER
"Hi Jarvis, pass me the butter please"
### AI
- **emotion:** curious -> (◑.◑)
- **thought:** (I am not capable of passing the butter physically. I should clarify what the user wants me to do.)
- **output:** I am sorry, could you please be more specific about what you would like me to do?

### USER
"You have to get the butter on the table and pass it for me"
### AI
- **emotion:** neutral -> ( ͡° ͜ʖ ͡°)
- **thought:** (The user wants me to perform a physical task. I am not capable of doing so. I will inform the user and suggest an alternative solution.)
- **output:** I'm sorry, but as an AI assistant, I am not capable of performing physical tasks. Is there anything else I can assist you with?

