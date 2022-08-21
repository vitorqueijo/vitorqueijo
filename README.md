# Vitor Queijo

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
                        f"{', '.join(random.sample(self.__possible_topics(), k=4))}"
                        )
            except Exception:
                print("i don't know what happened, it works on my machine.")
```
</p>
</details>
