##Install Gladys

Gladys is built to run on Linux, Windows or Mac. For more home automation interactions, use a Raspberry Pi.

#### Raspbian ISO

A packaged version of Gladys specially built for Raspberry Pi will be available soon.

#### Manual installation

To install Gladys, you just need to follow the instructions on [GitHub](https://github.com/GladysProject/Gladys).

## Developer program

#### Scripts

Everyone can write scripts for Gladys, that's very easy :

* Connect to Gladys, and go to the "script" panel on the dashboard.
* Select a script to edit.
* Write code, **what you want**, in JavaScript. (You can use Gladys function of course)
* Click on "Execute the script" to test it.

**API Gladys :** To know the list of available functions, you can go to the `api/services` folder. All the files in this folder are accessible, and you can use the function defined in these files like this : `file_name.function_name()`. For example, for the file `api/services/SpeakService.js`, if I want to call the function `say()`, I can simply call :

```
SpeakService.say("Hi !");
```


#### Modules

A Gladys module is just a sails.js hooks ( [More informations about Hooks](https://github.com/balderdashy/sails-docs/blob/master/concepts/extending-sails/Hooks/userhooks.md) ).

To show you an example, I've developed an "ExampleHooks" in the `api/hooks` folder. 

When Gladys start, this module does a lot of things :

* All files in `assets` are pasted in the `assets` folder of Gladys to be accessible everywhere.
* Models, Controllers, Services, Policies and config files are injected into Gladys.
* Widgets of the Home screen are defined in the `example/lib/parametres.js` file and are injected in the `DashboardBox` table in the database in order to be displayed on the dashboard.


**Example :**

Imagine you want to create a module to control your lamp.

* Duplicate the `api/hooks/example` folder to start from an existing module.
* Modify the `your_module/lib/defaults.js` file, and the `your_module/lib/parametres.js` file with the informations about your module.
* Create a sails Models in the `your_module/models` folder to create a table in the database for your lamps.
* Create a controller and build a REST API to Create/Read/Delete/Update a lamp.
* Modify the HTML code of the widget in the `your_module/views/box.ejs` folder. ( add buttons to control your lamps for this example )
* Create in the `assets` folder a JavaScript client ( an Angular App, or Jquery, or in pur JS as you want ) who will listen to click on button on the widget, and tell the lamp to turn on.


To make your tests, you can put some code in the `index.js` file, it will be executed when Gladys start. If you want Gladys to be fully ready, whait for the "sailsReady" event in the `index.js` file :

```
sails.config.Event.on('sailsReady', function(){
     // Will be executed when Gladys is ready, all models loaded,...
}); 
```

A more precise documentation will be edited soon !

#### Gladys Store

Gladys Store is coming for this new version !