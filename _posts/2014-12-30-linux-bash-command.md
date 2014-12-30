---
layout: post
title: Bash command to sum a column of numbers - Stack Overflow
date: 2014-12-30 10:43:00 +08:00
categories: [linux, bash]
---
#### 標題 : {{page.title}} ####

paste -sd+ infile | bc 

Using stdin:
<code>
<cmd> | paste -sd+ | bc
</code>

Edit: With some paste implementations you need to be more explicit when reading from stdin:
<code>
<cmd> | paste -sd+ - | bc
</code>
