
## Using Google-Translate API to translate texts to different languages

Under their AI & ML offerings, __google__ allows users to access their translation API which powers their Google Translate product. In recent years, Google has made huge strides in terms of improving their NLP capabilites and it would be very difficult for any developer to come up with their own translation toolkit. 

So for any translation use case, it makes sense for us to utilize the APIs that are provided by Google for translation. This page points you to the official page: [Google Translate API](https://cloud.google.com/translate/)


### This walk-through aims to guide you through a barebones implementation of a translation using this API

We would be writing a function which takes in a text input and outputs the translated text given a target languge. Google's service is very good at detecting the source language of the text input so giving that input is optional.

#### Following packages should be installed:
- google-cloud
- google-cloud-translate
- google-api-python-client


```python
from google.cloud import translate
import os
```


```python
# cred_file points to the API key that you would need to download from Google
# The key should be enabled to use the credential file
cred_file = r'C:\Users\Vivek\Documents\learn stuff\fall\unstructured\google-translate--vavlani-71362c26d436.json'
os.environ['GOOGLE_APPLICATION_CREDENTIALS'] = cred_file
```

### `tr_text` function is the main function which takes in a text string and converts it to a target language

You just need to initialize the `Client()` from the translate module of `google.cloud`
The call to translate just specifies the target_language & text


```python
def tr_text(text, target='en'):
    tr_client = translate.Client()
    result = tr_client.translate(text, target_language=target)
    print(f'Original Text: {result["input"]}')
    print(f'Translation: {result["translatedText"]}')
    print(f'Detected Source Language: {result["detectedSourceLanguage"]}')
    return result
```

### Here we convert a text from Hindi to English using the function that we just wrote


```python
demo_text = "इस पृष्ठ पर इन्टरनेट पर उपलब्ध विभिन्न हिन्दी एवं देवनागरी सम्बंधित साधनों की कड़ियों की सूची है। इसमें ऑनलाइन एवं ऑफ़लाइन उपकरण (टूल्स) शामिल हैं।"
result = tr_text(demo_text)
```

    Original Text: इस पृष्ठ पर इन्टरनेट पर उपलब्ध विभिन्न हिन्दी एवं देवनागरी सम्बंधित साधनों की कड़ियों की सूची है। इसमें ऑनलाइन एवं ऑफ़लाइन उपकरण (टूल्स) शामिल हैं।
    Translation: This page on the internet is a list of links to various resources related to Hindi and the Devanagari. This includes online and offline tools (tools).
    Detected Source Language: hi
    


```python
print(result)
```

    {'translatedText': 'This page on the internet is a list of links to various resources related to Hindi and the Devanagari. This includes online and offline tools (tools).', 'detectedSourceLanguage': 'hi', 'input': 'इस पृष्ठ पर इन्टरनेट पर उपलब्ध विभिन्न हिन्दी एवं देवनागरी सम्बंधित साधनों की कड़ियों की सूची है। इसमें ऑनलाइन एवं ऑफ़लाइन उपकरण (टूल्स) शामिल हैं।'}
    

### Available Languages

There are a lot of languages available in the API right now and this list should keep growing. Below we see a mapping from language to language name


```python
tr_client = translate.Client()
tr_client.get_languages()
```




    [{'language': 'af', 'name': 'Afrikaans'},
     {'language': 'sq', 'name': 'Albanian'},
     {'language': 'am', 'name': 'Amharic'},
     {'language': 'ar', 'name': 'Arabic'},
     {'language': 'hy', 'name': 'Armenian'},
     {'language': 'az', 'name': 'Azerbaijani'},
     {'language': 'eu', 'name': 'Basque'},
     {'language': 'be', 'name': 'Belarusian'},
     {'language': 'bn', 'name': 'Bengali'},
     {'language': 'bs', 'name': 'Bosnian'},
     {'language': 'bg', 'name': 'Bulgarian'},
     {'language': 'ca', 'name': 'Catalan'},
     {'language': 'ceb', 'name': 'Cebuano'},
     {'language': 'ny', 'name': 'Chichewa'},
     {'language': 'zh', 'name': 'Chinese (Simplified)'},
     {'language': 'zh-TW', 'name': 'Chinese (Traditional)'},
     {'language': 'co', 'name': 'Corsican'},
     {'language': 'hr', 'name': 'Croatian'},
     {'language': 'cs', 'name': 'Czech'},
     {'language': 'da', 'name': 'Danish'},
     {'language': 'nl', 'name': 'Dutch'},
     {'language': 'en', 'name': 'English'},
     {'language': 'eo', 'name': 'Esperanto'},
     {'language': 'et', 'name': 'Estonian'},
     {'language': 'tl', 'name': 'Filipino'},
     {'language': 'fi', 'name': 'Finnish'},
     {'language': 'fr', 'name': 'French'},
     {'language': 'fy', 'name': 'Frisian'},
     {'language': 'gl', 'name': 'Galician'},
     {'language': 'ka', 'name': 'Georgian'},
     {'language': 'de', 'name': 'German'},
     {'language': 'el', 'name': 'Greek'},
     {'language': 'gu', 'name': 'Gujarati'},
     {'language': 'ht', 'name': 'Haitian Creole'},
     {'language': 'ha', 'name': 'Hausa'},
     {'language': 'haw', 'name': 'Hawaiian'},
     {'language': 'iw', 'name': 'Hebrew'},
     {'language': 'hi', 'name': 'Hindi'},
     {'language': 'hmn', 'name': 'Hmong'},
     {'language': 'hu', 'name': 'Hungarian'},
     {'language': 'is', 'name': 'Icelandic'},
     {'language': 'ig', 'name': 'Igbo'},
     {'language': 'id', 'name': 'Indonesian'},
     {'language': 'ga', 'name': 'Irish'},
     {'language': 'it', 'name': 'Italian'},
     {'language': 'ja', 'name': 'Japanese'},
     {'language': 'jw', 'name': 'Javanese'},
     {'language': 'kn', 'name': 'Kannada'},
     {'language': 'kk', 'name': 'Kazakh'},
     {'language': 'km', 'name': 'Khmer'},
     {'language': 'ko', 'name': 'Korean'},
     {'language': 'ku', 'name': 'Kurdish (Kurmanji)'},
     {'language': 'ky', 'name': 'Kyrgyz'},
     {'language': 'lo', 'name': 'Lao'},
     {'language': 'la', 'name': 'Latin'},
     {'language': 'lv', 'name': 'Latvian'},
     {'language': 'lt', 'name': 'Lithuanian'},
     {'language': 'lb', 'name': 'Luxembourgish'},
     {'language': 'mk', 'name': 'Macedonian'},
     {'language': 'mg', 'name': 'Malagasy'},
     {'language': 'ms', 'name': 'Malay'},
     {'language': 'ml', 'name': 'Malayalam'},
     {'language': 'mt', 'name': 'Maltese'},
     {'language': 'mi', 'name': 'Maori'},
     {'language': 'mr', 'name': 'Marathi'},
     {'language': 'mn', 'name': 'Mongolian'},
     {'language': 'my', 'name': 'Myanmar (Burmese)'},
     {'language': 'ne', 'name': 'Nepali'},
     {'language': 'no', 'name': 'Norwegian'},
     {'language': 'ps', 'name': 'Pashto'},
     {'language': 'fa', 'name': 'Persian'},
     {'language': 'pl', 'name': 'Polish'},
     {'language': 'pt', 'name': 'Portuguese'},
     {'language': 'pa', 'name': 'Punjabi'},
     {'language': 'ro', 'name': 'Romanian'},
     {'language': 'ru', 'name': 'Russian'},
     {'language': 'sm', 'name': 'Samoan'},
     {'language': 'gd', 'name': 'Scots Gaelic'},
     {'language': 'sr', 'name': 'Serbian'},
     {'language': 'st', 'name': 'Sesotho'},
     {'language': 'sn', 'name': 'Shona'},
     {'language': 'sd', 'name': 'Sindhi'},
     {'language': 'si', 'name': 'Sinhala'},
     {'language': 'sk', 'name': 'Slovak'},
     {'language': 'sl', 'name': 'Slovenian'},
     {'language': 'so', 'name': 'Somali'},
     {'language': 'es', 'name': 'Spanish'},
     {'language': 'su', 'name': 'Sundanese'},
     {'language': 'sw', 'name': 'Swahili'},
     {'language': 'sv', 'name': 'Swedish'},
     {'language': 'tg', 'name': 'Tajik'},
     {'language': 'ta', 'name': 'Tamil'},
     {'language': 'te', 'name': 'Telugu'},
     {'language': 'th', 'name': 'Thai'},
     {'language': 'tr', 'name': 'Turkish'},
     {'language': 'uk', 'name': 'Ukrainian'},
     {'language': 'ur', 'name': 'Urdu'},
     {'language': 'uz', 'name': 'Uzbek'},
     {'language': 'vi', 'name': 'Vietnamese'},
     {'language': 'cy', 'name': 'Welsh'},
     {'language': 'xh', 'name': 'Xhosa'},
     {'language': 'yi', 'name': 'Yiddish'},
     {'language': 'yo', 'name': 'Yoruba'},
     {'language': 'zu', 'name': 'Zulu'}]


