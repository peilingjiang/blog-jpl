---
author: "Peiling Jiang"
date: "2019-11-03"
title: The Way @ Runway
tags: ["IMA", "Fall19"]
categories: ["Project"]
type: posts
bookToc: true
---

{{< hint >}}
I spent most of my time this weekend working on [knowSound](https://blog.jpl.design/posts/machine-learning-for-the-arts/knowsound/), which I thought I might be able to finish training and bring into Runway by yesterday, while now I seriously doubt if I can finish it by the end of the semester. (2019.11.04)
{{< /hint >}}

## Way to Grasshopper

Not many news about how machine learning helps industrial design or product design has caught people's eyes. It might because of the difficulty of connecting old-fashioned modeling tools to latest ML models, or it's just because of the cooling-down of the whole industry as a result of the raise of the demanding UI/UX design. Runway, however, can at least solve the first problem.

Hence, for this week's small experiment, I decided to use Runway to feed data into Rhino's most famous plug-in - Grasshopper, to knock open the door between industrial design (my original field) and machine learning. This could also be a good kick-off of my undecided final project: **Machine Learning for Computational Design**.

Since data flowing through Grasshopper are only either numbers or `Rhino.Geometry` objects, which as far as I'm concerned none of Runway models could return right now, I decided to try with **Face-Landmarks**, which are supposed to return straight forward coordinates of key points around the face.

<img src="/machine-learning-arts/the-way-runway/script-overview.png" alt="Script Overview" width="100%">

Currently there're no nice and clean way to directly visit Runway from Grasshopper, which is also what I'd like to contribute to the [runwayml/RunwayML-for-Grasshopper](https://github.com/runwayml/RunwayML-for-Grasshopper) repository. So I need to make an HTTP request - just as in p5.js - but a little harder as Grasshopper wasn't originally designed for streaming data. I found a piece of C# code and tuned into the way that works best with Runway. (Actually, Grasshopper also supports Python scripts, but installing one `requests` package into Rhino's Python environment took me forever.)

After loading data [(sample data)](https://github.com/peilingjiang/ima-courses/blob/master/f19-ml-art/the-way-runway/sample_data.json), which is in JSON format, into Grasshopper with C# component, I pass it into another Python component, read point locations from it, and draw `Rhino.Geometry` with it. The script is now on [GitHub](https://github.com/peilingjiang/ima-courses/tree/master/f19-ml-art/the-way-runway).

<img src="/machine-learning-arts/the-way-runway/script.gif" alt="Script" width="100%">
<img src="/machine-learning-arts/the-way-runway/points.gif" alt="Points" width="100%">
(Above GIFs might take some time to load.)

## References

From this post I'll divide **References** that are related to topic and concept from **Technical References**, which is a composite of *how to* learning materials I came across during the process of accomplishing the final outcome documented in the posts.

1. [runwayml/RunwayML-for-Grasshopper](https://github.com/runwayml/RunwayML-for-Grasshopper) is waiting for its first PR!
1. [davisking/dlib](https://github.com/davisking/dlib)
2. [Machine Learning En Plein Air: Building accessible tools for artists](https://medium.com/runwayml/machine-learning-en-plein-air-building-accessible-tools-for-artists-87bfc7f99f6b)

## Technical References

1. [Crow Tutorial1: Neural Sensing and Control in Grasshopper](https://www.youtube.com/watch?v=LGsQh0UQ0SE)
2. [Basic HTTP request - Grasshopper Forum](https://www.grasshopper3d.com/forum/topics/basic-http-request)
3. [Install Python packages in Rhino - Grasshopper Forum](https://www.grasshopper3d.com/forum/topics/using-third-party-module-in-rhinopython?commentId=2985220%3AComment%3A818878)
4. [C# Guide](https://docs.microsoft.com/en-us/dotnet/csharp/)
5. [How to Parse JSON into a C# Object](https://www.codementor.io/andrewbuchan/how-to-parse-json-into-a-c-object-4ui1o0bx8)
6. [ghJSON](https://mathrioshka.ru/ghjson) (Grasshopper extra component)
7. [What Every Computer Scientist Should Know About Floating-Point Arithmetic](https://docs.oracle.com/cd/E19957-01/806-3568/ncg_goldberg.html)
