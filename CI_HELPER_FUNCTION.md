# CodeIgniter Helpers

---

A several helpers of NSY PHP Framework from Codeigniter PHP Framework.

## Set Realpath

Checks to see if the path exists. This function will return a server path without symbolic links or relative directory structures. An optional second argument will cause an error to be triggered if the path cannot be resolved.

```php
$directory = '/etc/passwd';
echo set_realpath($directory);
// returns "/etc/passwd"

$non_existent_directory = '/path/to/nowhere';
echo set_realpath($non_existent_directory, TRUE);
// returns an error, as the path could not be resolved

echo set_realpath($non_existent_directory, FALSE);
// returns "/path/to/nowhere"
```

## Random Element

 Takes an array as input and returns a random element.

```php
$quotes = array(
        "I find that the harder I work, the more luck I seem to have. - Thomas Jefferson",
        "Don't stay in bed, unless you can make money in bed. - George Burns",
        "We didn't lose the game; we just ran out of time. - Vince Lombardi",
        "If everything seems under control, you're not going fast enough. - Mario Andretti",
        "Reality is merely an illusion, albeit a very persistent one. - Albert Einstein",
        "Chance favors the prepared mind - Louis Pasteur"
);

echo random_element($quotes);
```

## Directory Map

Reads the specified directory and builds an array representation of it. Sub-folders contained with the directory will be mapped as well. The Directory Helper file contains functions that assist in working with directories.

```php
directory_map($source_dir, $directory_depth = 0, $hidden = false);
```

Sub-folders contained within the directory will be mapped as well. If you wish to control the recursion depth, you can do so using the second parameter (integer). A depth of 1 will only map the top level directory:

```php
$map = directory_map('./mydirectory/', 1);
```

By default, hidden files will not be included in the returned array. To override this behavior, you may set a third parameter to true (boolean):

```php
$map = directory_map('./mydirectory/', FALSE, TRUE);
```

Each folder name will be an array index, while its contained files will be numerically indexed. Here is an example of a typical array:

```php
Array (
        [libraries] => Array
                (
                        [0] => benchmark.html
                        [1] => config.html
                        ["database/"] => Array
                                (
                                        [0] => query_builder.html
                                        [1] => binds.html
                                        [2] => configuration.html
                                        [3] => connecting.html
                                        [4] => examples.html
                                        [5] => fields.html
                                        [6] => index.html
                                        [7] => queries.html
                                )
                        [2] => email.html
                        [3] => file_uploading.html
                        [4] => image_lib.html
                        [5] => input.html
                        [6] => language.html
                        [7] => loader.html
                        [8] => pagination.html
                        [9] => uri.html
                )
```

## Encode PHP Tags

This is a security function that converts PHP tags to entities.

```php
$string = encode_php_tags($string);
```

## Word Limiter

uncates a string to the number of words specified. Example:

```php
$string = "Here is a nice text string consisting of eleven words.";
$string = word_limiter($string, 4);
// Returns:  Here is a nice
```

## Character Limiter

Truncates a string to the number of characters specified. It maintains the integrity of words so the character count may be slightly more or less than what you specify.

```php
$string = "Here is a nice text string consisting of eleven words.";
$string = character_limiter($string, 20);
// Returns:  Here is a nice text string
```

## ASCII to Entities

Converts ASCII values to character entities, including high ASCII and MS Word characters that can cause problems when used in a web page, so that they can be shown consistently regardless of browser settings or stored reliably in a database. There is some dependence on your server’s supported character sets, so it may not be 100% reliable in all cases, but for the most part it should correctly identify characters outside the normal range (like accented characters).

```php
$string = ascii_to_entities($string);
```

## Entities to ASCII

Converts character entities back to ASCII.

```php
$string = entities_to_ascii($string);
```

## Word Censor

Enables you to censor words within a text string. The first parameter will contain the original string. The second will contain an array of words which you disallow. The third (optional) parameter can contain a replacement value for the words. If not specified they are replaced with pound signs: ####.

```php
$disallowed = array('darn', 'shucks', 'golly', 'phooey');
$string = word_censor($string, $disallowed, 'Beep!');
```

## Highlight Code

Colorizes a string of code (PHP, HTML, etc.). Example:

```php
$string = highlight_code($string);
```

## Highlight Phrase

Will highlight a phrase within a text string. The first parameter will contain the original string, the second will contain the phrase you wish to highlight. The third and fourth parameters will contain the opening/closing HTML tags you would like the phrase wrapped in.

```php
$string = "Here is a nice text string about nothing in particular.";
echo highlight_phrase($string, "nice text", '<span style="color:#990000;">', '</span>');
```

The above code prints:

```html
Here is a <span style="color:#990000;">nice text</span> string about nothing in particular.
```

## Word Wrap

Wraps text at the specified character count while maintaining complete words.

```php
$string = "Here is a simple string of text that will help us demonstrate this function.";
echo word_wrap($string, 25);

// Would produce:
// Here is a simple string
// of text that will help us
// demonstrate this
// function.
```

## Ellipsize String

This function will strip tags from a string, split it at a defined maximum length, and insert an ellipsis.

