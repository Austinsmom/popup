# Custom jQuery Popup Object

This is a highly funcitonal JavaScript popup object. You can make as many named popups as you want, all with different data. Each popup can be opened and closed as is needed.  The popup can be used to simply display information, to force a page refresh, or to submit a form. jQuery is required for this to work.

## Basic Setup

To use the popup, you need to link to the style sheet in the head of the document:
```html
	<link type="text/css" rel="stylesheet" href="css/popup.css" />
```

You also need to add the JavaScript:
```html
	<script type="text/javascript" src="//code.jquery.com/jquery-1.11.3.min.js"></script>
	<script type="text/javascript" src="js/popup.js"></script>
```

## Configuration

To configure the each popup, you need to pass it an object variable. This should be constructed like so (explination of each option is below) (not every flag is required):

```javascript
var config = {
	title: "My Title",
	message: "Some message. <em>HTML</em> can be included, and will be treated as such.",
	buttons: ['yes', 'no'],
	buttonActn: [
					[{
						name: "submit",
						value: "true"
					}],
					[{
						name: "submit",
						value: "false"
					}]
				],
	url: "www.example.com/",
	method: "post",
	class: "myClass",
	reload: false
};
```

## Configuration Explaination

| Option | Required | Type | Function |
| -------------------- | -------- | ---- | -------- |
| title | yes | string | Text to be displayed on in the header section of the popup. |
| message | yes | string | The main body of the popup.  It can include HTML if you want to specify paragraphs or special text |
| buttons | yes | array | An array of button text, at least one is required (i.e. ['ok']). One button per array item will be created |
| buttonActn | no | 2D array of objects | Each button is wrapped in a form. If you want to add values to the buttons this is where you do it. The values will be in the form of hidden inputs with names and values. The the inner array at index[0] (the first one) will be applied to the button at index[0] of the buttons array. The inner array at index[1] will be applied to the button at index[1] of the buttons array, and so on. The inner arrays should contain objects with a name, and a value. If you put more than one object per array, then the corresponding button will have multiple hidden inputs. Clicking a button will close the popup regardless of what else it does. In the above example each button will have a single hidden input hidden to it. If this option is set, the number of inner arrays needs to match the number of buttons. |
| url | no | url string | The web address where the button forms will be submitted to (required if button action is provided). |
| method | no | string | 'get' or 'post' - The method you want to use to submit the button forms (defaults to get). |
| class | no | string | A class name that is attached to the overlay of the popup. Used to specify custom styles, or for targeting a specific popup with javascript. |
| reload | no | boolean | If set to true, the page will refresh when the popup is closed. If this is set to true, the button action and url will be ignored. |


## Create Popup

To create your popup object you simply need to create a variable, call the constructor function, and pass it the configuration variable. This is an example of a very simple popup:

```javascript
var config = {
	title: "My First Popup",
	message: "I just created a custom javascript popup!",
	buttons: ['neat!']
};

var myPopup = new Popup(config);
```

## Popup Methods

Each popup has an open and a close method that you can use to display the popup, and to remove it from the dom (clicking any of the buttons also calls the close method, so you don't have to do this separately):

```javascript
myPopup.open();

//or

myPopup.close();
