# Discord Emoji Parser

A Python library providing utilities for parsing and accessing Discord emojis with advanced functionality such as emoji enumeration and dynamic handling.

## Features

- Parse individual or multiple Discord emojis from a string.
- Generate CDN-hosted URLs for emojis (animated or static).
- Validate emoji format.
- Convert parsed emojis into JSON mappings for integration with other tools.
- Dynamically create Enum classes for Discord emojis, enabling easy programmatic access.


## Installation

This project uses Poetry for dependency management. To install, first ensure Poetry is installed, then run:

```sh
poetry install
```

## Usage

### Importing the Library

```py
from discordemojiparser.emoji_parser import EmojiParser
```

### Parsing Emojis

Parse a Single Emoji

```py
emoji_str = "<a:wave:123456789>"
emoji = EmojiParser.parse_single(emoji_str)

print(emoji.name)  # wave
print(emoji.url)   # https://cdn.discordapp.com/emojis/123456789.gif
```

### Parse All Emojis in a String

```py
text = "<a:wave:123456789> <:smile:987654321>"
emojis = EmojiParser.parse_all(text)

for emoji in emojis:
    print(emoji.name, emoji.url)
```

### Validate Emoji Strings

```py
print(EmojiParser.is_emoji("<a:wave:123456789>"))  # True
print(EmojiParser.has_emoji("Hello <a:wave:123456789>!"))  # True
print(EmojiParser.is_emoji("wave:123456789>"))  # False
```

### Generating JSON from Emojis

```py
text = "<a:wave:123456789> <:smile:987654321>"
emoji_json = EmojiParser.get_emojis_json(text)

print(emoji_json)
# Output: {'wave': 'https://cdn.discordapp.com/emojis/123456789.gif',
#          'smile': 'https://cdn.discordapp.com/emojis/987654321.png'}
```

### Creating Emoji Enums

Dynamically Generate an Enum for Emojis


```py
text = "<a:wave:123456789> <:smile:987654321>"
EmojiEnum = EmojiParser.get_emojis_enum(text)

# Access emoji attributes via Enum
print(EmojiEnum.wave.url)  # https://cdn.discordapp.com/emojis/123456789.gif
print(EmojiEnum.smile.name)  # smile

# Iterate through Enum members
for emoji_name, emoji in EmojiEnum.__members__.items():
    print(emoji_name, emoji.url)
```

### Example Application

```py
from discordemojiparser.emoji_parser import EmojiParser

# Input text containing Discord emojis
text = """
<:gamesir:1176772767132168232>
<a:wave:123456789>
<smile:987654321>
"""

# Parse all emojis and create an enum
EmojiEnum = EmojiParser.get_emojis_enum(text)

# Use the enum
print(EmojiEnum.gamesir.url)  # https://cdn.discordapp.com/emojis/1176772767132168232.png
print(EmojiEnum.wave.url)     # https://cdn.discordapp.com/emojis/123456789.gif
```

## Project Structure

```plaintext
discordemojiparser/
├── discordemojiparser/
│   ├── __init__.py
│   ├── emoji_parser.py
│   └── emoji_enum.py
├── pyproject.toml
└── README.md
└── LICENSE
```

- discordemojiparser/emoji_parser.py: Core logic for parsing and handling emojis.
- discordemojiparser/emoji_enum.py: Custom Enum implementation for managing emojis programmatically.
- pyproject.toml: Poetry configuration.


## Author

**Dylan Magar** ("DJ Stomp")
- GitHub: [@DJStompZone](https://github.com/djstompzone)

## License

MIT License (see LICENSE file)
