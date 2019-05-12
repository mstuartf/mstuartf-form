# aws-contact-form


(1) Install AWS cli and setup credentials

`$ pip install awscli`

In the top right corner of the AWS console, go to [your username] > My Security Credentials. Then click 'Create New Access Key' and download the file generated. (Best to keep the keys on screen as you will need them.)

`$ aws configure`

Follow the prompts to enter your credentials. When finished you should see a ./aws/credentials file in your root. 

(2) Copy the repo

`$ git clone https://github.com/mstuartf/aws-contact-form.git`

If you want to break the link to this project and start a new repo, run:

`$ rm -rf .git`

`$ git init`

`$ git add .`

`$ git commit -m "inital commit"`

(3) Install packages

`$ cd aws-contact-form`

`$ virtualenv env`

`$ . env/bin/activate`

`$ pip install -r requirements.txt`

(4) Configure

Set `SENDER_EMAIL` and `RECIPIENT_EMAIL` (these can be the same; make sure both are verified on AWS SES).

Change the `aws_region`, `project_name` and `s3_bucket` in zappa_settings.json.

(5) Test locally

`$ FLASK_APP=app.py flask run`

Then send a POST request using Postman / python requests / etc. to http://127.0.0.1:5000/new_enquiry

Any JSON payload is fine - it will just get forwarded to the recipient address.

(6) Deploy

`$ zappa deploy`

In the logs you will see:

`Creating [your-project-name]-prod-ZappaLambdaExecutionRole IAM Role..`

Go to AWS IAM > Roles > and give AmazonSESFullAccess to this Role

(7) Update

You will need to update once you have updated the IAM Role:

`$ zappa update`

(8) Test Live

The url will be printed in terminal: 

`Deployment complete!: https://[your-key].execute-api.[your-region].amazonaws.com/prod`
