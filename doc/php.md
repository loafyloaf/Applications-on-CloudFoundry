## Deploy a sample PHP app
### Technology involved:
* [PHP](https://secure.php.net/) 5.9 or later.
* A text editor — preferably one with PHP syntax highlighting, such as
[Sublime Text](http://www.sublimetext.com/) (available in a free trial version)
or an open source editor such as [Atom](https://atom.io/).

### Steps:
#### 1. [Download the code](http://www.ibm.com/developerworks/apps/download/index.jsp?contentid=1015413&filename=phptutorial-code-0728.zip&method=http&locale=)
for the sample PHP, phptutorial-code-0728.zip

Save phptutorial-code-0728.zip to your computer and extract its contents, which consists of the following files and directories:
* **index.php**, the main program, routes incoming requests to one of the templates in the views directory.
* **vars.php** contains variables used in this PHP project. One variable contains the text for the website's title.
* **views** is a directory that contains four templates — .tpl files — for the pages that constitute the app. Each template file can contain dynamic elements that are rendered on-the-fly with incoming requests.
* **static** is a directory that contains all the static assets of the app, which can include CSS, images, and client-side JavaScript code that runs on the browser.

#### 2. Deploy the app to Bluemix

This app, like most PHP web apps, can be deployed immediately to Bluemix with no additional modification or configuration. To deploy it now to Bluemix:
If you're not already logged in to Bluemix, run these commands from your OS command prompt to log in:
<pre>    	
cf api https://api.ng.bluemix.net/
cf login
</pre>
Upload the app to Bluemix by running the command:
<pre>
cf push your app name
</pre>
The name you choose for your application must be unique on Bluemix — not used by any other Bluemix user. You'll get an error if the name (called a route) is taken.

The command that you just ran:
* Uploads the app to Bluemix
* Runs the Cloud Foundry buildpack for PHP on Bluemix
* Starts an Apache web server instance, with PHP and your app loaded, on Bluemix
* Maps a route to your running app, enabling the app to be accessed over the Internet at the URL **https://<b><i>your app name</i></b>.mybluemix.net/**

Open **https://<b><i>your app name</i></b>.mybluemix.net/** in your browser to try out the app — a simple web store called Lauren's Lovely Landscapes. The store currently sells three prints; each print's page displays the associated name, image, and price.

#### 3. Examine the code structure
Starting with the next step, you'll begin to examine and modify the code. A syntax-highlighting editor with multiple-tabs support makes it much easier to work with the multiple PHP and template source code files.

Each web request for a page of the Lauren's Lovely Landscapes store is routed by your code to one of the templates. When routing to the template, your code attaches a PHP variable named $site_title that contains website title information. Each template uses this object to render its title (Lauren's Lovely Landscapes).

In index.php, you can see the code that routes requests to a template, together with a variable containing the title from the $site_title object:
```
$lll_route = trim("$_SERVER[REQUEST_URI]", "/");
 
if (file_exists("views/$lll_route.tpl")) {
    ob_start();
    require_once("views/$lll_route.tpl");
    $lllpage = ob_get_contents();
    ob_end_clean();
 
    echo $lllpage;
 
} elseif ...
```
In this case, the code first extracts the base name of the view from the URI and loads it into the $lll_route variable. Then it checks for the existence of a template file that matches the route name (alaska, say) and contains the .tpl file extension (alaska.tpl) — under the views subdirectory (views/alaska.tpl).

If the .tpl file exists, the contents are read into the output buffer and stored in the $lllpage variable. Reading the file into the output buffer enables index.php to process the PHP code in the template file. Once the HTML page with the processed PHP code is loaded into a variable ($lllpage), it can then be sent to the browser with the echo command.

If you examine one of the templates — alaska.tpl, for example — you can see the use of the $site_title PHP template variable to render the title:
```
<head>
    <title> <?php echo $site_title; ?> </title>
...
```

#### 4. Run the app with the built-in server

As of PHP version 5.4.0, an internal web server is included with every PHP install. This minimal server makes coding, testing, and demonstration of PHP apps considerably simpler. You no longer have to set up and configure an Apache or Ngnix server just to code in PHP.

You're now ready to run the app locally on your computer:
* At the root directory of your app, run:
```
php -S localhost:8000
```
* Point a browser to the local server at http://localhost:8000/.
* Try out this instance of the application and see if you notice any difference from the Bluemix-hosted one. Because you're looking at the same app, produced with the same code, there should be no noticeable differences between the two.

#### 5. Modify the code and rerun the app

In this step, you'll modify the price of a print and see it updated on the locally running website right away.

* In your text editor, open up the antarctica.tpl file and look for the price in the source code.
* Change the price from 100.00 to 80.00 and save the file. The changed line should look like:
```
    <div id="price">80.00</div>
```
* Run the app locally again:
```
    php -S localhost:8000
```
* Point a browser to the PHP server.
* Select the Antarctica print and note the print's changed price.

#### 6. Deploy the changed code to Bluemix

To let everyone on the Internet know about the Antarctica print's new price, you'll deploy the changed app to Bluemix.

Tip: You can also specify how much memory Bluemix should allocate to your app. For example, to set 128 megabytes of memory, use:
`cf push -m 128M your app name`

In Step 2, you saw how simple it is to deploy a PHP program to Bluemix. Again, run this command from the root directory of your code:
<pre>
cf push your app name
</pre>
After successful deployment, try out the app by pointing any web browser to:
**https://<b><i>your app name</i></b>.mybluemix.net/
