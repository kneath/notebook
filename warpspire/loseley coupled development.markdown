Loosely coupled development

One of the biggest lessons when learning how to build rich interfaces is the idea of building loosely coupled components -- components which are dumb and do not know much about their surroundings. They can carry on life by themselves and only respond to signals from the outside (usually events).  But this idea of losely coupled components also works beautifully for development.  This was one of the ideas I was hinting at with my piece on HAML.

## Starting at the frontend

Since the birth of the semantic web, I've been a big proponent of the idea of separation of style from structure and unobtrusive scripting. Your HTML should be dumb. It knows really only of it's structure.  CSS broadcasts style. Unobtrusive Javascript broadcasts functionality.  Coupled together they produce amazing results.

This loosely coupled structure allows each portion to be used indenpendently, shared, swapped out, and worked on independently.

## Moving to the backend

MVC is a great pattern that everyone should be familiar with.  MVC is loosely coupled to some extent.  Work in the view should not know whether your model is pulling data from a mysql database, a postgres database, an xml file, or a json feed hosted on a remote website.  Your view  is dumb. Your model cares not care whether you're outputting JSON or a dynamically rendered JPG.

Again, this loosely coupled structure allows each portion to be used independently, shared, swapped out and worked on independently.

## Moving to the management

There's a new layer here that people often forget about: managing the development of projects.  This is the idea of loosely coupled development.  To do this, you just make each portion of production dumb.  The copywriters should be dumb about what font is being used. They work in their own domain: Text. The graphic designers should be dumb about what backend technology you're making. They work in their domain: Photoshop (or similar).  The front end developers should be dumb about what database you're using. They work in their domain: HTML, CSS & Javascript. The backend developers should be dumb about what pictures are being used. They work in their domain: code.

Efficiency increases as each portion knows less about the other portion. When your copywriters deliver their copy in text files (say, instead of delivering them as XPS files), it makes the front-end developers happy. This makes it much easier to get new project members up to speed -- no new systems (copywriter systems) are introduced.  Remove interlocking parts.

