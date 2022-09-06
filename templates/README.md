# CasparCG HTML Template Examples

This folder contains one or more example templates designed for use with CasparCG graphics.

The templates are provided "as is" with no warrenty about their function. Using the templates is entirely at the users own risk.

To use a template, copy the html file and any associated files or folders to the CasparCG server folder configured for template replay. If using the standard client use the Library Refresh menu item to let the client discover the template which can then be instanced in the client rundown

## Example_01
This example template displays a simple static lower third with a solid red bar containing two lines of text. The content of the upper text row is set by key f0 sent by the client, the content of the lower row text is set by key f1 sent by the client. Both rows use Arial typeface as this should be availble on all computer system hosts.

To use the template in a CasparCG server copy the file into the server template folder. If a CasparCG client is already running when the file copy occurs, use the library refresh tool in the client to add the new template to the list of templates. The template can be instanced in a rundown, data entered for the f0 and f1 keys then run.

The template also runs in a browser, such as Chrome, by selecting the file in the finder list, right clicking the name and selecting the target program as Chrome browser. When the browser page shows as a blank display, right-click in the display area and choose Inspect which opens a second window that includes a Javascript console. Locate the console tab to make it the focus zone. Enter a command on the console similar to:

``` Javascript
play('{"f0": "My name shows here", "f1": "My job title shows here"}')
```

When entering the above command take great care with the placement of the single and double quotation marks. Some people find the data entry is simplified by using a command that uses the built-in function that converts a JSON object to stringified JSON form:

``` Javascript
play(JSON.stringify({f0:"CasparCG", f1:"Graphics made Cool"}))
```

Chrome was suggested as the browser, as this is closest to the embedded chromium browser used in CasparCG. Other browsers also work to show the template, but some error messages may be seen on the console display unless they are webkit based browsers.

The content update process is invoked in a similar fashion:

``` Javascript
update(JSON.stringify({f0:"CasparCG User Forum", f1:"https://casparcgforum.org/"}))
```

Finally the template can be removed by calling the stop function:

``` Javascript
stop()
```

This hides the text, and about 800 ms later closes the browser tab or window.

## Example_02
This example template displays a lower third caption with a name field, a job title/designator field, and an optional hashtag or email name all displayed over a semi-transparent strap. When the template is played it animates all elements onto the display. The animation actions use CSS animation methods coupled with Javascript promises that compute when the animations are complete. The properties of the strap are all defined as CSS variables to speed any design updates or maintenance requiring colour changes , size changes, or display typefaces.

The template requires a bitmap graphic which is stored in a sub-folder of the template folder. The sub-folder is called **_img** and the bitmap file is called **Vale_Viewpoints_44L.png**

Individual fields can be updated. The updated field data from the client is compared with the existing data. Only elements that have changed cause animations to occur.

When the template receives a stop request from the CasparCG client it animates all elements off the screen then closes the html window.

As with Example_01, the template can be run in a browser.

### Listing expected key names
It can be difficult for an operator or user to know what field names were used by the template creator. This template includes a special function that can display the field names. Once the template has been played, potentialy without any content, the function templatekeys(1) causes the names of the keys and a required bitmap to be shown. This overlay display can be removed by a second calll to templatekeys(1). The function can be invoked from the standard CasparCG client by entering the the function name in the Invoke field of the template item inspector, then pressing the F7 key to invoke the function.

### Template Debug Facilities
Several features are present just for testing and debugging the template.

Function ToggleBg() shows or hides a full frame still that enables the template display to be seen over the top of a representative background picture. The background picture is provided by the user as a bitmap called **GenericBgnd.jpg** stored in the same _img sub-folder as the programme icon bitmap. A second call to the function removes the background picture display.

Function DoPlay(*n*) simulates the action of playing the template in CasparCG server. The parameter *n* is an integer that selects one of several initial content displays for the template. A value of 0 provides short descriptions of the field content. Values starting at 1 are more representative of real content. If the parameter number does not exist the defult (value 0) information is displayed.

Function DoUpdate(*n*) simulates the action of sending a content update from CasparCG client to server. Several content strings are present, selected to check operations when one, two or all 3 fields change values. One string provides null content for all fields which causes the template to hide the strap. A subsequent call with non-null field content causes the strap to animate onto the output with the new field content in place.

