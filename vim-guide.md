* Helpful Vim Commands/Methods for Quick Reference

** Macros
- Pressing (`q` + `a`) + (<Commands to be performed>) + (<ESC> + `q`), allows for <Commands to be performed> to be registered and called again when pressing `@a`.
    - (`q` + `a`)
        - Begins recording into register @a
    - (<Commands to be performed>)
        - What is being recorded
    - (<ESC> + `q`)
        - End recording


** Navigation in Insert Mode
- <CTRL-o> while in Insert Mode
    - Gets you out of insert mode and let's you perform 1 task/command in Normal Mode, then automatically/immediately switches back to Insert Mode
- <CTRL-o> + h,j,k,l
    - single movement
    - Can be used with numeric movement
- <CTRL-w>
    - Delete work to the left of the cursor
- <CTRL-o> + D
    - Delete everything to the right of the cursor
- <CTRL-u>
    - Delete everything to the left of the cursor
- <CTRL-j>
    - Insert newline (This is amazing)
- <CTRL-t> && <CTRL-d>
    - Indent && unindent current line (another amazing find)


** List of Numbers
- Using Visual Block Mode, highlight the numbers and type `g + <CTRL-a>`
- You can also just increment a single number by pressing <CTRL-a>
<div class="test">[0]</div>
<div class="test">[0]</div>
<div class="test">[0]</div>
<div class="test">[0]</div>
<div class="test">[0]</div>
<div class="test">[0]</div>
<div class="test">[0]</div>
<div class="test">[0]</div>
<div class="test">[0]</div>

** Spelling
   - You can use `z=` for a list of spelling suggestions

** CTRL-O and CTRL-I in Normal Mode
   - Ctrl-O "jumps" the cursor backwards through their "jump list", or the list of places where the cursor has been. Ctrl-I "jumps" the cursor forwards through the "jump list".

** Replace string in file
- `:%s/to-replace-value/with-replacement-value/g`
    - `:%s` is the substitute command, acting on the entire file all at once. Think, replace all occurrences of.
    - `:s` would work on the first occurrence of the word, then move on to the next, and so on. Single replacement at a time.
    - `/to-replace-value` is the value string you want to find and replace.
    - `/with-replacement-value` is the value you're replacing with, since you don't want the `to-replace-value` anymore.
    - `/g` is an optional argument that is most likely wanted, but not always. It replaces all occurrences of the value multiple times per line. Otherwise, without the `/g`, the substitute command would simply replace the first occurrence on every line, instead of every occurrence on every line.
