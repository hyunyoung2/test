---
layout: post
title: What kind of Linux command is useful?
subtitle: During researching natural lanuage with Ubuntu, organizing Linux command that I have used. 
category: Natural Language Processing Labs
tags: [linux, command, nlp]
permalink: /2018/01/22/Linux_Command2/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

I dealt with some command of linux, and then I organized the command I have used once on [another blog](https://hyunyoung2.github.io/2017/6/27/Linux_Command/) of mine

That is too long post, so I will try to organize it again in here. 

# [Sed command](https://www.ibm.com/developerworks/library/l-sed2/)  with regular expression

 The following sed command will match a phrase beginning with "(" and ending with ")", and containing any number of characters inbetween 
 
 This phrase will be replaced with an empty string:

{% highlight shell linenos %}
 sed -e "s/(.*)//g" textfile
{% endhighlight %}

But It won't work well, That's because when sed tries to match the regular expression on a line, it finds the longest
match on the line like this : 

{% highlight shell lineon %}
Before sed command
제임스 얼 지미 카터 주니어 (  1924년 10월 1일 ~  ) 는 민주당 출신 미국 39번째 대통령  ( 1977년 ~ 1981년 ) 이다 .

After sed command
제임스 얼 지미 카터 주니어이다 .
{% endhighlight %}

My intention is :

{% highlight shell lineon %}
Before sed command
제임스 얼 지미 카터 주니어 (  1924년 10월 1일 ~  ) 는 민주당 출신 미국 39번째 대통령  ( 1977년 ~ 1981년 ) 이다 .

After sed command
제임스 얼 지미 카터 주니어는 민주당 출신 미국 39번째 대통령이다 .
{% endhighlight %}

If I want to do thing above, I change regular expression into the format, "a "(" character followed by any number of non-")" characters, and ending with a ")" character.

This will have the effect of matching the shortest possible match, rather than the longest possible one. 

Let's try it 

{% highlight shell linenos %}
 sed -e "s/([^)]*)//g" textfile
{% endhighlight %}

In the above example, the "[^)] specifies an "non-')'" character, and the "*" after it completes this expression to mean "zero or more than non-")" characters"

