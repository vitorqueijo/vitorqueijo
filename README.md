# Vitor Queijo

[![Linkedin Badge](https://img.shields.io/badge/-vitorqueijo-blue?style=flat-square&logo=Linkedin&logoColor=black&link=https://www.linkedin.com/in/vitorqueijo/)](https://www.linkedin.com/in/vitorqueijo/)

## Basic Input
```json
basic_input = {
    "_class": "BackEnd Developer",
    "_version": "2022.08.21",
    "name": "Vitor Queijo",
    "ticks": 1200936262130930.0,
    "languages": {
        "python": {
                "ticks": 924421091820490.0,
                "library-coverage": [ 
                    "django2", 
                    "flask", 
                    "pyspark", 
                    "numpy", 
                    "nltk", 
                    "spacy", 
                    "pandas", 
                    "redis-py", 
                    "graphviz", 
                    "pygame" ,
                    "scrapy",
                    "b4s",
                    "unittest",
                    "pytest",
                    "mongodb",
                    "sqlite3",
                    "boto3"
                    ],
                "comment": "library-coverage focuses on key frameworks"
        },
        "csharp": {
            "ticks": 665237082308710.0,
            "library-coverage": [
                "ASP.NET",
                "ASP.NET Core",
                "Entity Framework",
                "Swashbuckle",
                "AutoMapper",
                "FluentValidation",
                "Serilog",
                "xUnit",
                "FluentAssertions",
                "RestSharp",
                "MongoDB"
            ],
            "comment": "library-coverage focuses on key frameworks"
        },
        "scala": {
            "ticks": 123515605792059.98,
            "library-coverage": [
                "log4j",
                "spark-redis",
                "awscala-emr",
                "awscala-s3",
                "awscala-stepfunctions",
                "awscala-redshift"
            ],
            "comment": "library-coverage focuses on key frameworks"
        },
    },
    "interests": {
        "NLP": "moderate",
        "ETL-ELT": "average",
        "Microsservices": "below average",
        "Unsupervised learning": "above average",
        "Genetic Algorithms": "high",
        "Game Development": "high",
        "Cryptography": "high"
    },
    "weird-interests":{
       "keywords": [ 
        "chess", 
        "image-generation-ai", 
        "gaming",
        "data",
        "privacy",
        "history",
        "cryptowatermark"
        ]
    }
}
```

## Setup

```python
import json
import Developer

json_input = json.loads(basic_input)

interests = [*json_input['interests'], *json_input['weird-interests']]
code_languages = json_input["languages"].keys()

vitor_queijo = Developer(json_input["name"], code_languages, interests)
```

## Ask Me Anything

#### Positive Answers Examples
```python
vitor_queijo.ask_me("do you like chess?")
vitor_queijo.ask_me("do you code in python?")
vitor_queijo.ask_me("do you like data privacy?")
```

<details><summary>Code Source</summary>
<p>

#### Perhaps it's mine BaseClass
```python
    import re
    from typing import List
    import random


    QA_pattern = r"^(.*?(\b{answer}\b)[^$]*)$"

    class Developer(BaseHuman):
        def __init__(self, name: str, codes: List[str], weird_interests: List[str]) -> None:

            super().__init__()
            self.name = name
            self.codes = codes
            self.weird_interests = weird_interests

        def __str__(self) -> str:
            return f"Hello, lovely person, I'm {self.name}."
        
        def __possible_topics(self) -> List[str]:
            return [*self.codes, *self.weird_interests]
        
        def __find_answer(self, question: str) -> str:
            possible_topics = self.possible_topics()

            answer = [x for x in possible_topics \
                if re.match(QA_pattern.format(answer=x), question, re.I)]

            if any(answer):
                for a in answer:
                    if a in self.codes:
                        return f"Yes, I do code in {a}!"
                    elif a in self.weird_interests:
                        return f"Yes, I do interest in {a}!"
                    else:
                        raise ReferenceError("Sorry, mate, I don't know about it.")

        def ask_me(self, question: str) -> None:
            if not question and not question.isspace():
                raise NameError(f"So...do you wanna talk about " + 
                    f"{random.choice(self.weird_interests)}?")
            try:
                print(self.__find_answer(question))
            except ReferenceError as rex:
                if hasattr(rex, 'message'):
                    print(
                        f"{rex.message} maybe you could try asking about: " +
                        f"{', '.join(random.sample(self.__possible_topics(), k=2))}"
                        )
            except Exception:
                print("i don't know what happened, it works on my machine.")
```
</p>
</details>

## License
[The Unlicense](https://choosealicense.com/licenses/unlicense/)
