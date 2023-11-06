# streamlit contact form template

![contact-form](/img/screenshot.png)

## About
This repository contains a contact form template (`pages/contact-form.py`) as a separate page for streamlit apps, using exclusively python libraries and streamlit elements, and will therefore fit right in with your already set up app.

The template contains e-mail validation using [email-validator](https://pypi.org/project/email-validator/) and customizable CAPTCHA generation through python's [captcha](https://pypi.org/project/captcha/) library. Configuration should be done using [dotenv](https://pypi.org/project/python-dotenv/) and messages sent using the [smtplib](https://docs.python.org/3/library/smtplib.html) SMTP protocol client.

## Configuration

This application uses environment variables stored in a .env file for configuration. Make sure to create a .env file in the pages folder with the following variables:

    OPTIONS: A string of characters that can be included in the CAPTCHA. (e.g. ACDEFGHIJKLMNOQPRSTUVWXYZ123456789)
    SERVER: Your SMTP server address. (e.g. smtp.gmail.com)
    PORT: The port for your SMTP server. (e.g 587)
    U: Your SMTP username. (the e-mail address that will send the message, e.g. user@example-email.com)
    SECRET: Your SMTP password.
    RECIPIENT: The recipient email address where messages will be sent. (e.g .recipient@example-email.com)

You can use [gmail](https://support.google.com/a/answer/176600?hl=en) for your SMTP configuration.

## Setup

After you have configured your SMTP, uncomment the lines relative to "Email configuration" in `pages/contact-form.py` (lines 90-116, v0.1.0): 

``` python                   
#smtp_server = server
#smtp_port = port
#smtp_username = u
#smtp_password = secret
#recipient_email = recipient

## Create an SMTP connection
#server = smtplib.SMTP(smtp_server, smtp_port)
#server.starttls()
#server.login(smtp_username, smtp_password)

## Compose the email message
#subject = "Contact Form Submission" # subject of the e-mail you will receive upon contact.
#body = f"Email: {email}\nMessage: {message}"
#msg = MIMEMultipart()
#msg['From'] = smtp_username
#msg['To'] = recipient_email
#msg['Subject'] = subject
#msg.attach(MIMEText(body, 'plain'))

## Send the email
#server.sendmail(smtp_username, recipient_email, msg.as_string())

## Close the SMTP server connection
#server.quit()

#st.success("Sent successfully!") # Success message to the user.
```

and comment or delete the mock-up information (lines 119-120, v0.1.0):

``` python
st.info("""This would have been a message sent successfully!  
For more information on activating the contact form, please check the [documentation](https://github.com/jlnetosci/streamlit-contact-form).""") # Please delete this info box if you have the contact form setup correctly.
```

The contact form should be fully functional.

You can test a quasi-functional contact form at https://contact-form-template.streamlit.app/