---
layout: post
title:  "Kicking off Refacer"
date:   2026-04-30 08:00:00 -0500
categories:
---

## The camera remembers everything. Sometimes that's dangerous.

A few years ago I was doing photojournalism work, covering protests. One thing stuck with me — how much effort people put into not being seen. Coverings, masks, hoods pulled up, turning away the moment a camera came out.

That’s not paranoia. That’s a rational response to a real risk. And it made me think: why is the burden of anonymity falling entirely on the subject?

This tension isn’t new. Gordon Parks — one of the greatest photojournalists who ever lived — called the camera his “weapon of choice.” He meant it as a tool of justice, a way to document the humanity of people that powerful institutions wanted to erase. In 1956, he went to Alabama to photograph Black families living under Jim Crow segregation for Life magazine. The work was extraordinary. It was also dangerous — Parks was followed, harassed, and warned he’d be tarred and feathered. He fled the state via a back road and took the first plane out of Birmingham at dawn.

And the people he photographed? After the story ran, the Causey family — one of the families Parks documented — was stripped of their possessions and driven from their home.

Parks used the camera as a weapon. But the photographs themselves became a weapon against the people in them.

That was 1956. There was no facial recognition. No GPS metadata. No way to cross- reference a face against a global database in seconds. The risk back then was a photo ending up in the wrong hands locally. Today, a single image can travel the world instantly, be run through recognition software, and geolocate exactly where it was taken — all before the photographer has even left the scene.

The stakes haven’t gotten smaller. They’ve compounded enormously. Because the images themselves still matter just as much as they did then. A photograph of a protest isn’t just documentation — it’s testimony. It captures energy, emotion, and humanity in a way that words rarely can. The story lives in those images. But so does the risk.

I had photos I wanted to share that told exactly that kind of story. I hesitated anyway. Not because they weren’t worth sharing, but because sharing them meant potentially
exposing people who had already gone to great lengths to protect themselves.

So I shelved those photos.

The question Refacer is trying to answer is simple: what if you didn’t have to choose? What if the story could be told and the people in it could be protected?

---
## So I'm building something about it

Refacer is a locally-run, fully offline desktop tool for photojournalists and activist photographers. It does two things:
 - Anonymizes faces in batches of photos using AI inpainting — replacing each detected face with a uniquely generated one that can’t be reversed or traced back
 - Strips all metadata — GPS, timestamps, camera serial numbers, all of it, gone

No cloud. No API calls. No images ever leave your machine. The whole point is that it
runs on your hardware, under your control.

---
## Why this specifically 

There are existing tools for this kind of thing, but they tend to fall into one of two camps — either they’re heavyweight enterprise software that costs money and requires technical setup, or they’re online services that ask you to upload sensitive photos to someone else’s server, which somewhat defeats the purpose.

Refacer is meant to be FOSS, portable, and dead simple to use. If a photojournalist in the field with a modest laptop can run it, that’s the bar.
---
## The tech 

Under the hood it’s a Python pipeline:

Face Detection → Face Swap → Enhancement/Compositing → Metadata Scrub

Each stage is modular and independent. Face detection uses InsightFace’s RetinaFace backend, which handles crowds, angles, and partial occlusion well. Inpainting uses LaMa, a lightweight model optimized for CPU inference — no GPU required. Metadata scrubbing uses exiftool, which is about as battle-tested as it gets for this kind of thing.
   
Crucially, inpainting is intentionally non-deterministic — no random seed, different output every run. This makes reversal attacks infeasible. You can’t work backwards from the output to reconstruct the original face.

The UI will be a simple Gradio interface running locally in your browser. Drop in a folder, hit Run, get anonymized photos out.
---
## What's next
Right now I’m in the early prototyping phase — validating that the composite quality is actually good enough before building the full pipeline around it. I’ll be documenting the whole build process here as I go, including the dead ends.

If this sounds useful to you — whether you’re a journalist, an activist, a researcher, or just someone who thinks this kind of tool should exist — follow along. And if you want to contribute when it’s open sourced, that door will be wide open.
