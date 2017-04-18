A regular expression describes a pattern in a sequence of characters. A regular expression is a string that describes a character sequence.

We can then use pattern to

*   validate the sequence of characters
*   search through the sequence of characters
*   replace the characters matching the pattern

## Package

The `java.util.regex` package supports regular expression processing.

The general description in a regular expression called a pattern, can be used to find matches in other character sequences.

Regular expressions can specify wildcard characters, sets of characters, and various quantifiers.

We can specify a regular expression that represents a general form that can match several different specific character sequences.

There are two classes that support regular expression processing: `Pattern` and `Matcher`.

These classes work together: use `Pattern` to define a regular expression. and match the pattern against another sequence using `Matcher`.

Metacharacters are characters with special meanings in Java regular expression.

The metacharacters supported by the regular expressions in Java are as follows:

<pre>( ) [ ] { { \ ^ $ | ? * + . < > - = !
</pre>

## Character Classes

The metacharacters `[` and `]` specifies a character class inside a regular expression.

A character class is a set of characters. The regular expression engine will attempt to match one character from the set.

The character class "[ABC]" will match characters A, B, or C. For example, the strings "woman" or "women" will match the regular expression "wom[ae]n".

We can specify a range of characters using a character class.

The range is expressed using a hyphen `-` character.

For example, `[A-Z]` represents any uppercase English letters; "[0-9]" represents any digit between 0 and 9.

`^` means not.

For example, `[^ABC]` means any character except A, B, and C.

The character class `[^A-Z]` represents any character except uppercase letters.

If `^` appears in a character class except in the beginning, it just matches a `^` character.

For example, "[ABC^]" will match A, B, C, or ^.

You can also include two or more ranges in one character class. For example, `[a-zA-Z]` matches any character a through z and A through Z.

`[a-zA-Z0-9]` matches any character a through z (uppercase and lowercase), and any digit 0 through 9.

The following table has examples of Character Classes

Characters a through zCharacter ClassesMeaning[abc]Character a, b, or c[^xyz]A character except x, y, and z[a-z]  
[a-cx-z]Characters a through c, or x through z, which would include a, b, c, x, y, or z.[0-9&&[4-8]]Intersection of two ranges (4, 5, 6, 7, or 8)[a-z&&[^aeiou]]All lowercase letters minus vowels

## Predefined Character Classes

The following table lists some frequently used predefined character classes.

Predefined   
Character   
Classes  
Meaning.Any character\dA digit. Same as [0-9]\DA non-digit. Same as [^0-9]\sA whitespace character. Same as [ \t\n\x0B\f\r] which include. 

*   a space
*   a tab
*   a new line
*   a vertical tab
*   a form feed
*   a carriage return characters

\SA non-whitespace character. Same as [^\s]\wA word character. Same as [a-zA-Z_0-9].\WA non-word character. Same as [^\w]

## Example

The following code uses `\d` to match all digits.

`\\d` is used in the string to escape the `\`.

<pre>import java.util.regex.Matcher;
import java.util.regex.Pattern;
/*from  ww  w .ja  v a 2  s  .  co  m*/
public class Main {
  public static void main(String args[]) {
    Pattern p = Pattern.compile("Java \\d");

    String candidate = "Java 4";
    Matcher m = p.matcher(candidate);

    if (m != null)
      System.out.println(m.find());
  }
}
</pre>

The code above generates the following result.

![](http://www.java2s.com/Tutorials/JavaImage/myResult/E/EXAMPLE__E79CB79318B529DD69B9.PNG)

## Example 2

The following code `\w+` to match any word.

Double slash is used to escape `\`.

<pre>import java.util.regex.Matcher;
import java.util.regex.Pattern;
//  w w  w. java2s .  c  om
public class Main {
  public static void main(String args[]) {
    String regex = "\\w+";
    Pattern pattern = Pattern.compile(regex);

    String candidate = "asdf Java2s.com";

    Matcher matcher = pattern.matcher(candidate);

    if (matcher.find()) {
      System.out.println("GROUP 0:" + matcher.group(0));
    }

  }
}
</pre>

The code above generates the following result.

The package `java.util.regex` contains three classes to support the full version of regular expressions.

*   Pattern
*   Matcher
*   PatternSyntaxException

A `Pattern` holds the compiled form of a regular expression.

A `Matcher` associates the string to be matched with a Pattern and it performs the actual match.

A `PatternSyntaxException` represents an error in a malformed regular expression.

## Compiling Regular Expressions

A Pattern which has no public constructor is immutable and can be shared.

`Pattern` class contains a static compile() method, which returns a `Pattern` object.

The `compile()` method is overloaded.

<pre>static Pattern  compile(String regex)
static Pattern compile(String regex, int flags)
</pre>

The following code compiles a regular expression into a Pattern object:

<pre>import java.util.regex.Pattern;

public class Main {
  public static void main(String[] args) {
    // Prepare a regular expression
    String regex = "[a-z]@.";

    // Compile the regular expression into a Pattern object
    Pattern p = Pattern.compile(regex);
  }
}

</pre>

The second version of the compile() method sets flags that modify the way the pattern is matched.

The flags parameter is a bit mask and defines as int constants in the Pattern class.

FlagDescriptionPattern.CANON_EQEnables canonical equivalence.Pattern.CASE_INSENSITIVEEnables case-insensitive matching.Pattern.COMMENTSPermits whitespace and comments in pattern.  
ignore whitespace and embedded comments starting with # until the end of a line.Pattern.DOTALLEnables dotall mode.   
By default, `.` does not match line terminators. When this flag is set, `.` matches a line terminator.Pattern.LITERALEnables literal parsing of the pattern. This flag makes metacharacters and escape sequences as normal character.Pattern.MULTILINEEnables multiline mode. By default, `^` and `$` match the beginning and the end of the input sequence. This flag makes pattern only match line by line or the end of the input sequence.Pattern.UNICODE_CASEEnables Unicode-aware case. Together with the CASE_INSENSITIVE flag, the case-insensitive matching can be performed according to the Unicode Standard.Pattern.UNICODE_ CHARACTER_CLASSEnables the Unicode version of predefined character classes and POSIX character classes. When this flag is set, the Predefined character classes and POSIX character classes are in conformance with Unicode Technical Standard.Pattern.UNIX_LINESEnables Unix lines mode. When this flag is set, only the `\n` character is recognized as a line terminator.

## Example

The following code compiles a regular expression setting the CASE_INSENSTIVE and DOTALL flags.

<pre>import java.util.regex.Pattern;

public class Main {
  public static void main(String[] args) {
    String regex   = "[a-z]@.";
    Pattern p  = Pattern.compile(regex,  Pattern.CASE_INSENSITIVE|Pattern.DOTALL);
  }
}

</pre>

## Example 2

<pre>import java.util.regex.Matcher;
import java.util.regex.Pattern;
//from  w w  w.  j  a  v  a 2 s . com
public class Main {
  public static void main(String args[]) {
    Pattern p = Pattern.compile("java", Pattern.CASE_INSENSITIVE);

    String candidateString = "Java. java JAVA jAVA";

    Matcher matcher = p.matcher(candidateString);

    // display the latter match
    System.out.println(candidateString);
    matcher.find(11);
    System.out.println(matcher.group());

    // display the earlier match
    System.out.println(candidateString);
    matcher.find(0);
    System.out.println(matcher.group());
  }
}
</pre>

The code above generates the following result.

`Matcher` class performs a match on a sequence of characters by interpreting the compiled pattern defined in a `Pattern` object.

The `matcher()` method of the `Pattern` class creates an instance of the `Matcher` class.

<pre>import java.util.regex.Matcher;
import java.util.regex.Pattern;
/*from  ww  w .  ja  v  a2s.co m*/
public class Main {
  public static void main(String[] args) {
    String regex   = "[a-z]@.";
    Pattern p  = Pattern.compile(regex);
    String str = "abc@yahoo.com,123@cnn.com,abc@google.com";
    Matcher  m   = p.matcher(str);
  }
}
</pre>

The following methods of the Matcher performs the match.

*   find() method
*   start() method
*   end() method
*   group() method

## find method

The `find()` method finds a match for the pattern in the input.

If the find succeeds, it returns true. Otherwise, it returns false.

The first call to `find()` starts the search at the beginning of the input. The next call would start the search after the previous match.

We can use while loop with `find()` method to find all the matches.

`find()` method is an overloaded method. Another version of the find() method takes an integer argument, which is the offset to start the find for a match.

## start() method

The start() method returns the start index of the previous match. It is used after a successful find() method call.

## end() method

The `end()` method returns the index of the last character in the matched string plus one.

After a match, `str.substring(m.start(), m.end())` gives you the matched string.

<pre>import java.util.regex.Matcher;
import java.util.regex.Pattern;
//w ww.ja  v  a 2 s. co  m
public class Main {
  public static void main(String[] args) {
    String regex   = "[a-z]@.";
    Pattern p  = Pattern.compile(regex);
    String str = "abc@yahoo.com,123@cnn.com,abc@google.com";
    Matcher  m   = p.matcher(str);

    if (m.find())  {
      String  foundStr = str.substring(m.start(),  m.end());
      System.out.println("Found string  is:" + foundStr);
    }
  }
}
</pre>

The code above generates the following result.

![](http://www.java2s.com/Tutorials/JavaImage/myResult/E/END_METHOD__432BACDBB1C404DDBC97.PNG)

## group() method

The group() method returns the found string by the previous successful find() method call.

<pre>import java.util.regex.Matcher;
import java.util.regex.Pattern;
//from w  w  w  . j av a 2 s .co  m
public class Main {
  public static void main(String[] args) {
    String regex = "[a-z]@.";
    Pattern p = Pattern.compile(regex);
    String str = "abc@yahoo.com,123@cnn.com,abc@google.com";
    Matcher m = p.matcher(str);

    if (m.find()) {
      String foundStr = m.group();
      System.out.println("Found text is:" + foundStr);
    }
  }
}
</pre>

The code above generates the following result.

![](http://www.java2s.com/Tutorials/JavaImage/myResult/G/GROUP_METHOD__985A9EE2E6F3870D6741.PNG)

## Example

<pre>import java.util.regex.Pattern;
import java.util.regex.Matcher;
/*from   w w  w .j  a  v a 2s. c o  m*/
public class Main {
  public static void main(String[] args) {
    String regex = "[abc]@.";
    String source = "abc@example.com";
    findPattern(regex, source);
  }
  public static void findPattern(String regex, String source) {
    Pattern p = Pattern.compile(regex);
    Matcher m = p.matcher(source);

    System.out.println("Regex:" + regex);
    System.out.println("Text:" + source);
    while (m.find()) {
      System.out.println("Matched  Text:" + m.group() + ", Start:" + m.start()
          + ", " + "End:" + m.end());
    }
  }
}
</pre>

The code above generates the following result.

We can specify the number of times a character in a regular expression may match the sequence of characters.

To express a pattern "one digit or more" using a regular expression, we can use the quantifiers.

Quantifiers and their meanings are listed in the following Table.

QuantifiersMeaning*Zero or more times+One or more times?Once or not at all{m}Exactly m times{m,}At least m times{m, n}At least m, but not more than n times

The quantifiers must follow a character or character class.



## Example 2

`*` matches zero or more `d`.

<pre>import java.util.regex.Pattern;
//  w  ww .  j  a v a  2 s . c  om
public class Main {
  public static void main(String args[]) {

    String regex = "ad*";
    String input = "add";

    boolean isMatch = Pattern.matches(regex, input);
    System.out.println(isMatch);
  }
}
</pre>

The code above generates the following result.

## Example 2

`*` matches zero or more `d`.

<pre>import java.util.regex.Pattern;
//  w  ww .  j  a v a  2 s . c  om
public class Main {
  public static void main(String args[]) {

    String regex = "ad*";
    String input = "add";

    boolean isMatch = Pattern.matches(regex, input);
    System.out.println(isMatch);
  }
}
</pre>

The code above generates the following result.

## Example

The following code demonstrates how to match a word boundary using a regular expression.

<pre>//from  w w  w. j a v a 2 s  .  c  om
public class Main {
  public static void main(String[] args) {
    // \\b to get \b inside the string literal.
    String regex = "\\bJava\\b";
    String replacementStr = "XML";
    String inputStr = "Java and Javascript";
    String newStr = inputStr.replaceAll(regex, replacementStr);

    System.out.println("Regular  Expression: " + regex);
    System.out.println("Input String: " + inputStr);
    System.out.println("Replacement String:  " + replacementStr);
    System.out.println("New String:  " + newStr);
  }
}
</pre>

The code above generates the following result.

We can group multiple characters as a unit by parentheses. For example, `(ab)`.

Each group in a regular expression has a group number, which starts at 1.

Method `groupCount()` from `Matcher` class returns the number of groups in the pattern associated with the Matcher instance.

The group 0 refers to the entire regular expression and is not reported by the groupCount() method.

Each left parenthesis inside a regular expression marks the start of a new group.

We can back reference group numbers in a regular expression.

Suppose we want to match text that starts with "abc" followed by "xyz", which is followed by "abc".

We can write a regular expression as "abcxyzabc".

We can use the back reference to rewrite the regular expression as "(abc)xyz\1". `\1` refers to group 1, which is `(abc)`.

`\2` to refer to group 2, `\3` to refer to group 3, and so on.

The following code shows how to display formatted phone numbers. In the regular expression `\b(\d{3})(\d{3})(\d{4})\b`, `\b` denotes that we are interested in matching ten digits only at word boundaries.

<pre>import java.util.regex.Matcher;
import java.util.regex.Pattern;
// w ww.ja  v a2s  .  co m
public class Main {
  public static void main(String[] args) {
    String regex = "\\b(\\d{3})(\\d{3})(\\d{4})\\b";

    Pattern p = Pattern.compile(regex);
    String source = "1234567890, 12345,  and  9876543210";

    Matcher m = p.matcher(source);

    while (m.find()) {
      System.out.println("Phone: " + m.group() + ", Formatted Phone:  ("
          + m.group(1) + ") " + m.group(2) + "-" + m.group(3));
    }
  }
}
</pre>

The code above generates the following result.

![](http://www.java2s.com/Tutorials/JavaImage/myResult/D/DESCRIPTION__1E92DF93EE0765AD496B.PNG)

## Example

The following code shows how to reference groups in a replacement text.

`$n`, where `n` is a group number, inside a replacement text refers to the matched text for group `n`.

For example, `$1` refers to the first matched group. To reformat phone numbers, we would use `($1) $2-$3`.

<pre>import java.util.regex.Matcher;
import java.util.regex.Pattern;
/*ww  w .j a  v  a 2  s  . co m*/
public class Main {
  public static void main(String[] args) {
    String regex = "\\b(\\d{3})(\\d{3})(\\d{4})\\b";
    String replacementText = "($1) $2-$3";
    String source = "1234567890, 12345, and 9876543210";

    Pattern p = Pattern.compile(regex);
    Matcher m = p.matcher(source);

    String formattedSource = m.replaceAll(replacementText);

    System.out.println("Text: " + source);
    System.out.println("Formatted Text: " + formattedSource);
  }
}
</pre>

The code above generates the following result.

![](http://www.java2s.com/Tutorials/JavaImage/myResult/E/EXAMPLE__FBD771E58912055F17C4.PNG)
