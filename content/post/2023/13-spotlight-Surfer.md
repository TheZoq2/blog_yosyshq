---
title: "Community Spotlight - Surfer"
date: 1970-01-01T13:26:31+01:00
image: /static-2023/spotlight/surfer.png
tags: ["community spotlight"]
---

# Surfer

Welcome to another [community spotlight](/tags/community-spotlight/) article where we shine a light on open source EDA projects. If you want to [submit a project, please do so here](https://docs.google.com/forms/d/e/1FAIpQLSdIEgu6FJZam0-V3PMTjw-eDebJdg_JuIlN4MkLNDr4vs-a5A/viewform?usp=sf_link).

Surfer is a new waveform viewer with a focus on extensibility and a snappy
(optionally keyboard driven UI). It is written in rust and while it is still in
its early stages, it is usable as a day-to-day wave viewer.

# Frans Skarman's Bio

I am a 4th year PhD student at the department of electrical engineering at
Linköping university in Sweden. I'm originally a software person, who started off in game development and then descending lower and lower in the tech stack until I reached reached this wonderful world of hardware. The whole time, i've been most interested in writing tools: initially game engines instead of games, and now compilers instead of hardware design. My main project these days is https://spade-lang.org/ a hardware description language inspired by modern software languages.

Outside of programming I enjoy some 3d printing, playing flight simulators, as well as sailing or skiing when the weather permits.

<!-- TODO IMAGE -->


# What motivated you to make Surfer?

When building my HDL, Spade, I ran into a problem. With a powerful type system,
the bit representation of a signal is often hard to understand, so you need a
way to automatically translate the values back into their human-readable
representation to effectively debug your designs. While `gtkwave` has support
for custom translation via external programs, it turned out to be quite hard to
get right and wasn't as powerful as I wanted. For example, I found no way to
translate a value into a list of expandable sub-fields to, for example, expand
individual fields of a struct.

# What makes you excited about Surfer?



## Web assembly

Perhaps my favorite thing about Surfer right now is that it works almost
flawlessly in web assembly. You can see a demo of that at
[https://app.surfer-project.org](https://app.surfer-project.org), and if you
have a VCD file to analyze, you can just append that to the URL, for example
<!-- TODO -->.

Apart from being a cool tech demo, this also enables some cool workflow in
CI/CD. For example, we can <!-- have if we end up doing this before the blog
release --> augment the tinytapeout test action to link to surfer with the
resulting waveform. No longer will you have to re-run your tests locally, or
manually download a VCD file to view it in a desktop viewer.

I'm also very happy that going from idea to implementation of the web version
took less than a day thanks to the rich rust ecosystem around web assembly.

## Signal translation

As I mentioned earlier, a big motivator for building surfer was being able to
get richer translation of Spade types. Even though I had a hacky system for
doing that in gtkwave, the Surfer version where you can expand or collapse
structs, view individual enum variants and translate sub-fields as you please
is a game changer.

I have also done my best to build this translation system to be decoupled from
Spade, meaning that anyone could add translation for their own HDLs constructs,
or perhaps something completely different, like a Risc-V opcode translator. All that
is needed for that is to implement a [few methods in a trait](https://gitlab.com/surfer-project/surfer/-/blob/main/src/translation/mod.rs?ref_type=heads#L290)

## Keyboard based UI

As a vim user, I hate reaching for my mouse so we've put quite a bit of effort
into making surfer usable with just the keyboard. There are some keybindings
for normal navigation of course, but most of the happens via a fuzzy matching
based command palette, similar to ctrl-p in Visual Studio Code.


<!-- TODO: Demo video -->


# Why do you make open source tools?


# What are some challenges?

The biggest challenge in my mind is in UI design. I'm not a UI designer, I only
took a single course on it in my bachelor, so most of the time I'm just winging
it. For features I use myself, I at least have some idea of what I want, for
feature requests by others I might even have that.

There are also some technical hurdles, we currently rely on a VCD library for
loading waveforms, but there is no rust library for loading other wave formats
like `ghdw` or `fst` which we'd "need" for loading larger waveforms in a
reasonable time.

# What could the community do to support you?

First, give surfer a try. Let us know what you find nice and what could use
improvements. Especially as a non-UX person it is invaluable to get feedback
from users!

If you want to do more, consider contributing the features you think are
missing. This could be anything from tiny things like a button to zoom to fit
or a way to display the timescale, or larger things like support for
Chisel/spinal representations of values.

One of the great things about open source in my opinion is that anyone can
contribute and add their little feature that they want, or fix a small issue
that really bugs them. Long term, this makes open source projects feel very
complete, because it is likely that someone before you has already thought
about the little feature you're after. But in early stages of a project like
surfer, lots of little things will be missing and adding those things as a
small team takes a long time.


# What is the best link to give for the project?

If you want to learn more, see the [git repo](https://gitlab.com/surfer-project/surfer). You can also try Surfer right in your browser at https://app.surfer-project.org

# What is the best way for people to contact you?

* Email: [frans.skarman@liu.se](mailto:frans.skarman@liu.se)
* Mastodon: [TheZoq2@mastodon.social](https://mastodon.social/@thezoq2)
