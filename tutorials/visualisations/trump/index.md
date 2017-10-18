---
layout: tutorial
datasources: twitter
coding: a little
skills: creating vector-based visualistion, import library
title: tutorial - trump clock
duration: 20 minutes
---

This tutorial will get you familiar with using the UIBuilder to build high quality data-driven realtime visualisations.  By the end you will have a picture of trump that changes in response to the sentiment analysis performed on incoming tweets.  Trump's arm and the clock pointer will move in response to the sentiment score of the current tweet, and the tweet will be displayed on the green bar beneath trump.  All of the graphics have ben pre-made for you.

<figure class="figure">
  <img src="/images/tutorial/trump/apptest.png" class="thumbnail" width="60%" alt="trump clock">
  <figcaption class="figure-caption text-center">trump clock</figcaption>
</figure>

#### 1. connect the nodes together

First of all, lets connect together all of the nodes that will be used in creating this app:

<figure class="figure">
  <img src="/images/tutorial/trump/step1.svg" class="thumbnail" width="60%" alt="step one">
  <figcaption class="figure-caption text-center">step one - connect the flows</figcaption>
</figure>

The twitter node will provide the latest tweets (it can be configured by the user at app install time, using the twitter driver settings).  The tweets are sent to a **dbfunction** that will analyse for sentiment, and then send on the tweet and its score to the **uibuilder** node, which will craft the visualisation.  This visualisation will be sent to the **app**, which displays the visualisation in the databox dashboard.  So the main work in this app will be done in the dbfunction and the uibuilder app.  We also hook up a debugger node to the output of the function - this is always useful as a way of sanity checking the output. Lets write the function first.

#### 2. write the sentiment analysis code

Double click on the dbfunction node.  Here is the place that we want to write a function.  We want it to return an object with a payload that contains the sentiment score and the tweet, i.e.:

```javascript
return {
	tweet: [the tweet]
	score: [the tweet's sentiment score]
}
```

Fortunately for us, there's an npm library that performs sentiment analysis of arbitrary text, which we can use, rather than code it up ourselves.  Let's import it at the top of our function:

```javascript

var sentiment = require("sentiment");

return {
	tweet: [the tweet]
	score: [the tweet's sentiment score]
}
```

Currently the dbfunction node does not support the es6 'import' syntax, though this will soon change.    We now need to take the tweet from the incoming twitter message.  To find the format of the message, click on 'there are one inputs to this function', and you'll see that the incoming message has a schema with (alongside other attributes) a payload which has a 'value' and 'ts'.  Where 'value' is the tweet.  Therefore the latest tweet is:

```javascript
msg.payload.value
```

Incidentally, the dbfunction can automatically assign variables to the incoming message to save you the bother of looking up the schema.  You'll see down the left hand side of the function that the twitter node is listed under **in**.  If you click on that, it will generate the code that assigns variables to the input message's attributes:

```javascript
//the container object
const {name:msg_name,id:msg_id,type:msg_type,subtype:msg_subtype,payload:msg_payload} = msg;
 //the payload object
const {ts:msg_payload_ts,value:msg_payload_value} = msg_payload;
```

So a variable called <i>msg_payload_value</i> has been created with the tweet assigned to it.

