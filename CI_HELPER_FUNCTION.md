# CI helpers
A several CI helpers of NSY PHP Framework from Codeigniter.

#### Set Realpath

```
set_realpath($path, $check_existance = false)
```

#### Random Element - Takes an array as input and returns a random element

```
random_element($array)
```

#### directory_map
Reads the specified directory and builds an array representation of it. Sub-folders contained with the directory will be mapped as well.

```
directory_map($source_dir, $directory_depth = 0, $hidden = false)
```

#### Convert PHP tags to entities

```
encode_php_tags(string $str)
```

#### Word Limiter
Limits a string to X number of words.

```
word_limiter(string $str, int $limit = 100, string $end_char = '&#8230;')
```

#### Character Limiter
Limits the string based on the character count.  Preserves complete words
so the character count may not be exactly as specified.

```
character_limiter(string $str, int $n = 500, string $end_char = '&#8230;')
```

#### High ASCII to Entities
Converts high ASCII text and MS Word special characters to character entities.

```
ascii_to_entities(string $str)
```

#### Entities to ASCII
Converts character entities back to ASCII.

```
entities_to_ascii(string $str, bool $all = true)
```

#### Word Censoring Function
Supply a string and an array of disallowed words and any matched words will be converted to #### or to the replacement word you've submitted.

```
word_censor(string $str, array $censored, string $replacement = '')
```

#### Code Highlighter
Colorizes code strings.

```
highlight_code(string $str)
```

#### Phrase Highlighter
Highlights a phrase within a text string.

```
highlight_phrase(string $str, string $phrase, string $tag_open = '<mark>', string $tag_close = '</mark>')
```

#### Word Wrap
Wraps text at the specified character. Maintains the integrity of words.
Anything placed between {unwrap}{/unwrap} will not be word wrapped, nor will URLs.

```
word_wrap(string $str, int $charlim = 76)
```

#### Ellipsize String
This function will strip tags from a string, split it at its max_length and ellipsize.

```
ellipsize(string $str, int $max_length, $position = 1, string $ellipsis = '&hellip;')
```

#### Strip Slashes
Removes slashes contained in a string or in an array.

```
strip_slashes($str)
```

#### Strip Quotes
Removes single and double quotes from a string.

```
strip_quotes(string $str)
```

#### Quotes to Entities
Converts single and double quotes to entities.

```
quotes_to_entities(string $str)
```

#### Reduce Double Slashes
Converts double slashes in a string to a single slash, except those found in http://

```
reduce_double_slashes(string $str)
```

#### Reduce Multiples
Reduces multiple instances of a particular character.

```
reduce_multiples(string $str, string $character = ',', bool $trim = false)
```

#### Create a Random String
Useful for generating passwords or hashes.

```
random_string(string $type = 'alnum', int $len = 8)
```

#### Increment String
Add `_1` to a string or increment the ending number to allow `_2`,` _3`, etc

```
increment_string(string $str, string $separator = '_', int $first = 1)
```

#### Alternator
Allows strings to be alternated. See docs...

```
alternator()
```

#### Excerpt
Allows to extract a piece of text surrounding a word or phrase.

```
excerpt(string $text, string $phrase = null, int $radius = 100, string $ellipsis = '...')
```

#### Prep URL - Simply adds the http:// part if no scheme is included.
Formerly used URI, but that does not play nicely with URIs missing the scheme.

```
prep_url(string $str = '')
```

#### Create URL Title
Takes a "title" string as input and creates a human-friendly URL string with a "separator" string as the word separator.

```
url_title(string $str, string $separator = '-', bool $lowercase = false)
```

#### Convert Reserved XML characters to Entities

```
xml_convert($str, $protect_all = false)
```

#### Symbolic Permissions

```
symbolic_permissions($perms)
```

#### Octal Permissions
Takes a numeric value representing a file's permissions and returns a three character string representing the file's octal permissions.

```
octal_permissions($perms)
```