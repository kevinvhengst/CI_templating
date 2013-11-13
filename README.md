CI_templating
=============
I got this library through:
http://net.tutsplus.com/tutorials/php/an-introduction-to-views-templating-in-codeigniter/

All credit goes to them.

Using the Library
-------------
To start using our library, let’s create a template view, named default.php in application/views/templates,
and place the following HTML/PHP inside:

```
!DOCTYPE html>
<html>
 
   <head>
      <title><?php echo $title; ?></title>
   </head>
 
   <body>
    
      <h1>Default template</h1>
       
      <div class="wrapper">
          
         <?php echo $body; ?>
          
      </div>
       
   </body>
    
</html>
```

In this template, we reference two variables, $title and $body.
Recall that in our template files, $body serves as a placeholder for an embedded view.
We shall now make another view to be embedded inside this template. 
Create a new file named content.php in application/views/ and place this simple HTML inside:
```
<p>
   Hello world!
</p>
```

We are now ready to load the templated page view from within a controller.
Inside any controller method, place the following code to display the content view, within the default template.

```
$data = array(
 
   'title' => 'Title goes here',
    
);
 
$this->load->library('template');
$this->template->load('default', 'content', $data);
```

Note: the library has to be loaded in before you can call the load method. To save yourself loading the library every time a template view needs to be displayed,
autoload the class by adding it to the array of libraries in application/config/autoload.php.
If instead of a view file, you want a string to be embedded in the template, simply assign the string to the $data array using the key body, and pass null as the second parameter in the load call.

```
$data = array(
 
   'title' => 'Title goes here',
   'body'   => 'The string to be embedded here!'
    
);
 
$this->template->load('default', null, $data);
```

Quick Tip
-------------
I’ve found that grouping view files in folders by the controller, and even method, they belong to, really helps keep my views organized & easy to locate.
Organizing your views in this way results in the directory structure closely following the URL schema of controller/method.
For example, say your project has a controller named Members, containing method list.
An appropriate location for the list view file would be in application/views/members, or application/views/members/list, if this method loads multiple views.
This view could then be embedded into a template using our library with the following code:

```
$this->template->load('template_name', 'members/list');
```
