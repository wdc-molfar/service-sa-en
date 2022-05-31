# Програмний модуль **"service-sa-en"**

**Програмний модуль `service-sa-en` – "Програмний модуль виявлення емоційного забарвлення текстів інформаційних повідомлень поданих англійською мовою"**, який написаний мовою програмування `JavaScript` та `Python`, призначений для виявлення емоційного забарвлення текстів інформаційних повідомлень, що подані англійською мовою, за допомогою навченої засобами [fastText](https://github.com/facebookresearch/fastText) англійської моделі сентимент-аналізу.

Для навчання класифікатора [fastText](https://github.com/facebookresearch/fastText) спочатку була здійснена попередня обробка й формування збалансованого навчального набору даних у вигляді текстового файлу [en.txt](https://github.com/wdc-molfar/sentiment-datasets/tree/main/train), який міститься у архіві, що доступний за посиланням [https://github.com/wdc-molfar/sentiment-datasets/tree/main/train](https://github.com/wdc-molfar/sentiment-datasets/tree/main/train). Більш детальний [опис](https://github.com/wdc-molfar/sentiment-datasets) тренувального набору текстових даних, призначеного для навчання моделі сентимент-аналізу українських текстів інформаційних повідомлень та сам [тренувальний](https://github.com/wdc-molfar/sentiment-datasets/tree/main/train) та [тестовий](https://github.com/wdc-molfar/sentiment-datasets/tree/main/test) набори англійських текстових інформаційних повідомлень позитивної та негативної тональності розміщені у репозиторії [**`sentiment-datasets`**](https://github.com/wdc-molfar/sentiment-datasets).

В результаті навчання засобами [fastText](https://github.com/facebookresearch/fastText) для тренувального набору даних [en.txt](https://github.com/wdc-molfar/sentiment-datasets/tree/main/train) була отримана модель для сентимент-аналізу текстів інформаційних повідомлень поданих англійською мовою. Після процедури квантування модель була збережена у файлі формату `.ftz`  - [en.ftz](https://drive.google.com/u/0/uc?id=12MLctdlgzqw_tMYizZOzzY1Ja8AYK2AH&export=download&confirm=t).
Для [тестового набору даних](https://github.com/wdc-molfar/sentiment-datasets/tree/main/test) було отримано оцінку якості навчання англійської моделі – `99,7%`.

### Зміст
- [Позначення та найменування програмного модуля](#name)
- [Програмне забезпечення, необхідне для функціонування програмного модуля](#software)
- [Функціональне призначення](#function)
- [Опис логічної структури](#structure)
- [Використовувані технічні засоби](#hardware)
- [Виклик та завантаження](#run)
- [Приклад вхідних даних](#inputdata)
- [Приклад вихідних даних](#outputdata)

<a name="name"></a>
<h2>Позначення та найменування програмного модуля</h2>

Програмний модуль має позначення **`"service-sa-en"`**.

Повне найменування програмного модуля – **"Програмний модуль виявлення емоційного забарвлення текстів інформаційних повідомлень поданих англійською мовою"**.

<a name="software"></a>
<h2>Програмне забезпечення, необхідне для функціонування програмного модуля</h2>

Для функціонування програмного модуля **`service-sa-en`**, написаного мовою програмування `Python`, необхідне наступне програмне забезпечення:

- `Docker` [v20.10](https://docs.docker.com/engine/release-notes/#version-2010)
- `Kubernetes` [v1.22.4](https://github.com/kubernetes/kubernetes/releases/tag/v1.22.4)

- `python` [v3.6.0](https://www.python.org/downloads/release/python-360/) or newer

```sh
python --version Python 3.6.0
```
програмні модулі:
- `molfar-node` [@molfar/molfar-node](https://github.com/wdc-molfar/molfar-node)
- `MSAPI` [@molfar/msapi-schemas](https://github.com/wdc-molfar/msapi-schemas)

пакети:
- `fastText` [v0.9.2](https://github.com/facebookresearch/fastText)
- `json` [v1.6.1](https://github.com/facebookresearch/fastText)
- `axios` [v0.27.2](https://www.npmjs.com/package/axios/v/0.27.2)
- `execa` [v4.1.0](https://www.npmjs.com/package/execa/v/4.1.0)
- `fs-extra` [v10.1.0](https://www.npmjs.com/package/fs-extra/v/10.1.0)


Для функціонування програмного модуля **`service-sa-en`** також необхідна квантована модель [en.ftz](https://drive.google.com/u/0/uc?id=12MLctdlgzqw_tMYizZOzzY1Ja8AYK2AH&export=download&confirm=t) — модель для виявлення емоційного забарвлення текстів інформаційних повідомлень, що подані англійською мовою.

<a name="function"></a>
<h2>Функціональне призначення</h2>

Програмний модуль **`service-sa-en`** призначений для виявлення емоційного забарвлення текстів інформаційних повідомлень, що подані англійською мовою, за допомогою навченої засобами [fastText](https://github.com/facebookresearch/fastText) англійської моделі сентимент-аналізу.

<a name="structure"></a>
<h2>Опис логічної структури</h2>

Програмний модуль **`service-sa-en`** складається з:
- `main.py` - головного скрипта, який виконує наступне:
	- здійснює завантаження квантованої моделі [en.ftz](https://drive.google.com/u/0/uc?id=12MLctdlgzqw_tMYizZOzzY1Ja8AYK2AH&export=download&confirm=t) сентимент-аналізу текстів інформаційних повідомлень поданих українською мовою за допомогою функції `load_model()` бібліотеки [fastText](https://github.com/facebookresearch/fastText)
	- очікує вхідний потік у форматі `JSON`, звідки зчитує та відбирає значення пари з ключем `text` - текстом інформаційного повідомлення
	- здійснює сентимент-аналіз вхідного текстового повідомлення за допомогою функції `predict()` бібліотеки [fastText](https://github.com/facebookresearch/fastText) з використанням завантаженої моделі [en.ftz](https://drive.google.com/u/0/uc?id=12MLctdlgzqw_tMYizZOzzY1Ja8AYK2AH&export=download&confirm=t) та визначає імовірність приналежності до певного класу `__label__pos` та `__label__neg`. Результуюче передбачення емоційного забарвлення тексту містить одну із міток: `positive` - для позитивного емоційного забарвлення, `negative` - для негативного емоційного забарвлення та `unrecognised` - у випадку, коли імовірність приналежності до певного класу нижча за встановлений за замовчуванням поріг `0.9`
	- здійснює формування й вивід у вихідний потік результуючого `JSON`.
	Для цього програмного модуля в результаті встановлення для класифікатора порогу імовірності приналежності до певного класу більше `0.7` – мітки отримують близько `88%` інформаційних повідомлень, для порогового значення `0.8` цей показник становить близько `82%`, а для порогу `0.9` – `72%`.

<a name="hardware"></a>
<h2>Використовувані технічні засоби</h2>

Програмний модуль **`service-sa-en`** експлуатується на сервері (або у хмарі серверів) під управлінням операційної системи типу `Linux` (64-х разрядна). В основі управління всіх сервісів є система оркестрації `Kubernetes`, де всі контейнери працюють з використанням `Docker`.
Також **`service-sa-en`** працює під управлінням програмного модуля контейнера 
мікросервісів [@molfar/molfar-node](https://github.com/wdc-molfar/molfar-node).
Налаштування здійснюється за допомогою програмного модуля для оброблення та валідації специфікацій API мікросервісів та робочих процесів [MSAPI](https://github.com/wdc-molfar/msapi-schemas).
Приклад конфігурації програмного модуля можна знайти за [посиланням](https://github.com/wdc-molfar/workflow-example/tree/main/doc).

<a name="run"></a>
<h2>Виклик та завантаження</h2>

Для запуску програмного модуля **`service-sa-en`** необхідно:
1. Клонувати репозиторій:
```sh
git clone https://github.com/wdc-molfar/service-sa-en.git
```
2. Перейти в директорію склонованого репозиторія та проінсталювати залежності:
```sh
cd /service-sa-en
npm install
```
Успішний результат виконання повинен завершуватися наступним рядком:
```sh
Molfar Sentiment Analyzer(en) service successfully deployed
```
3. Для виклуку головного скрипта `main.py`, що виконує сентимент-аналіз текстів інформаційних повідомлень поданих англійською мовою, необхідно скористатися наступною командою, вказавши в якості додаткових параметрів повний шлях до квантованої моделі `model.ftz`:
```sh
python ./src/python/main.py ./model.ftz
```
4. В якості вхідних даних необхідно передати рядок у форматі `JSON`, що має наступний вигляд:
```JSON
{"text": "<message text>"}
```
де значення `<message text>` пари з ключем `text` - це текст текст інформаційного повідомлення, що поданий англійською мовою.

Результат обробки вхідного `JSON` має наступний вигляд:
```JSON
{"emotion": "<emotion label>", "classes": {"__label__neg": "<value>", "__label__pos": "<value>"}}
```
де значення `<emotion label>` пари з ключем `emotion` - це передбачення емоційного забарвлення тексту: `positive`, `negative` чи `unrecognised`; значення пари з ключем `classes` - набір, ключами якого є класи `__label__pos` та `__label__neg`, а їх відповідні значення `<value>` - ймовірності приналежності до цих класів.

У випадку виникнення виняткових ситуацій під час роботи програмного модуля формується `JSON`, що має наступний вигляд:
```JSON
{"error": "Опис виняткової ситуації..."}
``` 

<a name="inputdata"></a>
<h2>Приклад вхідних даних</h2>

Формат вхідних даних - `JSON`, що зчитується із вхідного потоку, може мати наступний вигляд:
```JSON
{"text": "A positive english text of messages."}
```

<a name="outputdata"></a>
<h2>Приклад вихідних даних</h2>

Формат результуючих даних, що записуються у вихідний потік - `JSON`, може мати наступний вигляд:
```JSON
{"emotion": "positive", "classes": {"__label__pos": 0.9852401614189148, "__label__neg": 0.014779872260987759}}
```

## Copyright
Copyright © 2022 [WDC-MOLFAR](https://github.com/wdc-molfar)

