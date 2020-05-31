# Regular Expressions

## Documentation

- [Regular-Expressions](https://www.regular-expressions.info)
  - [Lookahead and Lookbehind Zero-Length Assertions](http://www.regular-expressions.info/lookaround.html)
- [Regex 101](https://regex101.com/)

## Examples

**NB:**
Although there are at least two examples that parse HTML/XML-structured text with regular expressions,
in general one should analyse HTML with a DOM-based parser and XML with an XML parser instead.

- **Non-Greedy Matching** with quantifier `?`

  Expression   | Input              | Result
  -------------|--------------------|-----------------------
  `4{2,4}`     | `444444`           | `[4444][44]`
  `4{2,4}?`    | `444444`           | `[44][44][44]`
  `<p>.*</p>`  | `<p>a</p><p>a</p>` | `[<p>a</p><p>a</p>]`
  `<p>.*?</p>` | `<p>a</p><p>a</p>` | `[<p>a</p>][<p>a</p>]`

- Don't repeat yourself

  - Use `https?://.*` instead of the alternation `http|https`

  - Reuse capture groups with `\n`, e.g. `(cat|dog)\s+\1`

- **Non-Capture Group** `(?:Hello)` might match the given text
  but neither creates a variable nor registers the capture group `\1`

- Lookaround

  - **Positive Lookahead**:
    `cool(?=\ cat)` findet `cool` gefolgt von ` cat`.
    Letzteres wird nicht gespeichert

  - **Negative Lookahead**:
    `cool(?!\ cat)` findet `cool`, welches nicht von ` cat` gefolgt wird.
    Letzteres wird nicht gespeichert

  - **Positive Look Behind**
    `(?<=cool\ )cat` findet `cat`, welche nach `cool ` stehen

  - **Negative Look Behind**
    `(?<!cool\ )cat` findet `cat`, welche nicht nach `cool ` stehen

- Anchors for start `^` and end `$`

- (Inline) **Modifiers**

  - **Multi-Line Mode**:
    `(?m)^\w+` findet erstes Wort in jeder Zeile
    und `(?m)\w$+` findet letztes Wort in jeder Zeile

  - **Case Insensitive Modifier** `(?i)`, z.B. `(?i)[a-z]` findet auch große Buchstaben

  - **Single Line Modifier** lets `.` match newline characters,
    e.g. `(?s).+` matches everything even across line breaks

  - **Extended Modifier** (Free Space Mode) allows to write regular expressions over multiple lines and enables comments with `#`.
    The drawback of this mode is that whitespaces have to be escaped as they are ignored otherwise

    ```regexp
    (?x)
    \w+ # Matches all words and …
        # non-escaped whitespaces are ignored.
    ```

  - Modifier can be combined: `(?xims)`

  - Modifier can be disabled, e.g. `(?-i)` disabled the case insensitive modifier

- Word boundary with `\b`

  Expression | Input              | Result
  -----------|--------------------|----------
  `foo\b`    | `foo` or `foo bar` | `[foo]`
  `foo\b`    | `foobar`           | No result

- `\S` matches any non-whitespace character (equal to `[^\r\n\t\f\v ]`)

- Get the first and last word of every line

  ```regexp
  (?m) ^\S+|\S+$
  ```

- Extract the contents of regular table cells with the assumption,
  that cells contain no other HTML nodes.

  ```regexp
  (?x)
  (?<=<td>) # Match text following <td>.
  [^<>]+    # The text does not contain < and >.
  ```
