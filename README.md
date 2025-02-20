`pip install prlps_speller`


асинхронный спеллер с использованием API Yandex Speller.

ограничения для одного IP-адреса:

* на количество обращений к API - 10 000 обращений в сутки;
* на объем проверяемого текста - 10 000 000 символов в сутки.

параметры при создании экземпляра класса `YandexSpeller`:
- `format_text`: формат текста ('auto', 'html', 'text')
- `lang`: языки проверки ('en', 'ru', 'uk')
- `check_yo`: учитывать букву ё
- `ignore_urls`: игнорировать ссылки
- `ignore_tags`: игнорировать HTML-теги
- `ignore_capitalization`: игнорировать регистр
- `ignore_digits`: игнорировать цифры
- `find_repeat_words`: искать повторяющиеся слова


```python
from asyncio import run as async_run
from prlps_speller import YandexSpeller

async def test():
    speller = YandexSpeller(
        format_text='html',
        lang=['ru', 'en'],
        check_yo=True,
        ignore_urls=True,
        ignore_tags=True,
        ignore_capitalization=True,
        ignore_digits=True,
    )
    text = 'елка била бальшая и високоя, мольчешечки радывались и плисали вакруг, напивая песинькю "Jinkl Belz".'
    # получить готовый исправленный текст:
    fixed = await speller.spelled(text)
    print(fixed)  # елка была большая и высокая, мальчишечки радовались и плясали вокруг, напевая песенку "Jingle Bells".

    # вывод позиций ошибок и вариантов исправлений:
    changes = await speller.spell_text(text)
    print(changes)


# запуск теста:
async_run(test())

```