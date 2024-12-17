Конечно! Вот пример `README.md` для вашей библиотеки в формате Markdown.

---

# TGWindow

**TGWindow** — это библиотека для удобного создания и управления окнами (сообщениями) в **Telegram** с использованием **Aiogram**. Она предоставляет базовый интерфейс для работы с текстом, кнопками и отправкой сообщений.

---

## Возможности библиотеки
- Удобное создание сообщений с текстом и кнопками.
- Поддержка **Inline** и **Reply** клавиатур.
- Гибкая настройка размеров клавиатур.
- Простое взаимодействие с `Message` и `CallbackQuery`.

---

## Установка

Установите библиотеку через `pip` (если она доступна) или вручную.

```bash
pip install tgwindow
```

---

## Пример использования

### 1. **Создание окна и отправка сообщения**

```python
from datetime import datetime
import asyncio
from aiogram.types import Message, Chat
from src.sender.sender import Send
from src.windows.base_window import BaseWindow


# Создание окна
class HelloWindow(BaseWindow):
    def hello(self):
        self.text = "Hello, guys!"
        self.button("Say Hello")
        return self  # Возвращаем экземпляр для удобства


# Создание объекта Send
send = Send(event=message)


# Отправка сообщения
async def main():
    await send(HelloWindow().hello())


if __name__ == "__main__":
    asyncio.run(main())
```

---

### 2. **Добавление кнопок и размера клавиатуры**

```python
class CustomWindow(BaseWindow):
    def setup(self):
        self.text = "Choose an option:"
        self.button(("Option 1", "data_1"))  # Inline-кнопки
        self.button(("Option 2", "data_2"))
        self.size(2)  # Кнопки располагаются по 2 в ряд
        return self

# Отправка кастомного окна
async def main():
    await send(CustomWindow().setup())

if __name__ == "__main__":
    asyncio.run(main())
```

---

### 3. **Использование Reply-клавиатуры**

```python
from src.keyboard.base_keyboards import Reply


class MyKeyboard(Reply):
    block = "Block user"
    away_button = "Away button"


class ReplyWindow(BaseWindow):
    def setup(self):
        self.text = "Choose a command:"
        self.button("/start")
        self.button("/help")
        self.button("/settings")
        return self


class NewWindow(BaseWindow):
    def blocker(self):
        self.text = "Block user?"
        self.button(MyKeyboard())
        return self


async def main():
    await send(ReplyWindow().setup())


if __name__ == "__main__":
    asyncio.run(main())
```

---

## Основные классы

### 1. **`BaseWindow`**
`BaseWindow` — это базовый класс для создания окон. Он предоставляет методы для настройки текста и кнопок.

- **`self.text`** — текст сообщения.
- **`self.button(*args, keyboard=None)`** — добавление кнопок.
- **`self.size(int)`** — настройка количества кнопок в ряду.
- **`self._build()`** — возвращает текст и разметку для отправки.

---

### 2. **`Send`**
`Send` — класс для отправки сообщений.

**Инициализация:**
```python
send = Send(event: Message | CallbackQuery)
```

**Использование:**
```python
await send(window: BaseWindow | tuple[str, keyboard] | str, photo: str | None)
```

---

## Требования
- **Python 3.8+**
- **Aiogram 3.0+**

---

## Лицензия
Этот проект распространяется под лицензией **MIT**. Используйте свободно!

---

## Обратная связь
Если у вас есть вопросы или предложения, создавайте **Issue** или отправляйте PR.

---

Такой `README.md` можно сразу использовать в вашем репозитории.