# Lex Jeopardy Workshop

## Introduction
" 10/27 探索未來對話式科技 " ☁ 親手帶你做智慧語音助理：輕鬆上手 Amazon Lex 工作坊 ☁

## Lambda Part Setup
Import the package we need.

```python
import json
import random
import requests
```

```python
""" Helpers to call jService (https://jservice.io/) """

def get_question(category):

    id = {
        'Pop Music' : 2,
        'Sport' : 81,
        'Geography' : 158
    }

    try:
        payload = { 'id' : str(id[category]) }
        url = 'https://jservice.io/api/category'
        r = requests.get(url, params=payload)
        questions = r.json()['clues']
        q = random.choice(questions)
        return q['question'] + '  →  ' + q['answer']
    except:
        return 'Oops! Our question set is out of service. Please try it later.'
```

```python
""" Main handler """

def lambda_handler(event, context):

    intent_name = event['interpretations'][0]['intent']['name']
    slots = event['interpretations'][0]['intent']['slots']
    category = slots['CategoryName']['value']['interpretedValue']
    message = get_question(category)

    response = {
       'sessionState' : {
            'dialogAction' : {
                'type' : 'Close'
            },
            'intent' : {
                'name' : intent_name,
                'state' : 'Fulfilled'
            }
       },
        'messages': [
             {
                'contentType' : 'PlainText',
                'content' : message
             }
        ]
    }

    return response
```

## Lex Part Setup

### Bot

### Intent

### Utterance

### Slot

### Fulfillment

## CONTACT INFO.

> AWS Educate Cloud Ambassador, Technical Support </br>
> **Hugo ChunHo Lin**
> 
> <aside>
>   📩 E-mail: <a href="mailto:hugo970217@gmail.com">hugo970217@gmail.com</a>
> <br>
>   🧳 Linkedin: <a href="https://www.linkedin.com/in/1chooo/">Hugo ChunHo Lin</a>
> <br>
>   👨🏻‍💻 GitHub: <a href="https://github.com/1chooo">1chooo</a>
>    
> </aside>

## License
Released under [MIT](./LICENSE) by [AWS Educate TW](https://aws.amazon.com/tw/education/awseducate/), [Hugo ChunHo Lin](https://github.com/1chooo).

This software can be modified and reused without restriction.
The original license must be included with any copies of this software.
If a significant portion of the source code is used, please provide a link back to this repository.
