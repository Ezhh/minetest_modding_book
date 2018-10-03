---
title: Releasing a Mod
layout: default
root: ../..
idx: 7.5
redirect_from: /en/chapters/releasing.html
---

## Introduction

Releasing, or publishing, a mod allows other people to make use of it. Once a mod has been
released it might be used in singleplayer games or on servers, including public servers.

* [License Choices](#license-choices)
* [Packaging](#packaging)
* [Uploading](#uploading)
* [Forum Topic](#forum-topic)

## License Choices

You need to specify a license for your mod. This is important because it tells other
people the ways in which they are allowed to use your work. If your mod doesn't have
a license, people won't know whether they are allowed to modify, distribute or use your 
mod on a public server.

Your code and your art need different things from the licenses they use. For example,
Creative Commons licenses shouldn't be used with source code,
but can be suitable choices for artistic works such as images, text and meshes.

You are allowed any license; however, mods which disallow derivatives are banned from the
official Minetest forum. (For a mod to be allowed on the forum, other developers must be
able modify it and release the modified version.)

Please note that **public domain is not a valid licence**, because the definition varies
in different countries.

### LGPL and CC-BY-SA

This is a common license combination in the Minetest community, and is what
Minetest and minetest_game use.
You license your code under LGPL 2.1 and your art under CC-BY-SA. This means:

* Anyone can modify, redistribute and sell modified or unmodified versions.
* If someone modifies your mod, they must give their version the same license.
* Your copyright notice must be kept.

### WTFPL and CC0

These licenses allows anyone to do what they want with your mod.
This means they can modify, redistribute, sell, or leave out attribution.
These licenses can be used for both code and art.

It is important to note that WTFPL is strongly discouraged and people may
choose not to use your mod if it has this license.

### MIT

This is a common license for mod code. The only restriction it places on users
of your mod is that they must include the same copyright notice and license
in any copies of the mod or of substantial parts of the mod.

## Packaging

There are some files it is recommended to include in your mod
when you release it.

### README.txt

The readme file should state:

* What the mod does.
* What the license is.
* Current version of mod.
* How to install the mod.
* What dependencies there are / what the user needs to install.
* Where to report problems/bugs or get help.

See the [appendix](#appendix-readme-and-forum-generator) for an example readme and
readme generator.

### description.txt

This should explain what your mod does. Be concise without being vague.
It should be short because it will be displayed in the content installer which has
limited space.

Good example:

    Adds soup, cakes, bakes and juices.

Don't do this:

    (BAD)  The food mod for Minetest.

### screenshot.png

Screenshots should be 3:2 (3 pixels of width for every 2 pixels of height)
and have a minimum size of 300 x 200px.

The screenshot is displayed in the mod store.

Uploading
---------

So that a potential user can download your mod, you need to upload it somewhere
publicly accessible. There are several ways to do this, but you should use the
approach that works best for you, as long as it meets these requirements, and any
others which may be added by forum moderators:

* **Stable**      - The hosting website should be unlikely to shut down without warning.
* **Direct link** - You should be able to click a link on the forum and download the file
                   without having to view another page.
* **Virus Free**  - Mods with malicious content will be removed from the forum.

### Version Control Systems

It is recommended that you use a version control system which:

* Allows other developers to easily submit changes.
* Allows the code to be previewed before downloading.
* Allows users to submit bug reports.

The majority of Minetest developers use GitHub as a website to host their code,
but alternatives are possible. 

Using a GitHub can be difficult at first. If you need help with this, for
information on using GitHub, please see:

* [Using Git](http://git-scm.com/book/en/v1/Getting-Started) - Basic concepts. Using the command line.
* [GitHub for Windows](https://help.github.com/articles/getting-started-with-github-for-windows/) -
Using a graphical interface on Windows to upload your code.

### Forum Attachments

As an alternative to using a version management system, you can use forum attachments to share
your mods. This can be done when creating a mod's forum topic (covered below).

You need to zip the files for the mod into a single file. How to do this varies from
operating system to operating system.

If you use Windows, go to the mod's folder and select all the files.
Right click, Send To > Compressed (zipped) folder.
Rename the resulting zip file to the name of your mod.

When making a forum topic, on the "Create a Topic" page (see below), go to the
"Upload Attachment" tab at the bottom.
Click "Browse" and select the zipped file. It is recommended that you
enter the version of your mod in the comment field.

<figure>
    <img src="{{ page.root }}//static/releasing_attachments.png" alt="Upload Attachment">
    <figcaption>
        Upload Attachment tab.
    </figcaption>
</figure>

## Forum Topic

You can now create a forum topic. You should create it in
the ["WIP Mods"](https://forum.minetest.net/viewforum.php?f=9) (Work In Progress)
forum.\\
When you consider your mod no longer a work in progress, you can
[request that it be moved](https://forum.minetest.net/viewtopic.php?f=11&t=10418)
to "Mod Releases."

### Content

The requirements of a forum topic are mostly the same as the recommendations for
a readme file. The topic should include:

* What the mod does.
* What the license is.
* Current version of mod.
* How to install the mod.
* What dependencies there are.
* Where to report problems/bugs or get help.
* Link to download, or an attachment.

You should also include screenshots of your mod in action, if relevant.

The Minetest forum uses bbcode for formatting. Here is an example for a
mod named superspecial:


    Adds magic, rainbows and other special things.

    See download attached.

    [b]Version:[/b] 1.1
    [b]License:[/b] LGPL 2.1 or later

    Dependencies: default mod (found in minetest_game)

    Report bugs or request help on the forum topic.

    [h]Installation[/h]

    Unzip the archive, rename the folder to superspecial and
    place it in minetest/mods/

    (  GNU/Linux: If you use a system-wide installation place
        it in ~/.minetest/mods/.  )

    (  If you only want this to be used in a single world, place
        the folder in worldmods/ in your world directory.  )

    For further information or help see:
    [url]http://wiki.minetest.com/wiki/Installing_Mods[/url]

If you modify the above example for your mod topic, remember to
change "superspecial" to the name of your mod.

### Subject

The subject of topic must be in one of these formats:

* [Mod] Mod Title [modname]
* [Mod] Mod Title [version number] [modname]

For example:
* [Mod] More Blox [0.1] [moreblox]

This is what the forum topic for the example mod, superspecial, might
appear once complete:

<figure>
    <img src="{{ page.root }}//static/releasing_profit.png" alt="Profit">
    <figcaption style="display:none;">
        Profit
    </figcaption>
</figure>

## Appendix: Readme and Forum Generator

<noscript>
    <p>Javascript is required for this section!</p>
</noscript>

Title: <input id="t_title" value="My Super Special Mod"><br />
Modname: <input id="t_name" value="superspecial"><br />
Description: <input id="t_desc" value="Adds magic, rainbows and other special things."><br />
Version: <input id="t_version" value="1.1"><br />
License: <input id="t_license" value="LGPL 2.1 or later"><br />
Dependencies: <input id="t_dep" value="default mod (found in minetest_game)"><br />
Download: <input id="t_download" value="http://example.com/download.zip"><br />
Additional:<br />
<textarea id="t_add">Report bugs or request help on the forum topic.</textarea><br />

<pre><code id="readme">My Super Special Mod
====================

Adds magic, rainbows and other special things.

Version: 1.1
License: LGPL 2.1 or later
Dependencies: default mod (found in minetest_game)

Report bugs or request help on the forum topic.

Installation
------------

Unzip the archive, rename the folder to superspecial and
place it in minetest/mods/

(  GNU/Linux: If you use a system-wide installation place
    it in ~/.minetest/mods/.  )

(  If you only want this to be used in a single world, place
    the folder in worldmods/ in your world directory.  )

For further information or help see:
http://wiki.minetest.com/wiki/Installing_Mods</code></pre>

<pre><code id="forum">Adds magic, rainbows and other special things.

[b]Version:[/b] 1.1
[b]License:[/b] LGPL 2.1 or later
[b]Dependencies:[/b] default mod (found in minetest_game)
[b]Download:[/b] http://example.com/download.zip

Report bugs or request help on the forum topic.

[h]Installation[/h]

Unzip the archive, rename the folder to superspecial and
place it in minetest/mods/

(  GNU/Linux: If you use a system-wide installation place
    it in ~/.minetest/mods/.  )

(  If you only want this to be used in a single world, place
    the folder in worldmods/ in your world directory.  )

For further information or help see:
http://wiki.minetest.com/wiki/Installing_Mods</code></pre>

<script src="http://blog.rubenwardy.com/static/jquery.min.js"></script>
<script>function regen() {
    var title = $("#t_title").val();
    var name = $("#t_name").val();
    var desc = $("#t_desc").val();
    var version = $("#t_version").val();
    var license = $("#t_license").val();
    var dep = $("#t_dep").val();
    var add = $("#t_add").val();

    var download = $("#t_download").val();

    {
        var res = ((title.length > 0) ? title : name) + "\n";
        var header_count = res.length - 1;
        for (var i = 0; i < header_count; i++) {
            res += "=";
        }
        res += "\n\n";

        res += desc + "\n\n";

        if (version != "") {
            res += "Version: " + version + "\n";
        }

        res += "License: " + license + "\n";
        res += "Dependencies: " + dep + "\n\n";

        if (add != "") {
            res += add + "\n\n";
        }

        res += "Installation\n------------\n\nUnzip the archive, rename the folder to ";
        res += name + " and\nplace it in minetest/mods/\n\n";

        res += "(  GNU/Linux: If you use a system-wide installation place\n" +
            "\tit in ~/.minetest/mods/.  )\n\n" +
            "(  If you only want this to be used in a single world, place\n" +
            "\tthe folder in worldmods/ in your world directory.  )\n\n" +
            "For further information or help see:\n" +
            "http://wiki.minetest.com/wiki/Installing_Mods\n";

        $("#readme").text(res);
    }

    {
        var res = desc + "\n\n";

        if (version != "") {
            res += "[b]Version:[/b] " + version + "\n";
        }

        res += "[b]License:[/b] " + license + "\n";
        res += "[b]Dependencies:[/b] " + dep + "\n";

        res += "[b]Download:[/b] " + download + "\n\n";

        if (add != "") {
            res += add + "\n\n";
        }

        res += "[h]Installation[/h]\n\nUnzip the archive, rename the folder to ";
        res += name + " and\nplace it in minetest/mods/\n\n";

        res += "(  GNU/Linux: If you use a system-wide installation place\n" +
            "\tit in ~/.minetest/mods/.  )\n\n" +
            "(  If you only want this to be used in a single world, place\n" +
            "\tthe folder in worldmods/ in your world directory.  )\n\n" +
            "For further information or help see:\n" +
            "http://wiki.minetest.com/wiki/Installing_Mods\n";

        $("#forum").text(res);
    }
}

$(function() {
    jQuery('input').on('input propertychange paste', regen);
    jQuery('textarea').on('input propertychange paste', regen);
});
</script>
