---
layout: post
title:  "Simplifying Blog Post File Creation"
author: Nikolai Shields
date:   2017-09-18 15:04:23
categories: [blog]
tags: [bash]
---
This evening I decided to work on the task of building out my website with jekyll, And I must say at this point in the process jekyll has been
an absolute joy! (More on that in another post)

One thing that I'm looking forward to in particular is jekyll's lack of a CMS, and curating posts via markdow/HTML with only text files, NO DATABASE, aint that a thing of beauty!
That said, I hate having to datestamp each post myself, so I thought what better than to automate this task, by hacking together a small addition
to my dotfiles to simply create my post template, timestamp it, and open it for editing all in one motion.

To do this I first needed to find the best way to pull down the timestamp.
Using the "Date" utility on most any unix system will do:

``` bash
$ date "+%f"
```
Next we need to add this to your .bashrc, or to some other script, my dotfiles are configured to make use of a file called .functions.
This file contains a number of small useful scripts that arent necessarily large enough to warrant a whole file to be dedicated to them
``` bash
function new-post() {
	T=$1
	DATE="$(date "+%F")"
	TITLE=$DATE-$T.md
	vim $TITLE
}
```

When the script above is run it does everything we wanted it to do, save one thing: generate our blog post template.
Now, like anything there are a number of ways to do this.
We could:

1. copy a pre-existing template file
2. generate the template on each run
3. something else

I like my odds with option 2, and I have a guess that it will look something like this:
```` bash
function new-post() {
  while getopts 'ha:t:c:g:' flag; do
	case "${flag}" in
		h) ;;
		a) AUTHOR="${OPTARG}" ;;
		t) TITLE="${OPTARG}" ;;
		c) CATEGORY="${OPTARG}" ;;
		g) TAG="${OPTARG}" ;;
		*) error "Unexpected option ${flag}" ;;
	esac
  done
  FILENAME="$(date "+%F")"-${TITLE// /-}.md

echo \
"---
layout: post
title: "$TITLE" 
author: "$AUTHOR"
date:  "$(date "+%F %T")"
categories: ["$CATEGORY"]
tags: ["$TAG"]
---" >> $FILENAME
}

`````
Now the above script does a few things, namely establishes the use of flags so we can pass relevant arguments,
some string manipulation to create the filename (by getting rid of those pesky spaces),
and uses the variables gathered by the arguments to generate our template.

When this command is run like so:
```
$ new-post -t "How to use this tool" -a foobar -c some-category -g random-tag
```
 we get:
```
2017-09-18-How-to-use-this-tool.md
```
Beautiful.
And when we take a peak inside:
```
---
title: How to use this tool
author: foobar
date:  2017-09-18 03:30:07
categories: [some-category]
tags: [random-tag]
---
```

Lastly, all we have left to do is to autimatically open an editor of our choosing.
For me that would be vim at time of writing.

So to achieve the desired functionality, we need to add "&& vim $FILENAME" to the end of our script.
**This same functionality can be achievied by substituing vim for atom/nano/emacs/whatever**

``` bash
# Create a new blog post / project post file and open with vim
function new-post() {
  while getopts 'ha:t:c:g:' flag; do
	case "${flag}" in
		h) ;;
		a) AUTHOR="${OPTARG}" ;;
		t) TITLE="${OPTARG}" ;;
		c) CATEGORY="${OPTARG}" ;;
		g) TAG="${OPTARG}" ;;
		*) error "Unexpected option ${flag}" ;;
	esac
  done
FILENAME=$(date "+%F")-${TITLE// /-}.md
echo \
"---
title: "$TITLE" 
author: "$AUTHOR"
date:  "$(date "+%F %T")"
categories: ["$CATEGORY"]
tags: ["$TAG"]
---" >> $FILENAME && vim $FILENAME
}
```

All done!
You can see it in action below (or at whatever coffee shop im in at the moment).


Happy Hacking 
**-N**
