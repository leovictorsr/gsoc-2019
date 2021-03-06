This snippet is my way to think ahead what the usage of the CLI for Spidermon should be

With this gist I intend to be able to detect requirements and to have a good planning for the CLI implementation.

The CLI for Spidermon is a project for the GSoC 2019.


# help

```
$ spidermon help
```
This would be automatically generated by the usage of click library, and is part of documentation process.

# monitors

```
$ spidermon setup monitors
$ This is a list of monitors available
[1] Basic Scrapy Suite - Item Count
[2] Basic Scrapy Suite - Error Count
[3] Basic Scrapy Suite - Finish Reasons
[4] Basic Scrapy Suite - Unwanted HTTP Codes
[5] Text in response
Which monitor do you want to configure and enable? [1-5]: 1
$ How much items is the minimum to be notified?: 6
$ Do you want to configure and enable any more monitors?: y
$ This is a list of monitors available
[1] Item Count
[2] Error Count
[3] Finish Reasons
[4] Unwanted HTTP Codes
[5] Text in response
Which monitor do you want to configure and enable? [1-5]: 2
$ How much errors is the minimum to be notified? [default=0]: 10
$ Do you want to configure and enable any more monitors?: n
You have your monitors configured now! You're good to go.
```

An alternate approach would be:
```
$ spidermon setup monitors
$ Do you want to setup the Item Count Monitor [Y/n]: y
$ How much items is the minimum to be notified?: 6
$ Do you want to enable the Error Count Monitor [Y/n]: y
$ How much errors is the minimum to be notified? [default=0]: 10
$ Do you want to enable the Finish Reason Monitor [Y/n]: y
$ Which finish reasons do you want to track to be notified [default=finished]: finished error foo 
$ Do you want to enable the Unwanted HTTP Codes Monitor [Y/n]: y
$ Define a code to the first list of codes: 40
$ Which HTTP codes do you want to track under the code {40}: 403 404
$ Do you want to add any more list of codes [Y/n]: y
$ Define a code to the second list of codes: 50
$ Which HTTP codes do you want to track under the code {50}: 500 501 503
$ Do you want to add any more list of codes [Y/n]: n
Thanks for enabling the Basic Scrapy Suite! You have configured built-in monitor(s) now. 
```

# actions

```
$ spidermon setup actions
$ This is the list of actions to be performed after monitors are run:
[1] Send email
[2] Slack notification
[3] Job tags
[4] File report
[5] S3 report
[6] Sentry
Which action do you want to enable and configure [1-6]: 1
$ Which AWS access key is to be used: AKIAIOSFODNN7EXAMPLE
$ Which AWS secret key is to be used: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
$ Which address should be used to send the email: leovictorsr@gmail.com
$ Which address should be used to receive the email: leonardo.rodrigues@gmail.com
Thanks for configuring the Email Sender action!
$ Do you want to receive an example email from the Email Sender action? [Y/n]: Y
Email sent succesfully!
$ Do you want to enable and configure any more actions?: y
$ This is the list of actions to be performed after monitors are run:
[1] Send email
[2] Slack notification
[3] Job tags
[4] File report
[5] S3 report
[6] Sentry
Which action do you want to enable and configure [1-6]: 2
$ Which name should be used to send the notification?: SlackMonitor
$ Which recipient should be used to send the notification?: #spidermon
$ Which Slack API token is to be used: ab213234_cHJscaJRFVN
Thanks for configuring the Slack Notification action!
$ Do you want to receive an example notification from the Slack Notification action? [Y/n]: Y
Notification sent succesfully!
$ Do you want to enable and configure any more actions?: y
$ This is the list of actions to be performed after monitors are run:
[1] Send email
[2] Slack notification
[3] Job tags for Scrapy Cloud
[4] File report
[5] S3 report
[6] Sentry
Which action do you want to enable and configure [1-6]: 3
$ Which tag should be added to the job after failing: failed
$ Which tag should be removed from the job after running: running
$ Do you want to enable and configure any more actions?: y
$ This is the list of actions to be performed after monitors are run:
[1] Send email
[2] Slack notification
[3] Job tags
[4] File report
[5] S3 report
[6] Sentry
Which action do you want to enable and configure [1-6]: 4
$ Which template do you want to use for report? [default=reports/email/monitors/result.jinja]: 
$ What's the report title?: 'Spidermon File Report'
$ Where the report should be saved [default=./report.html]:
$ Do you want to enable and configure any more actions?: y
$ This is the list of actions to be performed after monitors are run:
[1] Send email
[2] Slack notification
[3] Job tags
[4] File report
[5] S3 report
[6] Sentry
Which action do you want to enable and configure [1-6]: 5
$ Please provide the S3 bucket: bucket
$ Please provide the S3 region endpoint: http://s3-sa-east-1.amazonaws.com
$ Where the report should be saved? report.html
$ Is the report going to be public [Y/n]: n
$ Do you want to enable and configure any more actions?: y
$ This is the list of actions to be performed after monitors are run:
[1] Send email
[2] Slack notification
[3] Job tags
[4] File report
[5] S3 report
[6] Sentry
Which action do you want to enable and configure [1-6]: 6
$ Please provide the Sentry DSN: https://ssnfeuSND@sentry.io/10236
$ What's the project name: 'Spidermon Monitor'
$ Do you want to receive an example notification from the Sentry action? [Y/n]: Y
Notification sent succesfully!
$ Do you want to enable and configure any more actions?: n
Thanks for enabling and configuring our built-in actions! You're good to go.
```

