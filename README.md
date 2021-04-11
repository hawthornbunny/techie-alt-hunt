# TheMajorTechie's alt-hunt challenge
On 25th March 2021, TheMajorTechie started an "alt-hunt" challenge, in which he claims to have an alternate account on Fimfiction and will award a prize to whomever identifies it first. The challenge was announced on his Fimfiction blog in the blog post [New 2nd alt hint! (+ details on what you get if you find it)][]:

> I suppose I should get around to choosing a prize, huh?
>
> Find the alt and you'll get a free story commission up to 20k words. I refuse to do anything NSFW regardless of if you found the alt or not. I'll work as closely as possible with you to make sure I get the story written the way you want it. PM me if you find it!

This document contains my (hawthornbunny's) findings so far, and is being periodically updated as the challenge continues.

## Important links
* [whatif.themajortechie.com][]: The website for TheMajorTechie's _What If..._ story. Most of the fragments are being hidden on this website.
* [TheMajorTechie's Fimfiction blog][]: Most hints are being posted here, as well as some indirect hints.
* [Techie's alt-hunt extravaganza! group][]: Fimfiction group for the challenge. TheMajorTechie is posting hints to this group as well as his own blog, and his comments sometimes contain hints.
* [#2nd alt hunt Fimfiction tag][]: Lists all of TheMajorTechie's Fimfiction blog posts that he's tagged as relating to the 2nd alt hunt, some of which contain hints. Posts which are specifically fragment hints are usually tagged `#hint`.
* [tmt-website `whatif` commits][]: The GitHub commit history for TheMajorTechie's website. Any change that he makes to the website can be seen here; usually, this just straight-up gives you the fragment. This is generally the best place to check if you're stuck. It's also useful for seeing the change history, which makes it easier to understand the context of older hints.

## Overview of the challenge
The main objective is to figure out which account on Fimfiction is an alternate account belonging to TheMajorTechie. (To be precise, it is his "second alt" since he already has a known one, [TechnoNerd](https://www.fimfiction.net/user/301253/TechnoNerd).

To do this, TheMajorTechie is posting hints nearly every day which point to "fragments". Each fragment is a piece of a large hex dump. When the fragments are decoded to bytes and assembled, they will presumably form a file which gives the name of the alt.

## Fragments
There are 41 fragments in total. We know this because TheMajorTechie has been posting a list of integers with each new hint, and the list gets longer by one each time. The integers generally match the file names of the fragments, indicating a one-to-one correspondence. (This is also one way to identify a hint post - if it has the fragment list, it's a hint to a fragment. The list can also be used to figure out which fragment the hint is for).

Based on the pattern that has been revealed so far, the complete fragment list will look like this:

    1 41 2 40 3 39 4 38 5 37 6 36 7 35 8 34 9 33 10 32 11 31 12 30 13 29 14 28 15 27 16 26 17 25 18 24 19 23 20 22 21

From this we can conclude that there are 41 fragments in the final file, and that the last fragment to be posted will be the 21st in the file.

### Identifying fragments
There are 2 ways a fragment can be referred to - by their chronological index (ie. the order in which they were posted) or their positional index (where they are in the final file). It doesn't really matter which we use since we can freely convert one to the other, but it's important to be clear about which identifier we're using to avoid confusion.

I've chosen to use the prefix `C` for chronological indices, and `P` for positional indices. Therefore, the first posted fragment is C1, and also P1 (since the first posted fragment also happens to be the first in the final file). The second posted fragment is C2 or P41, since it's the second posted but it's last in the file.

### Fragment structure
For the most part, every fragment is a hex dump. I don't recognize the dump format or what program was used to dump it - it doesn't look like Linux `hexdump`.

Each fragment consists of a header row, multiple body rows, and a footer row. Here is a truncated version of fragment C1, showing only the header, first body row, and footer:

    :020000020000FC
    :20000000504B0304140000000800F102795297B8A49EE79207006DA007001700000074684C
    ...383 more body rows...
    :00000001FF

The header and footer never seem to change - they're always `:020000020000FC` and `:00000001FF` respectively. I'm unsure why they're there, since they don't seem to relate to the dump data in any way and I can't figure out why the dumping tool would produce them. (They don't, for example, indicate the number of lines, nor do they identify the fragment in any way).

Each body row is 75 characters long and consists of 3 parts, with no separator between them:

* Character 1: Starting colon (:)
* Characters 2-9: Line number (hexadecimal)
* Characters 10-75: Dump line of 64 hex values representing representing 32 bytes

The line number is a little confusing. I have assumed it to be an 8-digit hexadecimal number, as this then leaves 64 characters for the dump line, which corresponds to 32 bytes - a natural row length for a hex dump. However, I've noticed that the line number always increments in steps of 2000 (hex), which is 8192 in decimal. This doesn't make sense to me since there obviously aren't 8192 bytes on each line. It's not the number of bits either (32 bytes is 256 bits). To be honest, I think the increment should be 20, not 2000, as this is 32 in decimal.

For now, I'm just going to suppose that the line number always has an extra `00` appended to it for some reason.

## Fragment list
The following is a list of the fragments in chronological ordering. Each section contains a table of information on the fragment, an explanation of how to obtain it, and any useful notes. The list will be updated as more fragments are found.

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

The two `.fragment` files together contain all of the dump fragment C2. However, they're a bit scrambled and some effort must be made to reconstruct the full fragment:

* `bottleFLIP.fragment` contains the first half of the fragment (dump lines 20000000 to 20068000).
* `say_hi.fragment` contains the second half (dump lines 2006A000 to 20136000), but the row list has been cut into two pieces near the middle and the two pieces swapped. This must be reversed before assembling the two halves of the fragment C2 together.

There is also one strange line in `say_hi.fragment` that I cannot account for:

    :1B138000453E21D701504B05060000000001000100690000001C93070000000F

It occurs before the footer, suggesting it's the last line of this fragment - but the line number, 1B138000, seems completely wrong, since the preceding line is 20136000. I would expect the line number to be 20138000, based on the established pattern.

It's also unclear to me how TheMajorTechie expected anyone to guess the correct URL from his hint - you would have to first guess that `say_hi` and `bottleFLIP` refer to files, and then you would have to guess that the files end with the extension `.fragment`. I don't think anyone would have gotten this. The only reasonable way to obtain this fragment is from the GitHub commit history.

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
* Hints
  * <https://www.fimfiction.net/blog/942500/->
  * <https://www.fimfiction.net/story/308542/what-if>

Solution: The blog post links to TheMajorTechie's anthology fic _What If..._. However, I'm not sure how Techie expected us to solve this one. The GitHub commit shows that he added a hex file named `the_reddest_herring.zip.040.hex` to the repo - however, it doesn't appear to be linked anywhere. He did change the `whatif.png` image on [whatif.themajortechie.com][] to `whatif.jpg`, but I can't figure out why that's significant.

Possibly he embedded the fragment in the fic somewhere, but I couldn't find it.

In any case, I'll assume that the `the_reddest_herring.zip.040.hex` file in GitHub is the fragment. (Note the `.zip` in the extension, however - either this is misdirection, or it could be a clue that the fragment dump is actually the dump of a zip file which we will need to unzip).

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

Techie posted the hint post in two places for this: his own blog, and the [Techie's alt-hunt extravaganza! group][]. This made it possible to identify this as fragment C5, as he said it was day 5 and we've had 4 fragments prior to this one.

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

The website also usefully confirmed that this is day 6, which proves this is fragment C6.

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

Solution: A TIFF file named `lovelyPicture.tif` was added to [whatif.themajortechie.com][]. Opening it shows a black-and-white image. Adjusting the contrast reveals a secret message containing a Pastebin URL, which contains fragment C7. (The Pastebin page names it as `file_4`, proving that this is also fragment P4).

*NOTE: Techie went back 2 days later and replaced this TIF file with a much larger one (see this commit: <https://github.com/TheMajorTechie/tmt-website/commit/89c9e278068103206c7a8c9e96f8087b358d22d9>). I'm not sure why he did this, since the new file appears to contain exactly the same content. Perhaps there was something wrong with the other one, although I had no problems opening it.*

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

### Fragment C11 (P6)

### Fragment C12 (P36)

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
* Chronological index: 10
* Positional index: 37
* Posted on: 2021-04-11
* GitHub commits
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

## Links
[TheMajorTechie's Fimfiction userpage]: https://www.fimfiction.net/user/234887/TheMajorTechie
[TheMajorTechie's Fimfiction blog]: https://www.fimfiction.net/user/234887/TheMajorTechie/blog
[Techie's alt-hunt extravaganza! group]: https://www.fimfiction.net/group/215617/techies-alt-hunt-extravaganza
[whatif.themajortechie.com]: https://whatif.themajortechie.com/
[tmt-website `whatif` commits]: https://github.com/TheMajorTechie/tmt-website/commits/whatif
[#2nd alt hunt Fimfiction tag]: https://www.fimfiction.net/search/blog-posts?q=%232nd+alt+hunt&s=date
[New 2nd alt hint! (+ details on what you get if you find it)]: https://www.fimfiction.net/blog/942118/new-2nd-alt-hint-details-on-what-you-get-if-you-find-it