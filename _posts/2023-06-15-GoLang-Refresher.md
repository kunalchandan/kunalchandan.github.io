---
title: Golang Refresher
date: 2023-06-17 20:00:00
categories: [projects]
tags: [personal-projects]
author: kchandan
math: true
---

# Project Idea:

Getting a refresher on Go for my upcoming Tesla SRE interview. For this I want to incorporate a wide variety of applicable tasks that would be relevant in a SRE role and also hopefully learn something interesting along the way.

Here were some things that caught my eye.

- https://github.com/avelino/awesome-go#bit-packing-and-compression
- https://github.com/avelino/awesome-go#miscellaneous-data-structures-and-algorithms
- https://github.com/avelino/awesome-go#embeddable-scripting-languages
- https://github.com/avelino/awesome-go#functional
- https://github.com/avelino/awesome-go#game-development
- https://github.com/avelino/awesome-go#goroutines
- https://github.com/avelino/awesome-go#gui
- https://github.com/avelino/awesome-go#images
- https://github.com/avelino/awesome-go#machine-learning
- https://github.com/avelino/awesome-go#project-layout
- https://github.com/avelino/awesome-go#opengl
- https://github.com/avelino/awesome-go#science-and-data-analysis


- https://github.com/fogleman/gg

Ideas:
- Calculator
- Compiler
- DNA sequencing algorithm

# Problem Statement

DNA sequencing algorithm: Simulate the process of reading and assembling genetic sequences by aligning raw reads against reference genomes or de novo assembly.

I wanna do some de novo assembly of short sequences.
https://www.ncbi.nlm.nih.gov/nuccore/NC_045512

I can use the COVID 19 sequence as starter data rather than generating my own.

Now to do the actual multiple sequence alignment we will use Progressive Alignment Construction. This is based on Needleman-Wunsch, which will need to be implemented first.

To implement NW I will start with a single threaded basic implementation, and I would like to progress to a more complex multithreaded implementation that I can hand to the multiple go threads that I could summon. I'm not sure if the multithreaded approach would actually be faster, but that would be something worthwhile exploring since the actual calculation of the scoring is relatively simple.

For data visualization, I considered using gonum/plot, but the API didn't seem as straightforward as I was hoping for heatmaps, and I also wanted to show directions for the NW algo, so I will be writing my own visualizers with a 2D drawing library.

I may also need to switch off of WSL onto Windows because Pixel (the arbitrarily chosen library) does not work with WSL?

```
/usr/local/go/pkg/tool/linux_amd64/link: running gcc failed: exit status 1
/usr/bin/ld: cannot find -lXxf86vm: No such file or directory
collect2: error: ld returned 1 exit status
```

I think I'll try one other GUI library then switch off if required.

Just tried fyne and I hit the exact same issue. I think this might be something more inherent to Golang itself. I don't really want to switch off of WSL. :(

So now I'm just displaying things to the console.

```
Initializing scoring matrix
Scoring...
Drawing Score Matrix
     Ad  Th  Cy  Ad
Ad    0  -2  -4  -6
Th   -2   1  -1  -3
Cy   -4  -1   2   0
Gu   -6  -3   0   1
Drawing Direction Matrix
   Ad Th Cy Ad
Ad  \  -  -  -
Th  |  \  -  -
Cy  |  |  \  -
Gu  |  |  |  \
Sequences 1 and 2
atcg
atca
Alignment Scores
4
4
-------------------------
-------------------------
-------------------------
Initializing scoring matrix
Scoring...
Drawing Score Matrix
     Gu  Ad  Th  Th  Ad  Cy  Ad
Gu    0  -2  -4  -6  -8 -10 -12
Cy   -2  -1  -3  -5  -7  -7  -9
Ad   -4  -1  -2  -4  -4  -6  -6
Th   -6  -3   0  -1  -3  -5  -7
Gu   -8  -5  -2  -1  -2  -4  -6
Cy  -10  -7  -4  -3  -2  -1  -3
Gu  -12  -9  -6  -5  -4  -3  -2
Drawing Direction Matrix
   Gu Ad Th Th Ad Cy Ad
Gu  \  -  -  -  -  -  -
Cy  |  \  \  \  \  \  -
Ad  |  \  \  \  \  -  \
Th  |  |  \  \  -  \  \
Gu  |  |  |  \  \  \  \
Cy  |  |  |  \  \  \  -
Gu  |  |  |  \  \  \  \
Sequences 1 and 2
gcatgcg
gattaca
Alignment Scores
-9
-9
-------------------------
-------------------------
-------------------------
Initializing scoring matrix
Scoring...
Drawing Score Matrix
     Gu  Gu  Gu  Gu  Gu  Ad  Ad  Ad  Ad  Ad  Ad  Gu  Gu  Gu  Gu  Gu  Gu
Gu    0  -2  -4  -6  -8 -10 -12 -14 -16 -18 -20 -22 -24 -26 -28 -30 -32
Gu   -2   1  -1  -3  -5  -7  -9 -11 -13 -15 -17 -19 -21 -23 -25 -27 -29
Gu   -4  -1   2   0  -2  -4  -6  -8 -10 -12 -14 -16 -18 -20 -22 -24 -26
Gu   -6  -3   0   3   1  -1  -3  -5  -7  -9 -11 -13 -15 -17 -19 -21 -23
Gu   -8  -5  -2   1   4   2   0  -2  -4  -6  -8 -10 -12 -14 -16 -18 -20
Gu  -10  -7  -4  -1   2   3   1  -1  -3  -5  -7  -7  -9 -11 -13 -15 -17
Gu  -12  -9  -6  -3   0   1   2   0  -2  -4  -6  -6  -6  -8 -10 -12 -14
Gu  -14 -11  -8  -5  -2  -1   0   1  -1  -3  -5  -5  -5  -5  -7  -9 -11
Gu  -16 -13 -10  -7  -4  -3  -2  -1   0  -2  -4  -4  -4  -4  -4  -6  -8
Gu  -18 -15 -12  -9  -6  -5  -4  -3  -2  -1  -3  -3  -3  -3  -3  -3  -5
Gu  -20 -17 -14 -11  -8  -7  -6  -5  -4  -3  -2  -2  -2  -2  -2  -2  -2
Gu  -22 -19 -16 -13 -10  -9  -8  -7  -6  -5  -4  -1  -1  -1  -1  -1  -1
Gu  -24 -21 -18 -15 -12 -11 -10  -9  -8  -7  -6  -3   0   0   0   0   0
Gu  -26 -23 -20 -17 -14 -13 -12 -11 -10  -9  -8  -5  -2   1   1   1   1
Drawing Direction Matrix
   Gu Gu Gu Gu Gu Ad Ad Ad Ad Ad Ad Gu Gu Gu Gu Gu Gu
Gu  \  -  -  -  -  -  -  -  -  -  -  -  -  -  -  -  -
Gu  |  \  \  \  \  -  -  -  -  -  -  \  \  \  \  \  \
Gu  |  \  \  \  \  -  -  -  -  -  -  \  \  \  \  \  \
Gu  |  \  \  \  \  -  -  -  -  -  -  \  \  \  \  \  \
Gu  |  \  \  \  \  -  -  -  -  -  -  \  \  \  \  \  \
Gu  |  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \
Gu  |  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \
Gu  |  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \
Gu  |  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \
Gu  |  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \
Gu  |  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \
Gu  |  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \
Gu  |  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \
Gu  |  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \  \
Gap in left sequence
Gap in left sequence
Gap in left sequence
Sequences 1 and 2
ggggggggggggggggg
ggggg===aaagggggg
Alignment Scores
-11
-11
```