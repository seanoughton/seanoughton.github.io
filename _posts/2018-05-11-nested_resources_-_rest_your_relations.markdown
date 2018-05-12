---
layout: post
title:      "Nested Resources - REST your Relations"
date:       2018-05-12 00:29:57 +0000
permalink:  nested_resources_-_rest_your_relations
---



## Why Nested Resources
Why you ask … why use Nested Resources?  The reason is REST and Relations.

You use **Rails Nested Resources** when you need to create/edit instances based on how they relate to each other and you want to do it in a **REST**ful way.  In other words, you use this technique when you have a **has_many** and **belongs_to** relationship and  you want to create the item that belongs_to in a form that is related to the parent.


## Nature of the Parent/Child relationship in an application
In the **parent/child relationship**, the child only really exists in relation to the parent.  You could create the child on it’s own, but it would have no relationship to it’s parent.  A child’s meaning, comes from its relationship to its parent, therefore, it's often best to create the child and immediately establish its relationship to its parent.

In order to do that effectively, you need to create models, views, routes and controllers that accomplish this, with as little code as possible and that follow **REST**ful conventions.  This is where Rails Nested Resources comes in to play.


## Do what’s best for the User and be RESTful
In real world scenarios, when you want to create a new Child and immediately relate it to a parent, you would want to do this from the Parent’s show page.  This not only takes advantage of the model relationships, but also makes sense from a User's perspective.

The Parent’s show page, gives you specific info about a particular Parent.  So that when you want to create new children of that Parent, the user doesn’t want to go to a different url, create the child then go back to the Parent’s page and add that Child from a list.  The user wants to be able to create or add a child directly in the Parent’s show page.

In order to do this, you need a form that will know about the parent and the child, collect and send the appropriate data, and be routed to the correct controller in order to process that data.  

You could manually create those routes and controllers, crafting new routes for creating a child through a parent and specific controllers that create a child and associate it with a parent at the same time.  However, this might not follow **REST**ful conventions. 

In order to maintain **REST**, you need to create and use URL’S/routes that mirror the relationship between parent and child. Rails provides a great way to simplify and streamline this process, by allowing you to take advantage of the Parent/Child relationship set up by ActiveRecord in the models.  

**Nested Resources** allows the Parent/Child relationship in the models to carry over to the routes. 

## How does Nested Resources work?
**Nested Resources** bases it’s logic on the Model relationships set up by ActiveRecord.  Then it sets up Routes and URL helpers to mirror the Model relationships.

## The Models
In the models, ActiveRecord gives us the ability to associate how the models will relate to each other, mirroring the database schema.  A Parent **has_many** children, and a child **belongs_to** a parent. 

This ActiveRecord designation gives us a bunch of methods for interacting with our models and objects that take advantage of the Parent/Child relationship.  

## The Routes
Rails gives us a lot of great routing tools as well.  These tools not only point the route to the appropriate controller, but also gives us URL helpers that we can use in the views and the routes, to generate dynamic urls that are linked to the models.  

Because the routes are linked to the models, they are also linked to how the models relate to each other.  So the routes not only know about the Parent/Child relationship, they can take advantage of it.  

You can simplify your routes and controller actions by taking advantage of the relationships set up in the model through ActiveRecord. You can do this by setting up Nested Resources in your routes.

A Nested Resource in the routes.rb file looks something like this:

* resources :parents do
         resources :children
* end

By adding the do...end we can pass it a block of its nested routes.

### This does two main things:
#### Creates URL helpers
Rails provides named helpers for our nested routes.  

Because we can use Dynamic Routes, the routes for our Parent/Child relationship would be:

* parent/:id/children  - **all of the parents children**
* parent/:id/children/1 - **one of the parents children**
 
The URL helpers are:

**all of the parents children:** parent_children(parent_id) or parent_children_path(@parent). 

This routes to children#create, so that the form data can be used to create a child.  The params id will have the parent_id in it.

**a single child for a parent:**
parent_child(parent_id, child_id).

#### Routing
Nested Resources creates a route: **children#create**.

This means that when you have a form on your Parent’s show page for the creation of a child, that form will route to the ChildrenController's  create action.

Instead of having to handcraft those routes and controller actions, you can use nested resources to create the routes and the wire up the correct controller actions.

## The Controller

For the controllers, you don’t need to add any new actions, you just need to modify the existing actions for the creation and editing of the Child.

#### Create/Edit
In order for these already existing routes to be able to create a Child and then associate it to a Parent, the routes need to know who the Parent is … they need to know the parent_id.  

Nested Resources takes care of that by separating the Child id from the Parents id.  Rails takes the parent resource's name and appends _id to it.  

The child’s id comes through as params[:id] and the Parent’s id comes through as params[:parent_id]. Then in the create/edit controller actions, you can use the Parent id to associate the child to the parent.

The controller needs to know whether the child to create has a parent specified or not, so you have to add some logic to the controller action to test if there is a parent_id, and if that parent actually exists, before you try and associate the child to the parent.

#### Index

The Children Index action needs to know whether or not the user wants to see an individual Parent’s Children or all of the Children.  

You have to add some conditional logic to the children#index action to account for this, looking for and testing the parent_id. 

The conditional hinges on whether there's an :parent_id key in the params hash — in other words, whether the user navigated to /parents/:id/children or simply /children.   

## The View

How does this translate to the views?  

You want to be able to have a form in the parents show view, that will be able to create a child.  In order for that to happen, the form has to know about the parent and the child, and has to send the form data, the params, to the appropriate controller.  The params has to have the parent_id, and the fields necessary to create the child.

The form knows about the Parent and the Child, because the Parent’s show controller sends that data through to the view through instance variables @parent & @child.  The @parent is whoever the current parent is, and the @child is currently a new Child with no attributes.  The attributes for this child will be created through the form.

Since the form has access to both the @parent and the @child, and because of the magic of Nested Resources the form can be written like this.

* form_for([@parent, @child]) do |f|
    	f.text_field :name
* end

What this means is that we are creating a form for a Child(@child) who is associated with this particular Parent(@parent).  @child is the main resource of the form, it is the resource that the form builders (f.) will be referring to. 

## Conclusion
Nested Resources continues on the logic of Rails created with Active Record, using the Model relations to help create logical and RESTful implementations of User Form data.










