In the IEEE format, for example, one should not use any personal pronouns. The use of "I", "me", "we", or "us" is not advised. There is a way for developers to alert users of style issues and offer suggestions of how to fix it. It may be a style issue like pronouns, or it may be spelling or grammar. 

More abstract, it is a way for a developer to markup any type of text and give users any type of note. Moreover, developers can use regular expressions to make marking up much easier.

Marked text will be underlined in a green-blue color. When hovered over, it will show a hovertag. Clicking the hovertag opens the Context Panel which includes more details about the issue and provides actions.

### OnStyleMarkup
The Context API is tied to the format using the function `onStyleMarkup()`. From this function, we can create various types of text markups that are placed in `window.context`
*Note:* Do not directly modify the `window.context` variable. The functions below will do that.

### Apply Context
To apply context markup, call this function:
`apply_context(text, d)`
* text - A regular expression containing the type of text you want to look for. This should be represented as a string and NOT A REGULAR EXPRESSION

Ex: `"[Ss]tudent [Bb]ody"`

NOT: `/[Ss]tudent [Bb]ody/gi`

* d - Data; a JSON object containing various properties of this context markup

#### Object Properties

##### Required

Please include these properties. Other properties are optional and can modify the behavior in the "suggestions" section of the Context Panel
* type - This is the reason why text was marked. Also, this text appears in the hovertag.

** If type is "Don't Overuse", then you can use the limit parameter
* text - This is HTML containing full details about why the text was marked

##### Not required
* replacement - If this parameter is included, it includes an action named "Replace all with {text}".
* limit - Including a type of "Don't Overuse", the system compares how often the given regular expression appears in the content. This parameter is a fraction, or decimal, that gives the frequency. For example, if `limit: 0.5`, then the system will flag that regular expression if it returns true more than half of the time compared to the number of words written. (Given this is the literal frequency, numbers lower than 0.5 will be more practical.)

### Context Service
It is preferred to link the Context API solely to a format, as each format has different rules. If one is fully inclined to create a service that will also check your context, you must override the onStyleMarkup function and add it to your InitPanel function.

```JavaScript
(function(){
    //saving the original function
    var preservedFnc = onStyleMarkup

    //overriding function
    onStyleMarkup = function() {
        preservedFnc.apply();
        /** New code here **/
    }
})()
```