The first parameter is the string to ellipsize, the second is the number of characters in the final string. The third parameter is where in the string the ellipsis should appear from 0 - 1, left to right. For example. a value of 1 will place the ellipsis at the right of the string, .5 in the middle, and 0 at the left.

An optional forth parameter is the kind of ellipsis. By default, &hellip; will be inserted.

```php
$str = 'this_string_is_entirely_too_long_and_might_break_my_design.jpg';
echo ellipsize($str, 32, .5);
```

Produces:

```text
this_string_is_e&hellip;ak_my_design.jpg
```

## Strip Slashes

Removes any slashes from an array of strings.

```php
$str = array(
        'question'  => 'Is your name O\'reilly?',
        'answer' => 'No, my name is O\'connor.'
);

$str = strip_slashes($str);
```

The above will return the following array:

```php
array(
        'question'  => "Is your name O'reilly?",
        'answer' => "No, my name is O'connor."
);
```

## Strip Quotes

Removes single and double quotes from a string. Example:

```php
$string = "Joe's \"dinner\"";
$string = strip_quotes($string); //results in "Joes dinner"
```

## Quotes to Entities

Converts single and double quotes in a string to the corresponding HTML entities. Example:

```php
$string = "Joe's \"dinner\"";
$string = quotes_to_entities($string); //results in "Joe&#39;s &quot;dinner&quot;"
```

## Reduce Double Slashes

Converts double slashes in a string to a single slash, except those found in URL protocol prefixes (e.g. http://).

```php
$string = "http://example.com//index.php";
echo reduce_double_slashes($string); // results in "http://example.com/index.php"
```

## Reduce Multiples

Reduces multiple instances of a particular character occurring directly after each other. Example:

```php
$string = "Fred, Bill,, Joe, Jimmy";
$string = reduce_multiples($string,","); //results in "Fred, Bill, Joe, Jimmy"
```

If the third parameter is set to TRUE it will remove occurrences of the character at the beginning and the end of the string. Example:

```php
$string = ",Fred, Bill,, Joe, Jimmy,";
$string = reduce_multiples($string, ", ", TRUE); //results in "Fred, Bill, Joe, Jimmy"
```

## Random String

Generates a random string based on the type and length you specify.

The first parameter specifies the type of string, the second parameter specifies the length. The following choices are available:

alpha: A string with lower and uppercase letters only.
alnum: Alpha-numeric string with lower and uppercase characters.
basic: A random number based on mt_rand().
numeric: Numeric string.
nozero: Numeric string with no zeros.
md5: An encrypted random number based on md5() (fixed length of 32).
sha1: An encrypted random number based on sha1() (fixed length of 40).

Usage example:

```php
echo random_string(string $type = 'alnum', int $len = 8)
```

## Increment String

Increments a string by appending a number to it or increasing the number. Useful for creating “copies” or a file or duplicating database content which has unique titles or slugs.

```php
echo increment_string('file', '_'); // "file_1"
echo increment_string('file', '-', 2); // "file-2"
echo increment_string('file_4'); // "file_5"
```

## Alternator

Allows two or more items to be alternated between, when cycling through a loop. Example:

```php
for ($i = 0; $i < 10; $i++)
{
    echo alternator('string one', 'string two');
}
```

You can add as many parameters as you want, and with each iteration of your loop the next item will be returned.

```php
for ($i = 0; $i < 10; $i++)
{
    echo alternator('one', 'two', 'three', 'four', 'five');
}
```

## Prep URL

This function will add http:// in the event that a protocol prefix is missing from a URL.

Pass the URL string to the function like this:

```php
$url = prep_url('example.com');
```

## URL Title

Takes a string as input and creates a human-friendly URL string. This is useful if, for example, you have a blog in which you’d like to use the title of your entries in the URL. Example:

```php
$title = "What's wrong with CSS?";
$url_title = url_title($title);
// Produces: Whats-wrong-with-CSS
The second parameter determines the word delimiter. By default dashes are used. Preferred options are: - (dash) or _ (underscore)
```

Example:

```php
$title = "What's wrong with CSS?";
$url_title = url_title($title, 'underscore');
// Produces: Whats_wrong_with_CSS
```

## XML Convert

Takes a string as input and converts the following reserved XML characters to entities:

* Ampersands: &
* Less than and greater than characters: < >
* Single and double quotes: ‘ “
* Dashes: -

This function ignores ampersands if they are part of existing numbered character entities, e.g. &#123;. Example:

```php
$string = '<p>Here is a paragraph & an entity (&#123;).</p>';
$string = xml_convert($string);
echo $string;
```

outputs:

```php
&lt;p&gt;Here is a paragraph &amp; an entity (&#123;).&lt;/p&gt;
```

## Symbolic Permissions

Takes numeric permissions (such as is returned by fileperms()) and returns standard symbolic notation of file permissions.

```php
echo symbolic_permissions(fileperms('./index.php'));  // -rw-r--r--
```

## Octal Permissions

Takes numeric permissions (such as is returned by fileperms()) and returns a three character octal notation of file permissions.

```php
echo octal_permissions(fileperms('./index.php')); // 644
```
