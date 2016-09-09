## How to use Sendgrid the right way

When we were trying to integrate Sendgrid with our website we realized that there wasn’t a way to add an user to a Sendgrid mailist and also send him a transactional email saved as a templeated.

We look for the Sendgrid docs and we saw that you can add a recipient with a post and also with the Sengrid nodejs api you can send transactional template emails.

So what we did was using the Sengrid nodejs api and Superagent module to create this script that automatically register the user on the contact mailist and also sends him the transactional email.

```
var request = require(‘superagent’)
var sendgrid = require(‘sendgrid’)(‘YourToken’)
//Registering the user to the mailing list
request
.post(‘https://api.sendgrid.com/v3/contactdb/recipients’)
.set(‘Content-Type’, ‘application/json’)
.set({‘Authorization’: ‘Bearer YourToken’})
.send([{’email’: email@email.com}])
.end(function (err, response) {
  res.send(‘<h1> Thank you for your Subscription</h1>’)
  //Sending the transactional email to the user
  var email = new sendgrid.Email();
  email.addTo(email_id);
  email.subject = “Thank you for Signing Up!”;
  email.from = ‘fromEmail’;
  email.replyto = “toEmail”;
  email.html = ‘ ‘;
  // add filter settings one at a time
  email.addFilter(‘templates’, ‘enable’, 1);
  email.addFilter(‘templates’, ‘template_id’, ‘ID’);
  // or set a filter using an object literal.
  sendgrid.send(email, function(err, json) {
    if (err) return console.error(err)
    console.log(json);
  })
})
```
             

Hope you find this code usefull