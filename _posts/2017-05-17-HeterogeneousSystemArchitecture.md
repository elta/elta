---
layout: post
category: "linux"
description: ""
title:  "异构系统架构 “Heterogeneous System Architecture”"
date: 2017-05-17 14:04:37+00:00
tags: [Heterogeneous,hsa]
---

# What is Heterogeneous Computing
Heterogeneous computing refers to systems that use more than one kind of processor. These are multi-core systems that gain performance not just by adding cores, but also by incorporating specialized processing capabilities to handle particular tasks. Heterogeneous System Architecture (HSA) systems utilize multiple processor types (typically CPUs and GPUs), usually on the same silicon die, to give you the best of both worlds: GPU processing, apart from its well-known 3D graphics rendering capabilities, can also perform mathematically intensive computations on very large data sets, while CPUs can run the operating system and perform traditional serial tasks.

By the end of 2010, nearly all new desktop computers had multicore processors, with dual-core and even quad core processors entering the mainstream of affordable computing. Still, multicore processing posed some challenges of its own. The extra cores and cache memory required to fuel their instruction pipelines came at a cost of both increased processor size and, again, high power consumption.

Meanwhile, the multi-core era also saw some interesting developments in GPUs, which were growing in sophistication and complexity, spurred on by advances in semiconductor technology. GPUs have vector processing capabilities that enable them to perform parallel operations on very large sets of data – and to do it at much lower power consumption relative to the serial processing of similar data sets on CPUs. This is what allows GPUs to drive capabilities such as incredibly realistic, multiple display stereoscopic gaming. And while their value was initially derived from the ability to improve 3D graphics performance by offloading graphics from the CPU, they became increasingly attractive for more general purposes, such as addressing data parallel programming tasks.

The early efforts to leverage GPUs for general purpose computing coincided with a notable shift in consumer culture. There was a dramatic increase in the availability and quality of digital content, coupled with an increasing consumer appetite for rich visual experiences like video playback and viewing content in HD. At the same time, the emergence of mainstream operating system support for advanced multitasking began to require processing efficiency of an entirely new magnitude.

## Heterogeneous Era: Setting the Stage for a Fantastic Leap Forward

> And that’s why heterogeneous computing, which brings together the best of both CPUs and GPUs, is essential to driving faster and more powerful processor designs for new and better experiences.

The drive to improve performance and the continuing constraints on power and scalability in multi-core CPU development have led semiconductor, software and systems designers increasingly to look to the vector processing capabilities of GPUs.

Vector processors like those in advanced GPUs have up to thousands of individual compute cores, which can operate simultaneously. This makes GPUs ideally suited for computing tasks that deal with a combination of very large data sets and intensive numerical computation requirements.

(And GPUs are rapidly advancing to do even more for less.) But – and this is a very important “but” – vector processing isn’t the answer all the time. For example, small data arrays have overhead associated with setting up vector processing that can easily outweigh the time saved. That’s why the scalar approach used by CPUs is still best for certain problems and algorithms. And that’s why heterogeneous computing, which brings together the best of both CPUs and GPUs, is essential to driving faster and more powerful processor designs for new and better experiences.

What is Heterogeneous Computing - Beginning of a beautiful relationship

The possibilities created by heterogeneous computing are truly fantastic – from flawless HD videoconferencing to heretofore unimaginable display clarity to real-time language translation and interpretation – all in lower and lower power envelopes for smaller and smaller form factors with longer and longer battery life.

Heterogeneous systems leverage the data parallelism and power efficiency of today’s GPUs to usher in a new era of innovation in computing. They can take mainstream visual applications and elevate them to new levels, enable new pixel intensive experiences and even introduce non visual capabilities that were unimaginable – until now. So let’s take a moment to look at the many ways GPUs continue to propel advances in mainstream computing.

## Refining Everyday Experiences

What is Heterogeneous Computing - Slimming down for smaller form factors

What’s your idea of long battery life in a notebook computer or mobile device? Depending on what you’re doing – watching a feature length movie vs. just checking email, for example – you might say maybe three hours? Five? How about all day battery life? Real all day battery life.

The days of lugging along a second battery or scampering around an airport looking for AC power are ending, as heterogeneous computing sets a new standard for battery life in smaller packages, like today’s ultra-thin notebooks, netbooks and tablets. High-definition (HD) video is another area in which today’s GPUs may improve existing experiences. You’ve no doubt experienced both HD and standard-definition video – the former on HD equipment, and the latter on a non-HD system. But what if you didn’t need content originally captured in HD to have an HD-quality experience? Standard-definition sources may be viewed in near HD-quality through the hardware-accelerated upscaling of lower quality content –dynamically. So you’ll be able to access streamed movies on more devices or watch HD TV on a PC. Similarly, you won’t need the highest-end PC powerhouse for 3D gaming.

