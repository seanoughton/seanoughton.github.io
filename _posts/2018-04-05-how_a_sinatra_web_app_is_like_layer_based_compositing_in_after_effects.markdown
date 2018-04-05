---
layout: post
title:      "**How a Sinatra Web App is like layer based Compositing in After Effects**"
date:       2018-04-05 23:18:41 +0000
permalink:  how_a_sinatra_web_app_is_like_layer_based_compositing_in_after_effects
---


Before beginning this journey of Web Development, I worked in Post Production for Agencies and Post Houses in the San Francisco Bay Area.  Throughout the course of this program, I have been making mental comparisons to how coding and Web Technologies mirror Post Production technologies and workflows.  In the Sinatra Section, this really became evident to me.  So here is a comparison of a Sinatra Web app to an After Effects Compositing workflow.

### How After Effects is similar to the Object model in Sinatra/ActiveRecord.

#### After Effects is basically composed of:
1. Compositions 
1. Layers
1. Effects/Transformations - (how you change the layers)
1. Rendering out the animations/videos

**Here is an image of an After Effects Composition**
![](http://orangestreetpost.com//blog-post-images/blog-post-5/After-Effects-layers.jpg)



**After Effects equates to Ruby/Sinatra/ActiveRecord like this:**

After Effect Compositions are like Ruby Classes that can create instances of that class
1. They have a Class Name, which is the Composition Name
1. They have attributes, which are the layers.
1. They can create instances of themselves through methods
           (the After Effects Method for creating instances is Render)
					 (it is like Composition.create)

Layers are individual attributes of the Composition Class

1. Layers allow the composition to hold data (shapes, videos, text, etc)
1. Layers are unique, you can duplicate them, but each layer has a unique id and has a unique effect on the Composition.
1. Layers can be **C**reated, **R**ead, **U**pdated, and **D**eleted

**Here is what an After Effects composition might look like if it were written as a Ruby class:**
![](http://orangestreetpost.com//blog-post-images/blog-post-5/MyFirstVFX_class_basic.png)


#### The has_many and belongs_to relationship in After Effects:

An After Effects Composition is usually just called a "Comp"

An After Effects Comp can have individual layers or it contain other Comps as layers.

A layer can only belong to one Comp and a Comp can have many individual layers.

A layer which is also Comp is called a **Nested Comp** or **PreComp**.

A  **PreComp** is just a Comp with a bunch of layers.
These Nested Comps are like a collection of objects in Ruby (an array or hash). 

The reason you create a Nested Comp in After Effects is to encapsulate layers that need to function together.  It makes working with those layers easier, because it isolates them from the other layers. It also means that you can use/reuse that Nested Comp in other Comps, rather than having to recreate those same layers in every Comp that needs them.

**Here is how that relationship of Comps to Nested Comps might be written in Ruby.**

![](http://orangestreetpost.com//blog-post-images/blog-post-5/MyFirstVFX_class_has_many.png)

![](http://orangestreetpost.com//blog-post-images/blog-post-5/NestedComp_class_belongs_to.png)

#### How using After Effects is similar to Nested Forms/Params Layers/Get/Post

**Forms** provide a way for a user to create and change instances of objects.

The form can be equated to the After Effects interface.  

The way the form is structured, specifically the way that the data being entered into the form is structured for data transfer, determines how the data will be processed by the application. 
Here is an example from our labs:


![](http://orangestreetpost.com//blog-post-images/blog-post-5/labs-params.png)


The way that this is similar to After Effects is that for a form’s params data to be able to be used effectively, it must know what object it wants to effect and which layer it wants to effect.

Similarly, in order for you to successfully change your After Effects Comp, you have to know which Comp you want to effect and which layer in that Comp you want to effect.

In After Effects, this is accomplished by choosing the correct layer and Comp in the application interface.  

With a Sinatra web app, it is accomplished by structuring the form data so that it can be used by the corresponding Class method, such as **create, update or find_by.**  

The way that the Ruby Models/Classes are set up determine, how you need to structure the data in the form in order for the objects to be created by the params hash.

![](http://orangestreetpost.com//blog-post-images/blog-post-5/Artist_class_has_many.png)
![](http://orangestreetpost.com//blog-post-images/blog-post-5/song_class_belongs_to.png)

The has_many, belongs to relationship and the many_to_many relationships must be established first, so that when the params hash is passed into the **.create method**, that method can appropriately parse the data, and then create the object.

**Here is a how the params data might be structured for an After Effects composition**

![](http://orangestreetpost.com//blog-post-images/blog-post-5/params_myfirstvfx.png)

In conclusion, I’d like to say that there are obvious differences between how a Sinatra Web App works and how After Effects works, but the basic structure of how the user interacts with the applications and the basics structure of the Class and Object relationships are similar.  And most importantly, writing this blog post has given me a deeper understanding of how a Sinatra Web App works




​



















