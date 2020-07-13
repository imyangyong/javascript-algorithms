# 正则表达式匹配

字符串 `s` 和正则模式 `p`，实现支持 `.` 和 `*` 的正则表达式匹配。

- `.`：匹配任何的单字符
- `*`：匹配 0 个或多个元素。

匹配应该覆盖整个输入字符（而不是部分）。

**注意！**

- `s` 可以是空的，并且只包含小写字母 `a-z`。

- `p` 可以是空的，同样只包含小写字母 `a-z`，以及 `.` 或 `*`。

## 示例

### **Example #1**

Input:

```javascript
s = 'aa'
p = 'a'
```

Output: `false`

说明：`a` 与整个字符串 `aa` 不匹配。

**Example #2**

Input:

```javascript
s = 'aa'
p = 'a*'
```

Output: `true`

说明：`*` 表示前面的元素 `a` 的 0 个或多个。因此，重复 `a` 一次，它就变成了 `aa`。

**Example #3**

Input:

```javascript
s = 'ab'
p = '.*'
```

Output: `true`

说明：`*` 表示重复 `.` 0 个或多个；`.` 代表任一字符。

**Example #4**

Input:

```javascript
s = 'aab'
p = 'c*a*b'
```

Output: `true`

说明：`c` 可以为 0 个；`a` 可以为两个。

## 代码

```javascript
onst ZERO_OR_MORE_CHARS = '*';
const ANY_CHAR = '.';

/**
 * Dynamic programming approach.
 *
 * @param {string} string
 * @param {string} pattern
 * @return {boolean}
 */
export default function regularExpressionMatching(string, pattern) {
  /*
    * Let's initiate dynamic programming matrix for this string and pattern.
    * We will have pattern characters on top (as columns) and string characters
    * will be placed to the left of the table (as rows).
    *
    * Example:
    *
    *     a * b . b
    *   - - - - - -
    * a - - - - - -
    * a - - - - - -
    * b - - - - - -
    * y - - - - - -
    * b - - - - - -
   */
  const matchMatrix = Array(string.length + 1).fill(null).map(() => {
    return Array(pattern.length + 1).fill(null);
  });

  // Let's fill the top-left cell with true. This would mean that empty
  // string '' matches to empty pattern ''.
  matchMatrix[0][0] = true;

  // Let's fill the first row of the matrix with false. That would mean that
  // empty string can't match any non-empty pattern.
  //
  // Example:
  // string: ''
  // pattern: 'a.z'
  //
  // The one exception here is patterns like a*b* that matches the empty string.
  for (let columnIndex = 1; columnIndex <= pattern.length; columnIndex += 1) {
    const patternIndex = columnIndex - 1;

    if (pattern[patternIndex] === ZERO_OR_MORE_CHARS) {
      matchMatrix[0][columnIndex] = matchMatrix[0][columnIndex - 2];
    } else {
      matchMatrix[0][columnIndex] = false;
    }
  }

  // Let's fill the first column with false. That would mean that empty pattern
  // can't match any non-empty string.
  //
  // Example:
  // string: 'ab'
  // pattern: ''
  for (let rowIndex = 1; rowIndex <= string.length; rowIndex += 1) {
    matchMatrix[rowIndex][0] = false;
  }

  // Not let's go through every letter of the pattern and every letter of
  // the string and compare them one by one.
  for (let rowIndex = 1; rowIndex <= string.length; rowIndex += 1) {
    for (let columnIndex = 1; columnIndex <= pattern.length; columnIndex += 1) {
      // Take into account that fact that matrix contain one extra column and row.
      const stringIndex = rowIndex - 1;
      const patternIndex = columnIndex - 1;

      if (pattern[patternIndex] === ZERO_OR_MORE_CHARS) {
        /*
         * In case if current pattern character is special '*' character we have
         * two options:
         *
         * 1. Since * char allows it previous char to not be presented in a string we
         * need to check if string matches the pattern without '*' char and without the
         * char that goes before '*'. That would mean to go two positions left on the
         * same row.
         *
         * 2. Since * char allows it previous char to be presented in a string many times we
         * need to check if char before * is the same as current string char. If they are the
         * same that would mean that current string matches the current pattern in case if
         * the string WITHOUT current char matches the same pattern. This would mean to go
         * one position up in the same row.
         */
        if (matchMatrix[rowIndex][columnIndex - 2] === true) {
          matchMatrix[rowIndex][columnIndex] = true;
        } else if (
          (
            pattern[patternIndex - 1] === string[stringIndex]
            || pattern[patternIndex - 1] === ANY_CHAR
          )
          && matchMatrix[rowIndex - 1][columnIndex] === true
        ) {
          matchMatrix[rowIndex][columnIndex] = true;
        } else {
          matchMatrix[rowIndex][columnIndex] = false;
        }
      } else if (
        pattern[patternIndex] === string[stringIndex]
        || pattern[patternIndex] === ANY_CHAR
      ) {
        /*
         * In case if current pattern char is the same as current string char
         * or it may be any character (in case if pattern contains '.' char)
         * we need to check if there was a match for the pattern and for the
         * string by WITHOUT current char. This would mean that we may copy
         * left-top diagonal value.
         *
         * Example:
         *
         *   a b
         * a 1 -
         * b - 1
         */
        matchMatrix[rowIndex][columnIndex] = matchMatrix[rowIndex - 1][columnIndex - 1];
      } else {
        /*
         * In case if pattern char and string char are different we may
         * treat this case as "no-match".
         *
         * Example:
         *
         *   a b
         * a - -
         * c - 0
         */
        matchMatrix[rowIndex][columnIndex] = false;
      }
    }
  }

  return matchMatrix[string.length][pattern.length];
}
```

