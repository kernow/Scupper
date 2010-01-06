Scupper
=======

Scupper is a JavaScript library that helps you work with HTML in your test environment. It lets you define html snippets in your HTML file, then sweeps them out of the way so they don't pollute your environment with unneeded HTML. Scupper then allows you to easily retrieve a snippet and insert it into a test dom element when you need it. Scupper relies on [jquery](http://jquery.com) so this must be included (switching scupper to use another library would be trivial).

Usage
-----

Using Scupper is really easy, include scupper.js in your test suite html file then create the html snippets you want to work with:

    <div id="snippets">
    
      <div id="unordered_list_snippet">
        <ul id="some_unique_id">
          <li>this is something we want to work with</li>
        </ul>
      </div>
    
      <div id="paragraph_snippet">
        <p id="some_cool_paragraph">A paragraph with a <a href="http://google.com">link in it</a></p>
      </div>
      
    </div>
    
We then tell Scupper to suck up all of our wonderful snippets and remove them from the dom by calling init after the dom has loaded and passing the id of the element storing our snippets:

    $(document).ready(function() {
      Scupper.init('snippets');
    });

Scupper's now ready to use in our test suite, let's grab the unordered list snippet and insert it into the dom_test element:

    Scupper.insert_into('unordered_list_snippet', 'dom_test');
    
This would make our dom_test element look like this:

    <div id="dom_test">
      <ul id="some_unique_id">
        <li>this is something we want to work with</li>
      </ul>
    </div>

Thats it, we now have our test snippet in the dom ready for use in a test. Note how the `<div id="unordered_list_snippet">` html is not included in the dom_test element as this is just a container for our snippet and should not be part of the tested code.

If you only want the raw html and don't want to insert the snippet into the dom:

    Scupper.retrieve('paragraph_snippet');

This can be useful for comparisons when you want to check one string of html against another.

License
-------

Scupper is distributed under the [MIT license](http://www.opensource.org/licenses/mit-license.php)