Today’s GPUs can enable ultra-high frame rates for realistic, immersive 3D gaming on mainstream (even entry level) notebook computers. They can also make it easy and cost-effective to add stereoscopic 3D realism to 2D content, from Hollywood movies to home video. At work, today’s GPUs can make both collaborative and independent work more productive. With support for flawless HD videoconference capabilities and new forms of virtual presence, GPUs make virtual meeting as close to meeting in person as it gets. They enable visual communications that were not even remotely possible before, like bidirectional HD video chats. They can also send desktop productivity soaring by making it easier and more seamless than before to move back and forth between applications on multiple monitors – even when working with graphics intensive content like PowerPoint presentations, product demos or simulations, and videos.

## Enabling New Pixel-Intensive Experiences

>Those are just a few of ways that heterogeneous computing could change the way people interact with computers forever.

The only thing more exciting than doing something better than you’ve ever done it is doing something entirely new. For example, what if you could log in to your computer just by looking at the screen? What if it could respond to just a gesture, not even need a touch, to know exactly what you want? And what if your HD video walkthrough of a new house could generate a 3D model of that space to see if your furniture could make that house your new home? Those are just a few of ways that heterogeneous computing could change the way people interact with computers forever. They’re also just three examples of the types of software innovations that are possible now with GPU application programming interfaces (APIs).

If you’re like most people, you probably find it hard to imagine something more mundane and time consuming than searching and categorizing your photos and videos based upon who is in them, where you were and what you were doing. But what if your computer could speed through by quickly and automatically finding and tagging photos and videos for you based on the faces, places or objects that are in the images? Or by helping you sort through photo libraries to eliminate duplicates saved under different names? Or by finding the IMDb or Wikipedia entry you’re looking for based on a “look” at an actor’s face? These are also pixel-intensive experiences made possible by today’s GPUs. And they’re enough to make current search and index capabilities seem almost unimaginably tedious and slow.

Today’s GPUs can also add measurably to the enjoyment of visual content in a number of new ways. Imagine a computer that enhances your shaky handheld video footage by automatically stabilizing HD content. Or one that delivers crystal clear content even on room-sized screens. Or that supports holographic imagery for unprecedented realism. We foresee display resolutions so high, they deliver density and clarity that rivals what the human eye can even perceive in the analog world. This is how technology improves our lives by getting out of the way.

## Creating New Non Visual Experiences

Chances are that when you think of new applications for GPUs, you’re likely to think of visual experiences. Facial and gesture recognition, photo or video indexing, and some of the others we’ve just described are good examples. That stands to reason, given that the “G” in GPU does stand for “graphics”. But as we have discussed, GPUs can do more than just push pixels to a display. They are very capable general purpose computing resources that can now stand side by side with the CPU and enable a broad range of compelling new experiences. For example, today’s GPUs enable a level of contextually aware computing that takes new experiences far outside the realm of the visual. We may not be at a point where “Computer: Earl Grey, hot” is going to be a reality anytime soon. But some of the very real possibilities are nearly as amazing.



In ambient computing – one term for contextually aware computing – massive amounts of data from multiple sensors enable a computer to adapt to user and situation, rather than the other way around. In the audio world, for example, consider the ever present lag in the time it takes to transcribe or translate live audio from one language to another during video conferencing, news broadcasting and similar scenarios. People have accepted this inconvenience for years, but ambient computing enabled by advanced data parallel processing capabilities of GPUs creates the potential for audio interpretation and voice translation to other languages immediately, in real time.

>This more contextually aware computing also opens the possibility for capabilities like speech recognition in audio recording applications…

This more contextually aware computing also opens the possibility for capabilities like speech recognition in audio recording applications – so that, for example, software will automatically determine who is speaking in a conference room and identify the different speakers in the auto-generated transcript of the conference. Another potential application is for software that will dynamically gauge the acoustics in a room and tweak output accordingly for whatever mobile device you’re using.

These kinds of audio applications translate into digital security as well – in, for example, systems that grant user access to physical locations and computer systems by recognizing and authenticating users based on voice. And while we’re on the subject of security, GPU capabilities could enable targeted malicious software scans that eliminate the painfully slow runtimes associated with today’s anti-virus programs.

These aren’t blue-sky speculations. Many of the capabilities exist today in labs all over the world. Why haven’t they found their way to the mainstream yet? The answer is in the limitations of existing hardware architecture and software programming models. And this is why heterogeneous systems architecture is vital to enabling the next era of computing innovation.

From：[[http://developer.amd.com/resources/heterogeneous-computing/what-is-heterogeneous-computing/]]