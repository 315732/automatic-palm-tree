## What are regular expressions?

Regular expressions (or Regex) are patterns of text that you define to search documents and match exactly what you're looking for.

## Why should I learn how to use them?

Even if you won't need them sooner or later, it's a great tool to know how to use. It will make you more capable in CTF's, and potentially a better developer if that's a goal you have. You spend a little time learning it and save yourself lots of time in the long run by using it.

## I know all that, but I'm lazy.

This is a lazy person's tutorial. There's a little reading, and then you **learn by doing**.

## Where's the 'Deploy' button?

**There's no machine to deploy.** There are two ways to test your expressions. Either:

1. create a text file with some test paragraphs (in a Unix machine) and then use `egrep <pattern> <file>` to see what matches and what doesn't, or
2. use an online editor like [https://regexr.com/](https://regexr.com/). You can add your own text in the "Text" field, and then type your expressions (patterns) in the "Expression" field.

I recommend the second way.

---
When searching for a specific string in a file or block of text, you can search for it as is, with `grep 'string' <file>` . But what happens if you want to search for **patterns of text**? For example, you could be looking for a word that starts with a specific letter, or any words that end with numbers. That's where Regular Expressions come in.

Both of the aforementioned problems can be solved by using **charsets**. A charset is defined by enclosing in `[` square brackets `]` the character(s), or range of characters that you want to match.  Then, it finds **every occurrence** of the pattern you have defined in the file/text you are searching.

`[abc]` will match `a`, `b`, and `c` (every occurrence of each letter)

`[abc]zz` will match `azz`, `bzz`, and `czz`.

You can also use a `-` dash to define ranges:  
`[a-c]zz` is the same as above.

And then you can combine ranges together:  
`[a-cx-z]zz` will match `azz`, `bzz`, `czz`, `xzz`, `yzz`, and `zzz`.

Most notably, this can be used to match any alphabetical character:  
`[a-zA-Z]` will match any **single** letter (lowercase or uppercase).

You can use numbers too:  
`file[1-3]` will match `file1`, `file2`, and `file3`.

Then, there is a way to **exclude** characters from a charset with the `^` hat symbol, and include everything else.  
`[^k]ing` will match `ring`, `sing`, `$ing`, but not `king`.

Of course, you can exclude charsets, not just single characters.  
`[^a-c]at` will match `fat` and `hat`, but not `bat` or `cat`.

**Note 1**: Don't confuse strings with charsets. The charset `[abc]` will match the string `abc`, but also `cba` and `ca`. It doesn't match the string, but rather **every occurrence** of the specified characters in that string.

**Note 2**: When specifying charsets, you should type the letters in the same order they appear in the questions, to avoid typing something correct that is not the right answer.

**Note 3: Answering some of these questions is going to be tricky.** Often times there are many different patterns that match specific strings. That means (as stated in the previous note) that you may find a proper solution that isn't the right answer for this room (because there can only be one). The right answer is typically the most efficient regex for that question. Efficient in this context means 2 things:  
    **1. Be specific.** Here's an example: you could match any character from a to c using the `[a-z]` charset. But if the question only requires you to match characters from `a` to `c`, you should use the `[a-c]` charset, not `[a-z]`.  
    **2. Don't be too specific.** In contrast to the previous example, if a question requires you to match `a`, `c`, `f`, `r`, `s`, `z`, at that point, the expression that matches those specific characters would get longer and more complicated. So, it would make more sense to use `[a-z]`, because it is short and simple.

To reiterate, **there cannot be one single correct solution**. So if you've tested your solution and it works, you can take a break and come back to it later, or ask for a hint in discord, but try not to get frustrated.

Match all of the following characters: c, o, g

**flag: `[cog]`**

Match all of the following words: cat, fat, hat

**flag: `[cfh]at`**

Match all of the following words: Cat, cat, Hat, hat

**flag: `[CcHh]at`**

Match all of the following filenames: File1, File2, file3, file4, file5, File7, file9

**flag: `[Ff]ile[1-9]`**

Match all of the filenames of question 4, except "File7" (use the hat symbol)

**flag: `[Ff]ile[^7]`**

---
The wildcard that is used to match any single character (except the line break) is the `.` dot. That means that `a.c` will match `aac`, `abc`, `a0c`, `a!c`, and so on.

Also, you can set a character as optional in your pattern using the `?` question mark. That means that `abc?` will match `ab` and `abc`, since the `c` is optional.

Note: If you want to search for `.` a literal dot, you have to **escape it** with a `\` reverse slash. That means that `a.c` will match `a.c`, but also `abc`, `a@c`, and so on. But `a\.c` will match **just** `a.c`.

Match all of the following words: Cat, fat, hat, rat

**flag: `.at`**

Match all of the following words: Cat, cats

**flag: `[Cc]ats?`**

Match the following domain name: cat.xyz

**flag: ``**

Match all of the following domain names: cat.xyz, cats.xyz, hats.xyz

**flag: ``**

Match every 4-letter string that doesn't end in any letter from n to z

**flag: ``**

Match bat, bats, hat, hats, but not rat or rats (use the hat symbol)

**flag: ``**