Now that we have the message, we can run it through the [sentiment](https://github.com/thisandagain/sentiment) library, which will then provide an object with <i>score</i> (which is the aggregate value of the sentiment values for each token in the string) and <i>comparative</i> which is a normalised score ranging from -5 to 5 (with 5 being the most positive, 0 neutral and -5 the most negative).  To make this easier to work with we convert it to a scale from 0 to 10, where 10 is the most negative and 0 the most positive.  Our code ends up as:

```javascript
var sentiment = require("sentiment");
var r = sentiment(msg.payload.value);

//r.comparative is between -5 and 5, so convert o scale 0-10 (where 0 is most negative)
var score = (r.comparative * -1) + 5;

return {
    payload: {
        tweet: msg.payload.value,
        sentiment: score,
    }
}

```

Finally, there is a bit of a sting in the tail.  All nodes in the sdk have associated data 'schemas' which allow nodes to know the format of data coming in or expected from their outputs.  In order to use the data from the dbfunction, the **uibuilder** node will need to know the format of the message coming in.  You'll see a final box in the dbfunction called 'output schema', where the details of the format of the output can be added.   The sdk uses [json schema](http://json-schema.org/) to define messages.  The messages coming from this node can be described in json-schema as:

```javascript
{
    "name": "container object",
    "type": "object",
    "properties": {
        "payload": {
            "type": "object",
            "properties":{
                "tweet": {"type":"string"},
                "sentiment": {"type": "number"}
            }
        }
    }
}
```

This is hopefully reasonably clear.  It is saying that the output is an object with one property called payload, which is itself an object with two properties: tweet (a string) and sentiment (a number).  Copy this schema into the 'output schema' box, and you are done.

#### 3. configure uibuilder

Now we need to create our visualisation of trump.  Double click on the uibuilder node.  You will be presented with a blank canvas.  Make your browser as large as possible to give yourself as much screen real estate as possible.   On the left-hand side is a palette of tools.  Click on <img src="/images/tutorial/gauge/librarybutton.png" style="display:inline-block; width: 30px"> (click it again to toggle the image library).

First lets drag in the background image:

<figure class="figure">
  <img src="/images/tutorial/trump/uibuilder1.png" class="thumbnail" width="60%" alt="uibuilder: drag in the background">
  <figcaption class="figure-caption text-center">uibuilder: drag in the background</figcaption>
</figure>

Give it a label such as 'background' on the right hand side of the screen.  And adjust the width to fill the box (it is easier to do this using the width text box on the right hand side of the screen). Now we need to create a circle that trump will sit in:

<figure class="figure">
  <img src="/images/tutorial/trump/uibuilder2.png" class="thumbnail" width="60%" alt="uibuilder: drag in the background">
  <figcaption class="figure-caption text-center">uibuilder: drag in a circle </figcaption>
</figure>

You can set the attributes of the circle on the right hand side of the screen.  Give it a label such as "backbluecircle" and a "fill" of #203C51.  Now we will pull in the pointer that moves round based on the tweet value.  Click on <img src="/images/tutorial/gauge/librarybutton.png" style="display:inline-block; width: 30px"> again and drag in the stick with the missile on top:

<figure class="figure">
  <img src="/images/tutorial/trump/uibuilder3.png" class="thumbnail" width="60%" alt="uibuilder: drag in the background">
  <figcaption class="figure-caption text-center">uibuilder: drag in the pointer </figcaption>
</figure>

Give it a label such as "pointer". Let's also add a place for the tweet to be shown.  Drag in some text from the palette (the A icon):

<figure class="figure">
  <img src="/images/tutorial/trump/uibuilder4.png" class="thumbnail" width="60%" alt="uibuilder: drag in text for tweet">
  <figcaption class="figure-caption text-center">uibuilder: drag in text for tweet </figcaption>
</figure>

Give it a label such as 'tweet' and set the text to something like 'trump latest tweet', which is the initial value it will be given.


##### connect up some data 

Ok lets connect up some data to what we currently have.  First, we want our tweet text to show the latest tweet.  Select the text then on the right hand side, click on 'mapper'.  This will give a list of all data that is currently connected to this node. If you click on "tweet sentiment", you will see that it has a breakdown of its attributes (which is why you needed to write the json-schema earlier!).  For sources, click on 'tweet' and for attributes click on 'text'.  So we are saying map the tweet from our data to the 'text' of our text.

<figure class="figure">
  <img src="/images/tutorial/trump/uibuilder5.png" class="thumbnail" width="60%" alt="uibuilder: map tweet to text">
  <figcaption class="figure-caption text-center">uibuilder: map tweet to text </figcaption>
</figure>

Once done, you should see a new 'transformer' has been created.  Transformers allow us to modify the way the mapping works (which we shall see shortly).

We want our pointer to rotate round the circle, with the pointer getting closer to 12 o'clock (doomsday) with the most negative sentiment score (10).  Click on the pointer, and in the mapper window, we want to connect the source sentiment to the attribute rotation.  Again this will set up a transformer.  Unlike the previous mapping the relationship between sentiment (0-10) to rotation (0-360) is not one-to-one.  We want to adjust it, which we can do by clicking on the transformer that has just been created (tweet sentiment:sentiment -> pointer:rotate).  The transformer shows us a bunch of detail:

<figure class="figure">
  <img src="/images/tutorial/trump/uibuilder6.png" class="thumbnail" width="60%" alt="uibuilder: sentiment transformer">
  <figcaption class="figure-caption text-center">uibuilder: sentiment transformer</figcaption>
</figure>

Instead of the default:

```javascript
return `rotate(${sentiment%360})`
```

We want:

```javascript
return `rotate(${sentiment/10*360})`
```

i.e. rotate as a fraction of the highest score (10).  Once changed, click on ok.

Let's test what we have so far.  Click on ok, then click on 'test' and wait for the container to build. If all works ok, after a while a new tweet will come in and update the text, and the pointer will rotate round the circle (based on sentiment score):

<figure class="figure">
  <img src="/images/tutorial/trump/uibuilder7.png" class="thumbnail" width="60%" alt="uibuilder: test output">
  <figcaption class="figure-caption text-center">uibuilder: test output</figcaption>
</figure>