# validation

For JSON Schema:
```
$ spidermon setup validation
$ Do you want to enable item validation [Y/n]: y
$ This is the list of item validation methods
[1] JSON Schema
[2] schematics
[3] cerberus
Which validation method you want to use?: 1
$ This is the list of items available
[1] QuoteItem
[2] ResponseItem
[3] PhotoItem
Which item do you want to enable validation?: 1
Your template JSON schema was created in /path/to/quoteitem.json, add your validation rules and you're good to go!
$ Do you want to enable any more item validation [Y/n]: y
$ This is the list of items available
[1] QuoteItem
[2] ResponseItem
[3] PhotoItem
Which item do you want to enable validation?: 2
Your template JSON schema was created in /path/to/responseitem.json, add your validation rules and you're good to go!
$ Do you want to enable any more item validation [Y/n]: n
Thanks for enabling and configuring validations! Remember to add your validation rules and you're good to go!
```

For schematics:
```
$ spidermon setup validation
$ Do you want to enable item validation [Y/n]: y
$ This is the list of item validation methods
[1] JSON Schema
[2] schematics
[3] cerberus
Which validation method you want to use?: 2
$ This is the list of items available
[1] QuoteItem
[2] ResponseItem
[3] PhotoItem
Which item do you want to enable validation?: 1
Your template JSON schema was created in /path/to/quoteitem.py, add your validation rules and you're good to go!
$ Do you want to enable any more item validation [Y/n]: y
$ This is the list of items available
[1] QuoteItem
[2] ResponseItem
[3] PhotoItem
Which item do you want to enable validation?: 2
Your template JSON schema was created in /path/to/responseitem.py, add your validation rules and you're good to go!
$ Do you want to enable any more item validation [Y/n]: n
Thanks for enabling and configuring validations! Remember to add your validation rules and you're good to go!
```

For future cerberus usage:
```
$ spidermon setup validation
$ Do you want to enable item validation [Y/n]: y
$ This is the list of item validation methods
[1] JSON Schema
[2] schematics
[3] cerberus
Which validation method you want to use?: 3
$ This is the list of items available
[1] QuoteItem
[2] ResponseItem
[3] PhotoItem
Which item do you want to enable validation?: 1
Your template JSON schema was created in /path/to/quoteitem.yaml, add your validation rules and you're good to go!
$ Do you want to enable any more item validation [Y/n]: y
$ This is the list of items available
[1] QuoteItem
[2] ResponseItem
[3] PhotoItem
Which item do you want to enable validation?: 2
Your template JSON schema was created in /path/to/responseitem.yaml, add your validation rules and you're good to go!
$ Do you want to enable any more item validation [Y/n]: n
Thanks for enabling and configuring validations! Remember to add your validation rules and you're good to go!
```
