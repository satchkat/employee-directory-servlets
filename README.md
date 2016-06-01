# SMS/MMS Employee Directory on Servlets

[![Build status](//ci.appveyor.com/api/projects/status/github/TwilioDevEd/employee-directory-servlets?svg=true)](//ci.appveyor.com/project/TwilioDevEd/employee-directory-servlets)

Use Twilio to accept SMS messages and translate them into queries against a SQL database. This example functions as an Employee Directory where a mobile phone user can send a text message with a partial string of the person's name and it will return their picture and contact information (Email address and Phone number).

[Read the full tutorial here](//www.twilio.com/docs/tutorials/walkthrough/employee-directory/java/servlets)

### Prerequisites

1. [Java 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed in your operative system
1. A Twilio account with a verified [phone number][twilio-phone-number]. (Get a [free account](//www.twilio.com/try-twilio?utm_campaign=tutorials&utm_medium=readme) here.).  If you are using a Twilio Trial Account, you can learn all about it [here](https://www.twilio.com/help/faq/twilio-basics/how-does-twilios-free-trial-work).

### Download and Run the Application

1. First clone this repository and `cd` into it:
   ```
   git clone git@github.com:TwilioDevEd/employee-directory-servlets.git
   cd employee-directory-servlets
   ```

1. Edit the sample configuration file `.env.example` and edit it to match your configuration.

   You can use the `.env.example` in a unix based operating system with the `source` command to load the variables into your environment:

   ```bash
   $ source .env.example
   ```

   If you are using a different operating system, make sure that all the
   variables from the `.env.example` file are loaded into your environment.

1. Make sure the tests succeed.

   ```bash
   $ ./gradlew check
   ```

1. Start the server.

   ```bash
   $ ./gradlew appRun
   ```

1. Expose your local web server to the internet using ngrok. You can click [here](https://www.twilio.com/blog/2015/09/6-awesome-reasons-to-use-ngrok-when-testing-webhooks.html) for more details.
This step is important because the application won't work as expected if you run it using `localhost`.

   ```bash
   $ ngrok http 8080
   ```
Once ngrok is running, open up your browser and go to your ngrok URL. It will look something like this:

  `http://<sub-domain>.ngrok.io/`

1. Configure Twilio to call your webhooks

  You will also need to configure Twilio to call your application when calls are received
  on your _Twilio Number_. The **SMS & MMS Request URL** should look something like this:

  ```
  http://<sub-domain>.ngrok.io/directory/search
  ```

  ![Configure SMS](http://howtodocs.s3.amazonaws.com/twilio-number-config-all-med.gif)

That's it!

# Running the app

Each time the applications loads the `IndexServlet#init` function will create a new SQLite database called `employee_db.sqlite`, seeded with data from the `seed-data.jso`n file, ie.: Data provided by Marvel. &copy; 2016 MARVEL.

1. You can query the employees by sending sms to your [Twilio Phone Number][twilio-phone-number]. To send free sms you can use [Text+](http://www.textplus.com/).
1. To query employees in your application directly from the web check [http://localhost:8080](http://localhost:8080) or the `http://<sub-domain>.ngrok.io` domain generated by ngrok.

### How To Demo?

1. Text your twilio number the name "Iron"
1. Should get the following response:

   ```
   We found multiple people, reply with:
   1 for Iron Man
   2 for Iron Clad
   Or start over
   ```
1. Reply with 1
1. Should get the following response:

   ```
   Iron Man
   +14155559368
   +1-202-555-0143
   IronMan@heroes.example.com
   [the image goes here]
   ```
1. If your query matches only one employee, he/she will be returned immediately. Eg.: "Spider" will return in the web version:

 ![Query an employee partially](https://s3.amazonaws.com/com.twilio.prod.twilio-docs/images/employee-directory-lookup.original.png)

## Meta

* No warranty expressed or implied. Software is as is. Diggity.
* [MIT License](http://www.opensource.org/licenses/mit-license.html)
* Lovingly crafted by Twilio Developer Education.

[twilio-phone-number]: https://www.twilio.com/console/phone-numbers/incoming