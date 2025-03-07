# Key values

A key value defines what a key on the keyboard does when pressed or swiped.

Key values appear in the following places:

- In custom layouts, they are the value of: the `c` attribute, the compass-point attributes `nw` ... `se`, and the old-style `key0` ... `key8` attributes.
- Internally, they are used in the definition of the "Add keys to the keyboard" setting.

Key values can be any of the following:

- The name of a special key. A complete list of valid special keys appears later in this document.

- Any other sequence of characters not containing `:` results in a key that sends those characters.

- `keyevent:keycode` An Android keycode: one of the numbers listed with symbol `KEYCODE_...` in the Android [KeyEvent](https://developer.android.com/reference/android/view/KeyEvent#summary) document.

- A macro, `key_def1,key_def2,...`. Each `key_def` is any of the above definitions. This results in a key that behaves as if the sequence of `key_def` had been pressed in order.

### Legends

Any of the above forms can be preceded by `legend:`. The string excluding `:` defines the visible legend on the keyboard. A legend cannot contain `:`, which is interpreted as the end of the legend, nor `,`, which is interpreted as a macro.

### Escape codes

**When defining a key value**, several characters have special effects. If you want a character not to have its usual effect but to be taken literally, you should "escape" it in the usual way for XML:

To get this character... | ...you can type
:---- | :------
A literal newline character, which is different from `enter` and `action` in certain apps. | `\n`
A literal tab character, which is different from `tab` in certain apps. | `\t`
`\` | `\\`
`&` | `&amp;`
`<` | `&lt;`
`>` | `&gt;`
`"` | `&quot;`

The characters `?`, `#`, and `@` do not need to be escaped when writing custom layouts. Internally, they can be escaped by prepending backslash (by typing `\?`, `\#`, and `\@`).

The characters `,` and `:` must be escaped in a key value, using single quotes.

**When defining a legend**, there are no escape codes.

### Examples
These examples use the `c=` attribute to define the effect of a touch, but the same syntax can also be used for swipes.

- `<key c="CA:ctrl,a,ctrl,c" />`<br />A key with legend CA that sends the sequence `ctrl+a`, `ctrl+c`
- `<key c="Cd:ctrl,backspace" />`<br />A key with legend Cd that sends the shortcut `ctrl+backspace`
- `<key c="⏯:keyevent:85" />`<br />A play/pause key (which has no effect in most apps)
- `<key c="my@:'my.email@domain.com'" />`<br />A key that sends an arbitrary string
- `<key c="http:home,'https://'" />`<br />The single-quotes here are required because the string contains `:`.

## Modifiers
System modifiers are sent to the app, which can take app-specific action.

Value       | Meaning
:---------- | :------
`shift`     | System modifier.
`ctrl`      | System modifier.
`alt`       | System modifier.
`meta`      | System modifier. Equivalent to the Windows key.

The other modifiers take effect only within the keyboard.

Value       | Meaning
:---------- | :------
`fn`        | Activates Fn mode, which assigns letters and symbols to special characters. Example: `fn` `!` = `¡`
`compose`   | Compose key. Enables composing characters using Linux-like shortcuts. Example: `Compose` `A` `'` types `Á` (A with acute accent).
`capslock`  | Activates and locks Shift.

## App function keys
These keys are sent to apps, which are free to ignore them. The keyboard does not perform editing in response to these keys.

`esc`, `enter`,
`up`, `right`,
`down`, `left`,
`page_up`, `page_down`,
`home`, `end`,
`backspace`, `delete`,
`insert`, `scroll_lock`,
`f1`-`f12`,
`tab`, `copy`,
`paste`, `cut`,
`selectAll`, `pasteAsPlainText`,
`undo`, `redo`

## Keyboard editing actions
In contrast, these keys perform editing on the text without sending anything to the app.
Value                 | Meaning
:-------------------- | :------
`cursor_left`         | Moves the cursor to the left with the slider gesture.
`cursor_right`        | Moves the cursor to the right with the slider gesture.
`cursor_up`           | Moves the cursor up with the slider gesture. Warning: this might make the cursor leave the text box.
`cursor_down`         | Moves the cursor down with the slider gesture. Warning: this might make the cursor leave the text box.
`delete_word`         | Delete the word to the left of the cursor.
`forward_delete_word` | Delete the word to the right of the cursor.

## Whitespace
Value   | Meaning
:------ | :------
`space` | Space bar.
`nbsp`  | Non-breaking space.
`nnbsp` | Narrow non-breaking space.
`zwj`   | Zero-width joiner.
`zwnj`  | Zero-width non-joiner.

## Other modifiers and diacritics
Value                | Meaning
:------------------- | :------
`accent_aigu`        | Acute accent. `á`
`accent_caron`       | Háček. `č`
`accent_cedille`     | Cedilla. `ç`
`accent_circonflexe` | Circumflex. `â`
`accent_grave`       | Grave accent. `à`
`accent_macron`      | Macron. `ā`
`accent_ring`        | Ring accent. `å`
`accent_tilde`       | Tilde. `ã`
`accent_trema`       | Dieresis/umlaut. `ä`
`accent_ogonek`      | Ogonek. `ą`
`accent_dot_above`   | Dot accent. `ż` If applied to the lowercase `i`, removes the dot instead for Turkish. `ı`
`accent_double_aigu` | Double acute accent. `ő`
`accent_slash`       | Slash through. `ø`
`accent_arrow_right` | Right arrow above, used to denote a vector. `a⃗`
`accent_breve`       | Breve. `ă`
`accent_bar`         | Bar/strikethrough. `ɨ`
`accent_dot_below`   | Dot below. `ạ`
`accent_horn`        | Horn accent. `ơ`
`accent_hook_above`  | Hook accent. `ả`
`accent_double_grave`  | Double grave accent. `ȁ`
`superscript`        | Superscript. `ᵃ`
`subscript`          | Subscript. `ₐ`
`ordinal`            | Turns `a` and `o` into `ª` and `º`.
`arrows`             | Turns `1`-`4` and `6`-`9` into arrows.
`box`                | Turns `1`-`9`, `0`, and `.` into single-line, thin box-drawing characters.

## Bidirectional
Value   | Meaning
:------ | :------
`lrm`   | Left-to-right mark.
`rlm`   | Right-to-left mark.
`b(`, `b)`, `b[`, `b]`, `b{`, `b}`, `blt`, `bgt` | Sends the bracket characters, but with mirrored key legends for right-to-left languages. (`blt` and `bgt` print `<` and `>` respectively.)

## Hebrew
Keys ending in `_placeholder` are normally hidden unless the Fn key is pressed.

`qamats`, `patah`,
`sheva`, `dagesh`,
`hiriq`, `segol`,
`tsere`, `holam`,
`qubuts`, `hataf_patah`,
`hataf_qamats`, `hataf_segol`,
`shindot`, `shindot_placeholder`,
`sindot`, `sindot_placeholder`,
`geresh`, `gershayim`,
`maqaf`, `rafe`,
`ole`, `ole_placeholder`,
`meteg`, `meteg_placeholder`

## Keyboard behavior keys
Value                  | Meaning
:--------------------- | :------
`config`               | Gear icon; opens Unexpected Keyboard settings.
`switch_text`          | Switch to the text layer (main layer).
`switch_numeric`       | Switch to the numeric layer.
`switch_emoji`         | Switch to the emoji layer.
`switch_back_emoji`    | Switch to the text layer from the emoji layer.
`switch_forward`       | Change the keyboard layout, as long as Unexpected Keyboard has multiple keyboard layouts enabled in the settings.
`switch_backward`      | Change the keyboard layout to the previous one in the list.
`switch_greekmath`     | Switch to the Greek & Math Symbols layer.
`switch_clipboard`     | Switch to the clipboard pane.
`change_method`        | Open the input method picker dialog.
`change_method_prev`   | Switch to the previously used input method.
`action`               | Performs a special context-sensitive operation related to the Enter key. For example, in the Twitter (X) app, `enter` adds a new line, while `action` posts.
`voice_typing`         | Begin voice typing.
`voice_typing_chooser` | Shows a menu where you can choose which voice typing provider to use, then begins voice typing when you make a selection.
`shareText`            | Emit a share Intent for the selected text. **Oddity:** This is in CamelCase.

## Unused
These keys are known to do nothing.

`replaceText`, `textAssist`,
`autofill`, `removed`

## Placeholders
These keys are normally hidden unless the Fn modifier is activated.

`f11_placeholder` | `f12_placeholder`