Also, another tutorial of sed command is [here](https://www.tutorialspoint.com/unix/unix-regular-expressions.htm)

# [Another usage of sed command](https://unix.stackexchange.com/questions/96226/delete-first-line-of-a-file)

Sometimes, You can use sed comand to remove some lines in a document. i.e. If you have a document but you want to get rid of fist and second line in the document, You can do it with sed command like this :

{% highlight shell linenos %}
sed '1d' file.txt > tmpfile; mv tmpfile file.txt # POSIX
sed -i '1d' file.txt # GNU sed only, creates a temporary file

# this is for perl user
perl -ip -e '$_ = undef if $. == 1' file.txt # also creates a temporary file
{% endhighlight %}

on the commands above, **sed '1d'** means erasing the first line in input file.

**sed '1d' file.txt > tmpfile...** means stdout is redirected to tmpfile with the sed command result. 

Also, if you want to delete several lines, prompt like this:

**sed '(start-line number), (end-line number)d' text_file > tempfile**

If you don't want to create tempfile, and then just want to overwrite on input file. Use **i** option like this:

**sed -i '(start-line number), (end-line number)d' text_file(input_file)**

i.e. if you use **i** option, the result of sed command will be overwritten in file.txt. i.e. the reuslt is overwritten to input file. 

# [paste command](https://stackoverflow.com/questions/2764051/how-to-join-multiple-lines-of-file-names-into-one-with-custom-delimiter)

When you want to paste several words which are in multiple lines to a line with some delimiter like "\t" or " ". 

Utilize **paste command** as follows

{% highlight shell linenos %}
 ls -1 | paste -sd " " - 
 
 
 $ ls -1 | paste -sd " " -
anaconda3 Desktop Documents Downloads konlp Music My_lab Pictures Practice_Project Public snap Templates Videos

{% endhighlight %}


**If you want to make a list formed line by line to a line with delimiter like white space**

Type in this :

{% highlight shell linenos %}
 cat file_name | paste -sd " " - > output_file_name
{% endhighlight %}

# [iconv command](https://www.mkssoftware.com/docs/man1/iconv.1.asp)

This is covertor from a encoding set to another encoding set. 

{% highlight shell linenos %}
  Usage: iconv [OPTION...] [FILE...]
 
 $ iconv -c -f cp949 -t utf8 input_file > output_file
{% endhighlight %}

# [awk command](https://www.thegeekstuff.com/2010/01/awk-introduction-tutorial-7-awk-print-examples)

If you deal with numerous data in linux, I recommend you to use this command jsut when you select some column as follow:

{% highlight shell linenos %}
 # Syntax:

# awk '/search pattern1/ {Actions}
#     /search pattern2/ {Actions}' file
     
 # If you have the following file
$cat employee.txt
100  Thomas  Manager    Sales       $5,000
200  Jason   Developer  Technology  $5,500
300  Sanjay  Sysadmin   Technology  $7,000
400  Nisha   Manager    Marketing   $9,500
500  Randy   DBA        Technology  $6,000

# If you wnat to select some column in the employee.txt 

$ awk '{print $2, $5;}' employee.txt
Thomas $5,000
Jason $5,500
Sanjay $7,000
Nisha $9,500
Randy $6,000
{% endhighlight %}

# [tr command](https://www.thegeekstuff.com/2012/12/linux-tr-command/)

If you translate a part into form you want to change, use this command as follows:

{% highlight shell linenos %}
  $ tr [OPTION] SET1 [SET2]
  
# hyunyoung2 @ hyunyoung2-desktop in ~ [14:50:46] 
$ echo "This is for testing" | tr " " "\t"
This	is	for	testing
{% endhighlight %}

another reference site is [a tutorial of awk command](https://www.tutorialspoint.com/unix_commands/awk.htm)

# [shuf command](https://shapeshed.com/unix-shuf/)

If you want to shuffle several lines and files into a file. use shuf command like this 

{% highlight shell linenos %}
$ shuf --help
Usage: shuf [OPTION]... [FILE]
  or:  shuf -e [OPTION]... [ARG]...

# hyunyoung2 @ hyunyoung2-desktop in ~ [17:59:39] 
$ shuf -e one two three four five six
one
five
two
six
three
four

# hyunyoung2 @ hyunyoung2-desktop in ~ [18:09:04] C:127
$ shuf -n 2 -e one two three four five six
six
four
{% endhighlight %}

As you can see the result above, **-n option** is to randomly select in a sequence above. 

and **-e** option is just for using stdin on command line. 

if you use stdin as files. type in like this :

> cat file1 file2 | shuf -o ouput.txt

**Be careful of the following one** When you use redirection of linux command such as **> output.txt**

the **output.txt** could be empty, that is because **> output.txt** is already executed before **shuf** command is done!.

you have to type in the command like this:

> shuf file1 -o output.txt  

or 

> shuf file1 --output=output.txt

or

> shuf file1 > output_flie && mv output_file resulting_output_file    


Keep in mind of **&&** lets you do something based on whether or not thr previous command completed successfully. 

i.e. do_somthing && do_something_else_that_depended_on_something

**gshuf is another way to randomly shuffle multiple lines**

# Reference 

 - [Sed command of IBM developerworks](https://www.ibm.com/developerworks/library/l-sed2/)
 
 - [Sed command tutorial](https://www.tutorialspoint.com/unix/unix-regular-expressions.htm)
 
 - [Another way to use sed command](https://unix.stackexchange.com/questions/96226/delete-first-line-of-a-file)
 
 - [paste stackoverflow](https://stackoverflow.com/questions/2764051/how-to-join-multiple-lines-of-file-names-into-one-with-custom-delimiter)

 - [iconv](https://www.mkssoftware.com/docs/man1/iconv.1.asp)
 
 - [THE GEEK STUFF's awk](https://www.thegeekstuff.com/2010/01/awk-introduction-tutorial-7-awk-print-examples)
 
 - [THE GEEK STUFF's tf](https://www.thegeekstuff.com/2012/12/linux-tr-command/)
 
 - [Shuf command](https://shapeshed.com/unix-shuf/)
 - [stackchange of shuf command](https://unix.stackexchange.com/questions/110490/why-does-the-command-shuf-file-file-leave-an-empty-file-but-similar-commands)
 - [Stackoverflow about "&&" in linux command](https://stackoverflow.com/questions/4510640/what-is-the-purpose-of-in-a-shell-command)


Korea ver. 
  - [awk command](https://recipes4dev.tistory.com/171)
