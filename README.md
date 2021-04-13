# TheMajorTechie's alt-hunt challenge
On 25th March 2021, [TheMajorTechie](https://www.fimfiction.net/user/234887/TheMajorTechie) started an "alt-hunt" challenge, in which he claims to have an alternate account on Fimfiction and will award a prize to whomever identifies it first. The challenge was announced on his Fimfiction blog in the blog post [New 2nd alt hint! (+ details on what you get if you find it)][]:

> I suppose I should get around to choosing a prize, huh?
>
> Find the alt and you'll get a free story commission up to 20k words. I refuse to do anything NSFW regardless of if you found the alt or not. I'll work as closely as possible with you to make sure I get the story written the way you want it. PM me if you find it!

This document contains my (hawthornbunny's) findings so far, and is being periodically updated as the challenge continues.

## Important links
* [whatif.themajortechie.com][]: The website for TheMajorTechie's _What If..._ story. Most of the fragments are being hidden on this website.
* [TheMajorTechie's Fimfiction blog][]: Most hints are being posted here, as well as some indirect hints.
* [Techie's alt-hunt extravaganza! group][]: Fimfiction group for the challenge. TheMajorTechie is posting hints to this group as well as his own blog, and his comments sometimes contain hints.
* [#2nd alt hunt Fimfiction tag][]: Lists all of TheMajorTechie's Fimfiction blog posts that he's tagged as relating to the 2nd alt hunt, some of which contain hints. Posts which are specifically fragment hints are usually tagged `#hint`.
* [tmt-website `whatif` commits][]: The GitHub commit history for TheMajorTechie's website. Any change that he makes to the website can be seen here; usually, this just straight up gives you the fragment. This is generally the best place to check if you're stuck. It's also useful for seeing the change history, which makes it easier to understand the context of older hints.

## Overview of the challenge
The main objective is to figure out which account on Fimfiction is an alternate account belonging to TheMajorTechie. (To be precise, it is his "second alt" since he already has a known one, [TechnoNerd](https://www.fimfiction.net/user/301253/TechnoNerd)).

To do this, TheMajorTechie is posting hints nearly every day which point to "fragments". Each fragment is a file containing encoded binary data. When all of the fragments are found, decoded to bytes, and assembled in the correct sequence, they will presumably form one large file which gives the name of the TheMajorTechie's alternate account.

## Fragments
There are 41 fragments in total. We know this because TheMajorTechie has been posting a list of integers with each new hint, and the list gets longer by one each time. The integers generally match the file names of the fragments, indicating a one-to-one correspondence. (This is also one way to identify a hint post - if it has the fragment list, it's a hint to a fragment. The list can also be used to figure out which fragment the hint is for).

Based on the pattern that has been revealed so far, the complete fragment list will look like this:

    1 41 2 40 3 39 4 38 5 37 6 36 7 35 8 34 9 33 10 32 11 31 12 30 13 29 14 28 15 27 16 26 17 25 18 24 19 23 20 22 21

From this we can conclude that there are 41 fragments in the final file, and that the last fragment to be posted will be the 21st in the file.

NOTE: Techie independently confirmed the existence of 41 fragments in [this comment](https://www.fimfiction.net/group/215617/techies-alt-hunt-extravaganza#comment/442022) on the Techie's alt-hunt extravaganza! group.

### Referencing fragments
There are 2 ways to refer to a fragment - by its chronological index (ie. when it was posted) or its positional index (where it is in the final file). It doesn't really matter which index we use since we can freely convert one to the other - however, it's important to be clear about which identifier we're using to avoid confusion.

I've chosen to use the prefix C for chronological indices, and P for positional indices. Therefore, the first posted fragment is C1, and also P1 (since the first posted fragment also happens to be the first in the final file). The second posted fragment is C2 or P41, since it's the second posted but it's last in the file.

### Fragment format
Each fragment is in Intel HEX format (`.hex`), which can be recognized by the colon at the start of every line (the _start code_). Every line of a `.hex` file is called a _record_, and contains some data (along with other metadata fields, such as a checksum).

I will not go too deeply into the details of the Intel HEX format - for more information on how to read it, see the [Intel HEX Wikipedia article][]. For the purposes of this challenge, however, it is useful to know that the 4-digit _address_ of a record in a `.hex` file is given by characters 4 to 7.

For example, in this record from fragment C1:

    :2001E0000AE3437D4A6B0FA69B775E5331FF32E153553BB5C0DDA768161BCF511A56415943

Characters 4 to 7 are `01E0`, so that's the (hexadecimal) address of this record. Knowing the address can be useful in fragments that have been scrambled in some way, as this allows you to spot and correct it.

Otherwise, all you need to know about Intel HEX is that a `.hex` file is an ASCII encoding of binary data which can be decoded into bytes. I'm using the [Python intelhex][] library to decode them.

## Fragment list
The following is a list of all fragments found so far in chronological ordering. Each section contains a table of information on the fragment, an explanation of how to obtain it, and any useful notes. The list will be updated as more fragments are found.

### Fragment C1 (P1)
* Chronological index: 1
* Positional index: 1
* Posted on: 2021-03-25
* GitHub commits
  * <https://github.com/TheMajorTechie/tmt-website/commit/d69e02bd56404e267e0a570c805481c841b9316f>
* Relevant URLs
  * <https://whatif.themajortechie.com/>
* Hints
  * <https://www.fimfiction.net/blog/942118/new-2nd-alt-hint-details-on-what-you-get-if-you-find-it>

Solution: The blog post linked to [whatif.themajortechie.com][], and the fragment was in an HTML comment in the page source.

### Fragment C2 (P41)
* Chronological index: 2
* Positional index: 41
* Posted on: 2021-03-26
* GitHub commits
  * <https://github.com/TheMajorTechie/tmt-website/commit/9fec0009976d52f0f17e4391daa332d19695d089>
* Relevant URLs
  * <https://whatif.themajortechie.com/>
  * <https://whatif.themajortechie.com/bottleFLIP.fragment>
  * <https://whatif.themajortechie.com/say_hi.fragment>
* Hints
  * <https://www.fimfiction.net/blog/942244/day-2-clues-updated-the-what-if-website>

Solution: The blog post linked to [whatif.themajortechie.com][], which added a new HTML comment: `<!--say_hi and do a bottleFLIP while you're at it!-->`. The GitHub commit shows that two files were added to the site repository: `bottleFLIP.fragment` and `say_hi.fragment`. These are downloadable at Relevant URLs above.

The two `.fragment` files together contain all of the fragment C2. However, they're a bit scrambled and some effort must be made to reconstruct the full fragment:

* `bottleFLIP.fragment` contains the first half of the fragment (records 0000 to 0680).
* `say_hi.fragment` contains the second half (records 06A0 to 1380), but the row list has been cut into two pieces near the middle and the two pieces swapped. This must be reversed before assembling the two halves of the fragment C2 together.

It's unclear to me how TheMajorTechie expected anyone to guess the correct URL from his hint - you would have to first guess that `say_hi` and `bottleFLIP` refer to files, and then you would have to guess that the files end with the extension `.fragment`. I don't think anyone would have gotten this. The only reasonable way to obtain this fragment is from the GitHub commit history.

### Fragment C3 (P2)
* Chronological index: 3
* Positional index: 2
* Posted on: 2021-03-27
* GitHub commits
  * <https://github.com/TheMajorTechie/tmt-website/commit/3847b181eee929e348d51b0188731b7cbf1b84a3>
* Relevant URLs
  * <https://whatif.themajortechie.com/wrong.ERROR> (or any nonexistent URL)
  * <https://whatif.themajortechie.com/img/the_reddest_herring.002.hex>
* Hints
  * <https://www.fimfiction.net/blog/942376/wrongerror>

Solution: The blog post contained the hint "it is not found.". This is obviously a reference to the 404 not found page, which can be reached by entering any nonexistent URL. Doing so gives a link ("You found me! Have the next fragment. :)") to a file named `the_reddest_herring.002.hex`, which contains the fragment.

### Fragment C4 (P40)
* Chronological index: 4
* Positional index: 40
* Posted on: 2021-03-28
* GitHub commits
  * <https://github.com/TheMajorTechie/tmt-website/commit/8b23fb898888d8a23e6790c70341fa7ca26a8c73>
* Relevant URLs
  * <https://whatif.themajortechie.com>
  * <https://whatif.themajortechie.com/the_reddest_herring.zip.040.hex>
* Hints
  * <https://www.fimfiction.net/blog/942500/->

Solution: The GitHub commit shows that Techie changed the button image on [whatif.themajortechie.com][] from `whatif.png` to `whatif.jpg`. I couldn't figure this one out at first, since it didn't seem like a particularly significant change - however, a hexdump of the `whatif.jpg` file revealed that the fragment is appended to the end of that file. Interestingly this doesn't seem to prevent the image from displaying at all, which was a good way to conceal the fragment in GitHub.

One oddity, however, is that Techie also uploaded a file named `the_reddest_herring.zip.040.hex` to the site, which you can simply download. I don't understand why he did this - it wasn't necessary, since the file is already contained in `whatif.jpg`. Adding this file effectively bypasses the challenge entirely since you now don't need to figure out the trick with the jpeg file.

Also note the `.zip` in the file extension - either this is misdirection, or it could be a clue that the fragment is actually a zip file which we will need to unzip.

### Fragment C5 (P3)
* Chronological index: 7
* Positional index: 4
* Posted on: 2021-03-29
* GitHub commits
  * <https://github.com/TheMajorTechie/tmt-website/commit/7e572a55c0847a726da2e96d96823db09a225154>
  * <https://github.com/TheMajorTechie/tmt-website/commit/740ef06ac46a3b4be98f50960877fdf23eecc2ee>
* Relevant URLs
  * <https://whatif.themajortechie.com/threepigs.docx>
* Hints
  * <https://www.fimfiction.net/blog/942624/threepigsdocx>
  * <https://www.fimfiction.net/group/215617/techies-alt-hunt-extravaganza/thread/465605/day-5>

Techie posted the hint post in two places for this: his own blog, and the [Techie's alt-hunt extravaganza! group][].

The hint was a link to a file named `threepigs.docx`, with the line "corruption isn't the end". docx is the OpenOffice document format, so I tried to open it with LibreOffice - however, LibreOffice claims the document is corrupt.

Interestingly, vim was able to open the file and found it to be a zip container. When I unzipped it, I found it contained several XML files defining a document. This suggests that it really is a .docx file - I suspect that, as per the hint, Techie has manually corrupted the end of the file somehow.

I did a hexdump of the file and found that fragment C5 has simply been appended to the end of it. (I would have seen this if vim had actually opened the raw bytes of the file, but it didn't, since it thought it was a zip and unzipped it for me). Interestingly, appending these bytes didn't seem to prevent it being recognized as a zip.

To separate the fragment from the file, I opened vim and used the following command:

    :noautocmd e threepigs.docx

This disables the autocommand that would open the document as a zip, then opens the document. The fragment can then be removed from the file.

### Fragment C6 (P39)
* Chronological index: 6
* Positional index: 39
* Posted on: 2021-03-30
* GitHub commits
  * <https://github.com/TheMajorTechie/tmt-website/commit/cd091593467dd6740b8be35432014e75b7e690a7>
* Relevant URLs
  * <https://whatif.themajortechie.com/README.md>
* Hints
  * <https://www.fimfiction.net/blog/942740/i-wonder-if-you-can-read-this>

Techie updated the [whatif.themajortechie.com][] website with the following hint:

> Now, I wonder where you can READ ME...

This refers to the `README.md` file in the site's GitHub repo, which contains an HTML comment with a fragment inside it. The fragment is encoded, however - each character of the fragment has been replaced by its hexadecimal ASCII code. To obtain the fragment, this needs to be decoded.

### Fragment C7 (P4)
* Chronological index: 7
* Positional index: 4
* Posted on: 2021-04-02
* GitHub commits
  * <https://github.com/TheMajorTechie/tmt-website/commit/7e572a55c0847a726da2e96d96823db09a225154>
  * <https://github.com/TheMajorTechie/tmt-website/commit/740ef06ac46a3b4be98f50960877fdf23eecc2ee>
* Relevant URLs
  * <https://www.fimfiction.net/blog/943219/the-secrets-lay-within>
  * <https://whatif.themajortechie.com>
  * <https://pastebin.com/96ZCiK7u>

Solution: A TIFF file named `lovelyPicture.tif` was added to [whatif.themajortechie.com][]. Opening it shows a black-and-white image. Adjusting the contrast reveals a secret message containing a Pastebin URL, which contains fragment C7.

*NOTE: Techie went back 2 days later and replaced this TIFF file with a much larger one (see this commit: <https://github.com/TheMajorTechie/tmt-website/commit/89c9e278068103206c7a8c9e96f8087b358d22d9>). I'm not sure why he did this, since the new file appears to contain exactly the same content. Perhaps there was something wrong with the other one, although I had no problems opening it.*

### Fragment C8 (P38)
* Chronological index: 8
* Positional index: 38
* Posted on: 2021-04-04
* Hints
  * <https://www.fimfiction.net/blog/943501/ran-out-of-ideas-so-have-fragment-38-in-the-raw>

Solution: Techie just gave us this one for free by posting the fragment on his blog.

### Fragment C9 (P5)
* Chronological index: 9
* Positional index: 5
* Posted on: 2021-04-05
* GitHub commits
  * <https://github.com/TheMajorTechie/tmt-website/commit/6bdec9c55fe8baa5ae781568a559bd5d8750df4c>
* Relevant URLs
  * <https://whatif.themajortechie.com>
* Hints
  * <https://www.fimfiction.net/blog/943637/1-41-2-40-3-39-4-38-5>

The blog post gave the following hint:

> Sometimes it's the little things. :)

The GitHub commit shows that Techie replaced the favicon of [whatif.themajortechie.com][] (`favicon.png`) with a new file named `faviconNew.png`, and also uploaded a file named `the_reddest_herring.zip.005.zip`. I assume the "little things" hint refers to the characteristic small size of a favicon.

After some examination of `faviconNew.png` and comparing it to the zip file I obtained from GitHub, I eventually discovered that the favicon is somehow both a PNG and a zip at the same time - that is, it displays as a PNG, but it contains zip archive data and can simply be extracted like any normal zip file. Unzipping it yields a fragment named `the_reddest_herring.zip.005.hex`.

I think I got a bit lucky with this one - it looks like Techie didn't mean to upload the `the_reddest_herring.zip.005.zip` file to GitHub (he deleted it immediately). If he had just uploaded the favicon, I might not have figured this one out.

### Fragment C10 (P37)
* Chronological index: 10
* Positional index: 37
* Posted on: 2021-04-06
* GitHub commits
  * <https://github.com/TheMajorTechie/tmt-website/commit/a6eed8d3b0ff348bb5a244cc0929bbee84d6e0e6>
* Relevant URLs
  * <https://whatif.themajortechie.com>
  * <https://whatif.themajortechie.com/bottleFLIP.fragment>
  * <https://whatif.themajortechie.com/037.7z>
  * <https://themajortechie.neocities.org/museum.html>
* Hints
  * <https://www.fimfiction.net/blog/943775/revisit-the-past>

Solution: Techie added an HTML comment to [whatif.themajortechie.com][]: `<!--i suppose a bottleflip is nice to have once in a while.-->`. This was a hint to look back at `bottleFLIP.fragment`, which was discovered with fragment C2. Techie updated this file with the string `037.7z`, indicating the location of a new file on the whatif website.

As the name suggests, `037.7z` is a 7zip archive. Extracting the file produces a file called `037.pdn`.

`.pdn` files are Paint.NET, an old Windows image editing program. This is presumably what the hint was indicating:

> what is old is now new again.

By reading the raw file data I was able to ascertain that the file contained multiple layers, and I even managed to extract a thumbnail of what the image looks like (it's one of TheMajorTechie's meme emojis) - however, I guessed that the file contained a hidden layer that I would need Paint.NET to open. This presented a big problem for me, as I simply don't have any Windows machines, and Paint.NET is notoriously unsupported on Linux.

In the end, I sent the file to fellow Fimfictioneer [SweetAI Belle](https://www.fimfiction.net/user/98035/SweetAI+Belle), who I know has used Paint.NET, and she kindly found the hidden layer for me.

The layer contained the URL <https://themajortechie.neocities.org/museum.html>. This is the URL of TheMajorTechie's Neocities site. Fragment C10 can be found in the source of that site.

### Fragment C11 (P6)
* Chronological index: 11
* Positional index: 6
* Posted on: 2021-04-07
* GitHub commits
  * <https://github.com/TheMajorTechie/tmt-website/commit/fa9dc53fba0d5e6a3dc17c69b51fd245ffa37acf>
  * <https://github.com/TheMajorTechie/tmt-website/commit/683376ac9d7c39b3889dc72a04a453b04e19d25d>
  * <https://github.com/TheMajorTechie/tmt-website/commit/29f22925fb9a552102a10bc3989a10729499f7da>
* Relevant URLs
  * <https://whatif.themajortechie.com>
  * <https://whatif.themajortechie.com/6.dc42>
  * <https://whatif.themajortechie.com/the_reddest_herring.zip.006.7z>
* Hints
  * <https://www.fimfiction.net/blog/943893/file-6-has-been-posted-early-because-dangit-i-have-a-lotta-homework-to-do-right-now>

Solution: Techie added a button to [whatif.themajortechie.com][] with the following label:

> Sometimes, it's the legacy of the past that will assist you toward the future.

He also added the following comment to the HTML source:

    <!--Say hi to Lisa for me. :) Oh wait, forgot the file itself. It's the_reddest_herring.zip.006.7z-->

As the hint says, a 7zip file named `the_reddest_herring.zip.006.7z` can be downloaded from [whatif.themajortechie.com][]. However, this only gets you part of the way there, as the file is password-protected and requires a password to be unzipped.

Clicking on the aforementioned button downloads a file named `6.dc42`. This appears to be a disk image format used by the Apple Lisa, an Apple computer released in 1983 - hence the hint "Say hi to Lisa for me". See the [Apple Lisa Wikipedia article](https://en.wikipedia.org/wiki/Apple_Lisa) for more information on the machine.

To read this format, we therefore need a Lisa emulator. This can be downloaded from the [Lisa Emulator Project](https://lisa.sunder.net/).

Unfortunately for me, the Linux version of this emulator has to be built from source and the build procedure looks an utter mess. However, it turned out that the Windows version surprisingly runs more or less perfectly under Wine, so I used that instead.

With absolutely no experience of the Apple Lisa, I had to tinker a bit to figure out how to actually start it. Inserting the `6.dc42` file as a diskette didn't work (even though it's the correct format, apparently the file is not a diskette image). Eventually I found that specifying `6.dc42` as the boot ROM in the preferences was good enough.

Once the Apple Lisa is booted with the `6.dc42` file, the disk can be opened. It contains several files, including one named `:)`. Opening the `:)` file reveals a message:

> You found me! Here's the password that you're looking for.
>
> howMuchJ4mCanaJam$1AmCramIfaClamcancantCramslAm

This is the password to unzip the file `the_reddest_herring.zip.006.7z`. Doing so produces fragment C11.

### Fragment C12 (P36)
* Chronological index: 12
* Positional index: 36
* Posted on: 2021-04-08
* Relevant URLs
  * <https://whatif.themajortechie.com>
  * <https://whatif.themajortechie.com/the_reddest_herring.zip.006.7z>
* Hints
  * <https://www.fimfiction.net/group/215617/techies-alt-hunt-extravaganza/thread/466417/eh-tonights-fragment-is-tacked-onto-the-end-of-yesterdays-fragment-have-fun-yall>
  * <https://www.fimfiction.net/blog/944058/eh-tonights-fragment-is-tacked-onto-the-end-of-yesterdays-fragment-have-fun-yall>

The hint blog says:

> eh. tonight's fragment is tacked onto the end of yesterday's fragment. have fun yall

It's a shame Techie gave the answer to this one, because I thought it was quite a clever way to hide this fragment. Yesterday's file `the_reddest_herring.zip.006.7z` actually contains _two_ fragments - the first is fragment C11, the one that's locked inside the password-protected archive. But it also contains fragment C12, which - like several other fragments have been - was simply appended directly to the end of the file data. Chances are you wouldn't look twice if you thought you'd already found the fragment, so this was a neat way to hide it.

### Fragment C13 (P7)
* Chronological index: 13
* Positional index: 7
* Posted on: 2021-04-10
* GitHub commits
  * <https://github.com/TheMajorTechie/tmt-website/commit/a7ac402204b49af4bc8a8c9dba7a01c97e26d28d>
  * <https://github.com/TheMajorTechie/tmt-website/commit/94a9a7739ac0238e36aae2126876989383793ef6>
* Relevant URLs
  * <https://whatif.themajortechie.com>
  * <https://whatif.themajortechie.com/the_reddest_herring.zip.007.hex>
* Hints
  * <https://www.fimfiction.net/blog/944342/excavation-time>

The blog gave the following hint:

> Dig a little deeper into what you already know.

The [whatif.themajortechie.com][] website was updated with the following comment above the `<!--Day1-->` block which contained fragment C1:

    <!--oh boy, is it time to excavate? I'll get my shovel!-->

The "what you already know" obviously refers to this fragment. A close inspection of the fragment reveals that some of the hex characters have been replaced by new ones, so the "excavate" hint refers to digging these characters out.

Doing so reveals `the_reddest_herring.zip.007.hex`, but you can just download the fragment straight from GitHub anyway. I'm not really sure how Techie expects to hide them if he knows people can just check GitHub, unless they really are all red herrings.

### Fragment C14 (P35)
* Chronological index: 14
* Positional index: 35
* Posted on: 2021-04-11
* GitHub commits
  * <https://github.com/TheMajorTechie/tmt-website/commit/f0ebb0e38ca32446f2d206bee89ea44d72be9f69>
  * <https://github.com/TheMajorTechie/tmt-website/commit/47a28f97e65f35b77089094d3f917fd1d24f3867>
* Relevant URLs
  * <https://whatif.themajortechie.com>
  * <https://whatif.themajortechie.com/the_reddest_herring.zip.035.hex>
* Hints
  * <https://www.fimfiction.net/group/215617/techies-alt-hunt-extravaganza/thread/466658/i-wonder-what-da-button-do>
  * <https://www.fimfiction.net/blog/944474/i-wonder-what-da-button-do>

Techie added an HTML comment inside the href of the button on [whatif.themajortechie.com][]:

    <!--the_reddest_herring.zip.035.hex-->

This isn't a valid place for an HTML comment, since hrefs are interpreted as strings - indeed, you can see what he added just by hovering over the button. The `the_reddest_herring.zip.035.hex` file can be downloaded straight from the document root of the site. Didn't even need to go to GitHub for this one.

### Fragment C15 (P8)
* Chronological index: 15
* Positional index: 8
* Posted on: 2021-04-12
* Hints
  * <https://www.fimfiction.net/group/215617/techies-alt-hunt-extravaganza/thread/466751/anyone-still-doing-this>
  * <https://www.fimfiction.net/blog/944607/anyone-still-doing-this>

Solution: As before, Techie gave this one for free by posting it directly.

### Fragment C16 (P34)

### Fragment C17 (P9)

### Fragment C18 (P33)

### Fragment C19 (P10)

### Fragment C20 (P32)

### Fragment C21 (P11)

### Fragment C22 (P31)

### Fragment C23 (P12)

### Fragment C24 (P30)

### Fragment C25 (P13)

### Fragment C26 (P29)

### Fragment C27 (P14)

### Fragment C28 (P28)

### Fragment C29 (P15)

### Fragment C30 (P27)

### Fragment C31 (P16)

### Fragment C32 (P26)

### Fragment C33 (P17)

### Fragment C34 (P25)

### Fragment C35 (P18)

### Fragment C36 (P24)

### Fragment C37 (P19)

### Fragment C38 (P23)

### Fragment C39 (P20)

### Fragment C40 (P22)

### Fragment C41 (P21)

[TheMajorTechie's Fimfiction userpage]: https://www.fimfiction.net/user/234887/TheMajorTechie
[TheMajorTechie's Fimfiction blog]: https://www.fimfiction.net/user/234887/TheMajorTechie/blog
[Techie's alt-hunt extravaganza! group]: https://www.fimfiction.net/group/215617/techies-alt-hunt-extravaganza
[whatif.themajortechie.com]: https://whatif.themajortechie.com/
[tmt-website `whatif` commits]: https://github.com/TheMajorTechie/tmt-website/commits/whatif
[#2nd alt hunt Fimfiction tag]: https://www.fimfiction.net/search/blog-posts?q=%232nd+alt+hunt&s=date
[New 2nd alt hint! (+ details on what you get if you find it)]: https://www.fimfiction.net/blog/942118/new-2nd-alt-hint-details-on-what-you-get-if-you-find-it
[Intel HEX Wikipedia article]: https://en.wikipedia.org/wiki/Intel_HEX
[Python intelhex]: https://pypi.org/project/intelhex/
