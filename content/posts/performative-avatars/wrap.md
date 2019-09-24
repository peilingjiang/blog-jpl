---
author: "Peiling Jiang"
date: "2019-09-23"
title: Wrap
tags: ["IMA", "Fall19"]
categories: ["Reading"]
type: posts
bookToc: true
---

## Remesh

Now it's time to wrap the scanned model to eliminate broken or undetailed parts.

<img src="/performative-avatar/wrap/wrap_process.gif" alt="Wrap process" width="100%">

Using Wrap3 and a base mesh, I re-meshed my scanned model and made it closed, less polygon and control points, and detailed in terms of hands and face. However, a few things didn't go very well.

1. **Feet**. I was scanned with my shoes on while the base model has bare feet. What would happen (and happened) is that if I didn't select foot parts as isolated polygon (and the scanned model would be more important during morphing), the feet and fingers would turn into strange squeezed shape with separated tips still there. Alternatively, if I selected feet, the front part of it, I would get a half-foot-half-shoe model, with black fabric texture and a Nike logo on it. Finally, I chose to have a logo on my feet.<br><br>
<img src="/performative-avatar/wrap/feet.png" alt="Feet" width="500rem">

2. **Eye**. My eyes became weirdly big after the morph. It's probably because I just added morphing alignment points on eye corners but not eye lashes.

3. **Clothes**. All clothes are mixed with my body, blended to each other. And gradient colors are like those in Adobe Fuse.

## Animate

Then I used Adobe Mixamo to add skeleton and animation to the model.

<img src="/performative-avatar/wrap/animation.gif" alt="Model Animation" width="100%">

I chose many different ones including ***Capoeira***, ***Stop jumping***, ***Sitting*** (with shaking legs), ***Illegal elbow punch***, and ***Strafe***. Mixamo skeleton works very well with the remeshed model with even just 8 markers (chin, wrists, elbows, knees, and groin) for auto-rigging.

## Questions

1. Is our gender selection in digital sphere the true reflection of our self-identity?<br>
We might think that we intend to create or choose digital Avatars that can realize our ideal self, which could better represent our self-identities. However, according to [this survey](http://www.nickyee.com/daedalus/archives/000431.php), only a portion of players claimed that their Avatars are idealized version of themselves. Could other reasons affect our choices of our own Avatars?

2. We cannot deny that the identity (and life, body or face) of most internet famous people are objectified and sold on the internet. But what's the moment that the objectification happen？ Is it when they bake their posts based on advertisement requirements? Or is it when they worried about fans and the public reactions? If exhaustedly caring about public criticism a part of objectification, are we all objectifying ourselves when we post - what we basically just bake for people to see and appreciate - on social media?

## Related Readings

Avatars & Gender

1. [Men Are Working Out Their Issues By Playing As Their Lovers and Exes in RPGs](https://www.vice.com/en_us/article/gv5583/men-are-working-out-their-issues-by-playing-as-their-lovers-and-exes-in-rpgs)
2. [How Video Game Breasts Are Made](https://kotaku.com/how-video-game-breasts-are-made-and-why-they-can-go-so-1687753475)
3. [Dealing With Harassment in VR](http://uploadvr.com/dealing-with-harassment-in-vr/)
4. [How Video Game Avatars Can Help Trans Kids Cope](https://play.acast.com/s/viceguide/379afc7e-b299-4d19-b62d-b293824ee850)
