### Use | or > sign

Use |

Preserves line returns within string:

```yaml
include_newlines: |
         Example Company
         123 Main Street
         Atlanta, GA 30303
```
Use >

Converts line returns to spaces. Removes leading white spaces in lines

Use to break long strings at space characters
Spanning multiple lines promotes better readability
```yaml
fold_newlines: >
          This is
          a very long,
          long, long, long
          sentence.
```
There are two ways to write multiline strings. One method uses the vertical bar character to denote that line returns within the string must be preserved, as shown in the first example here.

The second method uses the greater-than character to indicate that line returns in the strong are to be converted to spaces and that leading white spaces in the lines are to be removed, as shown in the second example here. This method is often used to break long strings at space characters so that they can span multiple lines for better readability.